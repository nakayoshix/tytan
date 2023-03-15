# TYTAN（タイタン）
大規模QUBOアニーリングのためのSDK

## 問題形式
QUBO形式

## 問題サイズ
ローカル：1,000量子ビット程度   
API経由：1,000-10万量子ビット程度

## インストール
```
pip install tytan
```

```
pip install git+https://github.com/tytansdk/tytan
```

## 計算
```
from tytan import *

# QUBOを設定
qubo = {('s3', 's3'): -196.0,
 ('s2', 's2'): -96.0,
 ('s3', 's2'): 112.0,
 ('s1', 's2'): 64.0,
 ('s3', 's1'): 224.0,
 ('s4', 's3'): 56.0,
 ('s4', 's4'): -52.0,
 ('s4', 's1'): 32.0,
 ('s4', 's2'): 16.0,
 ('s1', 's1'): -160.0}

# サンプラーを選択
sampler = sampler.SASampler()

# 計算
res = sampler.run(qubo, shots=100)

# 結果を出力
print(res)

[[{'s1': 1, 's4': 1, 's3': 0, 's2': 1}, -196.0, 1.0],
 [{'s1': 0, 's4': 1, 's3': 1, 's2': 0}, -192.0, 1.0],
 [{'s1': 1, 's4': 0, 's3': 0, 's2': 1}, -192.0, 1.0],
 [{'s1': 0, 's4': 0, 's3': 1, 's2': 1}, -180.0, 1.0],
 [{'s1': 0, 's4': 1, 's3': 1, 's2': 1}, -160.0, 1.0],
 [{'s1': 0, 's4': 1, 's3': 0, 's2': 1}, -132.0, 1.0],
 [{'s1': 1, 's4': 1, 's3': 1, 's2': 0}, -96.0, 1.0],
 [{'s1': 1, 's4': 0, 's3': 1, 's2': 1}, -52.0, 1.0],
 [{'s1': 0, 's4': 0, 's3': 0, 's2': 0}, 0.0, 1.0],
 [{'s1': 1, 's4': 1, 's3': 1, 's2': 1}, 0.0, 1.0]]
```

# サンプラー
SASampler()

# コントリビューター
https://github.com/tytansdk/tytan/graphs/contributors

# 著作権
Copyright 2023 TYTAN TEAM
