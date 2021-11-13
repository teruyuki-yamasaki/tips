# tips


Xのaxis=-2の配列をそれぞれaxis=-1の最小値の配列に置き換える
```
Xmin = np.min(X, axis=-1, keepdims=True) * np.ones_like(X)
print(Xmin)
```

同サイズの2次元画像データ同士の各ピクセル周りのpatchの差分のペアワイズ
```
import numpy as np 

X = np.random.randint(1,8,(2,3,4))
print("X=")
print(X) 

X1 = X.reshape(X.shape[0], X.shape[1], 1, -1)
print("X1=")
print(X1)

X2 = X.reshape(X.shape[0], X.shape[1], 1, X.shape[2]) * np.ones((X.shape[0], X.shape[1], X.shape[1], X.shape[2]))
print("X2=")
print(X2)

X3 = np.transpose(X2, axes=(0,2,1,3))
print("X3=")
print(X3)

X2 - X3
```
patches_leftの(yi, xj)とpatches_right(yi, xk) k = 0,1,...,n-1のssd[y,xj,x0:n-1]を計算したい
    # 各y = yiについて、patches_left[yi,:]とpatches_right[yi,:]のssdの2次元対応表ssd[yi]を作る
    # 各y = yiについて、patches_left[yi,:]とpatches_right[yi,:]の差分ベクトルの2次元対応表diff[yi]を作り、ssdを計算 np.sum(diff**2, axis=-1)
    # patches_leftについては、各y=yiにおいて、各x=xjのpatch[i,j]をそれぞれaxis=2の方向にn回複製する
    # patches_leftは、X.reshape(X.shape[0],X.shape[1],1,X.shape[2])として1軸増やしてから、np.ones((X.shape[0],X.shape[1],X.shape[1],X.shape[2]))を*でかけて
    # patches_rightについては、各y=yiにおいて、axis=1方向のpatch[i,1:n]をaxis=2の方向に並べ直し、これをaxis=1方向にn回複製する
    # patches_rightは、patches_leftと同じ処理をしてからnp.transpose(X, axes=(0,2,1,3))とすれば良い
