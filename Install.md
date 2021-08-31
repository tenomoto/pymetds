(install)=
# Python環境の構築

Python環境として，環境構築が不要な[Google Colaboratory](https://colab.research.google.com/)を推奨していますが，手元のパソコンに環境を構築したい場合は以下を参考にしてください。

## Conda

AnacondaとMinicondaはAnaconda社が提供しているPythonのディストリビューションです。
Anacondaはデータサイエンスに必要なもののを多くをプレインストールするのに対し，後者は最低限のものだけがインストールされます。
Linux, Windows, Mac上で，Python以外のライブラリもインストールでき，管理者権限が不要で手軽であることから，多くの人が利用しています。
Anaconda/MinicondaはPython以外のライブラリのインストールが難しいWindowsで有用です。
インターネット上の情報も`conda`でインストールするように書いてあるものが大多数だと思います。

私も以前はMinicondaを使っていましたが，いくつか問題があるので現在は使っておらず，お勧めもしていません。
一つ目は自動で環境変数を定義するスクリプトが実行されることです。
UnixやWindows等のOSに詳しくない初心者に対して親切である反面，知らないままに設定されていて問題が生じたときに原因が分かりにくいことがあります。
もう一つは`conda`でインストールできないものがあると，`pip`でインストールすることになり，多重管理になるということです。

## Windows

WindowsではMicrosoft Store，Visual StudioなどでもPythonがインストールできますが，
最新で最も信頼できる[本家](https://www.python.org)からインストーラーをダウンロードしてインストールすることをお勧めします。
以前はインストールが難しかった`scipy`も`pip`だけでインストールできます。
`cartopy`の[インストール](https://scitools.org.uk/cartopy/docs/latest/installing.html#installing)で，外部ライブラリの構築が難しいので，Christoph Gohlkeさんの[バイナリ](https://www.lfd.uci.edu/~gohlke/pythonlibs/)を使うとよいでしょう。
現在のほとんどのマシンは64ビットなので，特段の理由がない限りWindows installer (64-bit)を選んでください。
Windows上のLinux環境であるWSL2使う人も増えてきました。
WSL2は以下のLinuxを参考にしてください。

## Mac

Macのパッケージ管理システムは[Homebrew](https://brew.sh/index_ja)が人気ですが，[MacPorts](https://www.macports.org)や[Fink](https://www.finkproject.org/)もあります。
著者はかつてFink，現在はMacPortsの地球科学等のパッケージの管理者をしているので，MacPortsをお勧めします。
MacPortsは[variants](https://guide.macports.org/chunked/using.variants.html)という仕組みがあり，既定にはない機能をオンオフしてコンパイルすることができます。
MacPortsのPythonのパッケージは豊富で，Linux等のディストリビューションと比較して新しく，最新であることが多いです。
MacPortsにないとやはり`pip`との二重管理になりますが，MacPortsのパッケージは管理者権限がないとインストールできないので，`pip`に`--user`オプションを付けてインストールすることになります。
どちらでインストールしたかは明確に区別されます。

## Linux, FreeBSD

LinuxディストリビューションやFreeBSDのportsのPythonは古いことが多いです。
LinuxはCondaや本家のバイナリを利用することができます。
Pythonをソースから構築することはあまり難しくありません。

私はFreeBSDで以下のオプションで最適化された最新のPythonをインストールしています。
`--prefix`はインストール先でホームディレクトリの下の`.local`に入れています。
外部ライブラリはpkgやportsを利用しています。

```shell
% ./configure --prefix=${HOME}/.local --enable-optimizations
```