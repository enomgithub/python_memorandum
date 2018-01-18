# matplotlib の日本語設定 (Windows 10)

# はじめに

matplotlib を試そうと pip でインストールして使用してみたが、デフォルトでは日本語が表示できなかった。そのため、備忘録として設定方法を以下に記す。使用する日本語フォントは [IPAexフォント](https://ipafont.ipa.go.jp/) とした。


## 環境

- Windows 10 Home
- Python 3.6.4


## matplotlib の設定ファイルの場所を確認する

Python の対話モードで下記を実行すると、設定ファイル matplotlibrc が存在するディレクトリが表示される。

```
>>> import matplotlib
>>> matplotlib.matplotlib_fname()
```

`Pythonのインストールディレクトリ\Lib\site-packages\matplotlib\mpl-data\` に matplotlibrc が存在する。`Pythonのインストールディレクトリ` は、例えば C ドライブ直下に Python3.6 をデフォルトでインストールしている場合では `C:\python36\` である。


## IPA フォントのインストール

1. [ここ](https://ipafont.ipa.go.jp/node17#jp) から圧縮ファイルをダウンロードし、任意の場所で解凍する。
2. 解凍したフォルダ内にある `ipaexg.ttf` と `ipaexm.ttf` を、`Pythonのインストールディレクトリ\Lib\site-packages\matplotlib\mpl-data\fonts\ttf` に置く。


## matplotlibrc のコピーと編集

1. `matplotlibrc` を、`~/.matplotlib/` 内に**コピーする**。
2. `~/.matplotlib/` 内にコピーした `matplotlibrc` をエディタで開き、下記のように、`### FONT` 以下の `#font.serif :` に `IPAexMincho` を、`#font.sans-serif :` に `IPAexGothic` を**追加する**。
```
...
### FONT
#
# font properties used by text.Text.  See
...
#font.size           : 10.0
#font.serif          : IPAexMincho, DejaVu Serif, Bitstream Vera Serif, New Century Schoolbook, Century Schoolbook L, Utopia, ITC Bookman, Bookman, Nimbus Roman No9 L, Times New Roman, Times, Palatino, Charter, serif
#font.sans-serif     : IPAexGothic, DejaVu Sans, Bitstream Vera Sans, Lucida Grande, Verdana, Geneva, Lucid, Arial, Helvetica, Avant Garde, sans-serif
#font.cursive        : Apple Chancery, Textile, Zapf Chancery, Sand, Script MT, Felipa, cursive
...
```



## fontList.json の編集

`~/.matplotlib/` 内の `fontList.json` を編集する。

1. `"ttffiles"` 内に、下記のように `ipaexg.ttf` と `ipaexm.ttf` のパスを**追加する**。
```
...
"ttffiles": [
  "Pythonのインストールディレクトリ\\lib\\site-packages\\matplotlib\\mpl-data\\fonts\\ttf\\ipaexg.ttf",
  "Pythonのインストールディレクトリ\\python36\\lib\\site-packages\\matplotlib\\mpl-data\\fonts\\ttf\\ipaexm.ttf",
  ...
```
2. デフォルトフォントを下記のように**書き換える**。
```
...
"defaultFont": {
  "ttf": "Pythonのインストールディレクトリ\\lib\\site-packages\\matplotlib\\mpl-data\\fonts\\ttf\\ipaexg.ttf",
  ...
```
この設定をすると、`matplotlib.pyplot.rcParams["font.family"] = IPAexGothic"` と書かなくても `IPAexGothic` がデフォルトのフォントとして選択される。
3. `"ttflist"` 内に、下記のようにttfフォントの設定を**追加する**。
```
...
"ttflist": [
  {
    "fname": "Pythonのインストールディレクトリ\\lib\\site-packages\\matplotlib\\mpl-data\\fonts\\ttf\\ipaexg.ttf",
    "name": "IPAexGothic",
    "style": "normal",
    "variant": "normal",
    "weight": 400,
    "stretch": "normal",
    "size": "scalable",
    "_class": "FontEntry"
  },
  {
    "fname": "Pythonのインストールディレクトリ\\lib\\site-packages\\matplotlib\\mpl-data\\fonts\\ttf\\ipaexm.ttf",
    "name": "IPAexMincho",
    "style": "normal",
    "variant": "normal",
    "weight": 400,
    "stretch": "normal",
    "size": "scalable",
    "_class": "FontEntry"
  },
  ...
```
