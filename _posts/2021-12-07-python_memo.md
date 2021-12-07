---
title: Pythonについての備忘録
tags: tips
---
何回もする操作なのに、すぐ忘れるものを一覧にしました。自分用のメモです。

## ライブラリ関係
### 自作の関数を使いたいとき

自作の関数が格納されているディレクトリのpathを通す必要がある。
```python
import sys
sys.path.append("path_directory")
import my_module
```

## ディレクトリ操作
### current directoryの確認
```python
os.getcwd()
```
### ディレクトリの移動
```python
os.chdir(dir_path)
```
### 現在のディレクトリ内のすべてのtifファイルの名前を取得
```python
list_tif = glob.glob(os.path.join(r"*.tif"))
```
### 目的のファイルがあるか確認
```python
os.path.exists('file_name')
```

## matplotlib

### 作図用のパラメータを一括で変更する
見た目を一括で変更するには`plt.rcParams`を使えばいい。
だいたいいつも次のように設定している。  
[matplotlibのドキュメントの該当部分](https://matplotlib.org/stable/tutorials/introductory/customizing.html)

```python
plt.rcParams['font.size'] = 16                  #全体のフォントサイズ
plt.rcParams["xtick.labelsize"] = 12            #x軸のラベルのフォントサイズ
plt.rcParams["ytick.labelsize"] = 12            #y軸のラベルのフォントサイズ
plt.rcParams['font.sans-serif'] = 'Helvetica'   #フォント
plt.rcParams['mathtext.fontset'] = 'cm'         #数式用フォント
plt.rcParams['xtick.direction'] = 'in'          #x軸のメモリの向き
plt.rcParams['ytick.direction'] = 'in'          #y軸のメモリの向き
plt.rcParams['xtick.major.width'] = 2.4         #x軸の太さ
plt.rcParams['ytick.major.width'] = 2.4         #y軸の太さ
plt.rcParams['axes.linewidth'] = 2.4            #囲みの太さ
plt.rcParams['axes.grid']=True                  #gridをつけるか
plt.rcParams['grid.linestyle']='--'             #gridの線の種類
plt.rcParams['grid.linewidth'] = 1.6            #gridの太さ
plt.rcParams["legend.markerscale"] = 2          #legendの点の大きさ
plt.rcParams["legend.fancybox"] = False         #legendの角を丸めるかどうか
plt.rcParams["legend.framealpha"] = 1           #legend背景の透過率
plt.rcParams["legend.edgecolor"] = 'black'      #legendの囲み線の色
plt.rcParams["xtick.major.size"] = 3            #x軸主目盛り線の長さ
plt.rcParams["ytick.major.size"] = 3            #y軸主目盛り線の長さ
plt.rcParams['figure.dpi'] = 60                 #図の解像度
plt.rcParams["xtick.major.pad"] = 2             #x軸の数字とグラフ間の間隔
plt.rcParams["ytick.major.pad"] = 2             #y軸の数字とグラフ間の間隔
plt.rcParams["axes.labelpad"] = 1               #ラベルと軸の間の間隔 (defaultは4.0)
```

### 複数の図を表示
```python
h, w = 2, 3 #高さ方向に何個並べるか、横方向に何個並べるか
fix, axes = plt.subplots(h, w, figsize=(20, 15))
plt.subplots_adjust(wspace=0.2, hspace=0.3)
for i, ax in enumerate(axes.ravel()):
    ax.plot(data[i])
```
### legendの表示場所の指定
legendを指定する時のオプションでlegend自体の表示場所も指定できる。下の例はレジェンドを図の外の右上に表示している。
```python
ax.legend(["result1", "result2"], frameon=False, bbox_to_anchor=(1.05, 1), loc='upper left')
```
### 図の保存
背景を透明にしたいときは、下のようにオプション`transparent=True`をつければよい。
```python
plt.savefig("figure.svg", bbox_inches='tight', transparent=True)
```

## scipy

<!--more-->
