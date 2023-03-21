# TYTAN（タイタン）
大規模QUBOアニーリングのためのSDK

## 問題形式
QUBO形式

## 問題サイズ
ローカル：1,000量子ビット程度   
API経由：1,000-10万量子ビット程度

## インストール
pipインストールで簡単に導入ができます。

```
pip install tytan
```

github版の方が更新が早いので、こちらの方が基本的には最新です。

```
pip install git+https://github.com/tytansdk/tytan
```

## 計算

### 事前準備

```
# 以下のコード例ではsympyが必要
pip install sympy
```

### コード例
基本的には定式化を行い、ソルバーと呼ばれる問題を解いてくれるプログラムにdict形式で入力をします。下記の例ではsympyを使って数式から入力をしています。数式以外にもcsvやnumpy matrixやpandas dataframeなど様々な入出力に対応しています。

```
from tytan import *
import sympy as sym

# 変数を定義
x, y, z = sym.symbols('x y z')

#式を記述
expr = 3*x**2 + 2*x*y + 4*y**2 + z**2 + 2*x*z + 2*y*z

# Compileクラスを使用して、QUBOを取得
Q, offset = qubo.Compile(expr).get_qubo()

# サンプラーを選択
solver = sampler.SASampler()

# 計算
result = solver.run(Q, shots=100)
print(result)
```

### 出力例
上記の例は入力に変数のラベルごと入力できるので、定式化した変数そのままで数値が戻ってきます。配列となっている答えは、「量子ビットの値」、「エネルギー（コスト）値」、「出現確率」の順で格納されています。

```
[[{'z': 0, 'y': 0, 'x': 0}, 0.0, 8], [{'z': 1, 'y': 0, 'x': 0}, 1.0, 15], [{'z': 0, 'y': 0, 'x': 1}, 3.0, 12], [{'z': 0, 'y': 1, 'x': 0}, 4.0, 11], [{'z': 1, 'y': 0, 'x': 1}, 6.0, 17], [{'z': 1, 'y': 1, 'x': 0}, 7.0, 12], [{'z': 0, 'y': 1, 'x': 1}, 9.0, 16], [{'z': 1, 'y': 1, 'x': 1}, 14.0, 9]]
```

# サンプラー
サンプラーと呼ばれる計算をしてくれるプログラムが搭載されています。TYTANでは基本的には簡単なソルバーを用意はしていますが、ユーザーごとにソルバーを用意して簡単に繋げられるようにしています。ローカルのサンプラーのように手元のマシンにプログラムとして搭載する以外にも、APIのサンプラーでサーバーに接続する専用サンプラーなど様々な形態に対応できます。

ローカルサンプラー：
```
SASampler
GASampler
```

商用クラウドサンプラー：
```
ZekeSampler
NQSSampler　準備中
```

# 商用利用
TYTANは商用利用前提ですので、個人での利用はもちろん企業での活用を許可し、促進しています。

# コントリビューター
https://github.com/tytansdk/tytan/graphs/contributors
