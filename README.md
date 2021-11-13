# tips


テンソルのaxis=-2の配列をそれぞれaxis=-1の最小値の配列に置き換える
```
X = np.random.randint(1,8,(2,3,3,2))
print(X) 

Xmin = np.min(X, axis=-1, keepdims=True) * np.ones_like(X)
print(Xmin)
```
