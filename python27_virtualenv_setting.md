# Python 2.7 で virtualenv を使った仮想環境構築

# はじめに

Python 2 系で仮想環境の構築方法が分からなかったので、備忘録として構築手順を以下に記述する。
前提条件として、py.exe がインストールされており、Python 2.7 が `C:\python27\` にインストールされているものとする。


# 実施内容

## pip がインストールされているか確認する

下記を実行し、`pip 9.0.1 from C:\Python27\lib\site-packages (python 2.7)` のように pip のバージョンが表示されればインストールされている。

```
> py -2 -m pip -V
```


## virtualenv のインストール

```
> cd C:\python27\Script\
> pip2.7 install virtualenv
```


## virtualenv で仮想環境を構築する

下記を実行すると、仮想環境がカレントディレクトリ下に構築される。
ここで `<env_name>` は、任意の仮想環境の名前である。
カレントディレクトリ以外の場所に環境を構築する場合は、 `<env_name>` にそのパスを含める。

```
> py -2 -m virtualenv <env_name>
```

仮想環境を有効にするには、`<env_name>\Scripts\activate.bat` を実行する。
仮想環境を無効にするには、`<env_name>\Scripts\deactivate.bat` を実行する。

仮想環境にモジュールをインストールするには、仮想環境を有効にし、`python pip install <module_name>` を実行する。
