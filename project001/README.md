# 人口統計情報の表示

* 日本の都道府県別人口のcsvを読みこんでグラフを表示する
* csv, matplotlibを使う


## 前準備

### csvの用意

以下のURLからcsvをダウンロードする

https://www.e-stat.go.jp/regional-statistics/ssdsview/prefectures

このとき、「総人口」が項目に含まれるようにする。
コードでは2022年度の情報を使っている。

## 発生した課題と対処

### 人口データが三桁区切り文字列で格納されている

#### 対処

* カンマを消して数値に変換した

```python
int(row['A1101_総人口【人】'].replace(",",""))
```

### 日本語が表示されない

#### 原因

* 初期指定されているフォントに日本語が含まれていない

#### 対処

* rmParamsの値を変更する

```python
rcParams['font.family'] = 'sans-serif'
rcParams['font.sans-serif'] = ['BIZ UDGothic']
```

### 各棒のレジェンドが被って読めない

#### 原因

* 横幅が狭くて文字が重なっている

#### 対処

* 複数の方法を組み合わせて対処した
* レジェンドを45度回転させて被らないようにした

```python
matplotlib.pyplot.xticks(rotation=45)
```

* 文字サイズを調整した

```python
rcParams['font.size'] = 10
```

* グラフ自体の大きさを変更した

```python
matplotlib.pyplot.figure(figsize=(15,6))
```

## アレンジ

* 昇順でソートした
* 人口が200万、500万、それ以上で色を変えた

## 未解決

* 紐づいたデータを管理するいい方法がわからなかった
  * 今回はcollections.namedtupleをつかった