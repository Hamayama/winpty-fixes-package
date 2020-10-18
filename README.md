# winpty-fixes-package


## 概要
- winpty-fixes ( https://github.com/Hamayama/winpty-fixes ) の  
  MSYS2 用のパッケージファイルを配布するリポジトリです。

- PKGBUILD ファイルは、以下のものをベースに変更しました。  
  https://github.com/msys2/MSYS2-packages/blob/41e554277125055d2f99e2ef580da5dbe51304f0/winpty/PKGBUILD


## インストール方法
- MSYS2/MinGW-w64 (64bit) 環境での、本パッケージのインストール手順を、  
  以下に示します。

1. MSYS2/MinGW-w64 (64bit) のインストール  
   事前に MSYS2/MinGW-w64 (64bit) がインストールされている必要があります。  
   以下のページを参考に、開発環境のインストールを実施ください。  
   https://gist.github.com/Hamayama/eb4b4824ada3ac71beee0c9bb5fa546d  
   (すでにインストール済みであれば本手順は不要です)

2. パッケージファイルのダウンロード  
   以下のリリースページから、パッケージファイルをダウンロードして、  
   適当な作業用フォルダに置いてください。  
   (作業用フォルダのパスには、空白を入れないようにしてください)  
   
   https://github.com/Hamayama/winpty-fixes-package/releases

3. パッケージファイルのインストール  
   ダウンロードしたパッケージファイルを、開発環境にインストールします。  
   
   プログラムメニューから MSYS2 の MinGW 64bit Shell を起動して、以下のコマンドを実行してください。  
   ( c:\work にパッケージファイルを置いた場合)
   ```
   cd /c/work
   pacman -U winpty-fixes-0.4.4-2-x86_64.pkg.tar.xz
   ```

- 以上です。


## 保守用メモ
1. 事前に、ビルドに必要なパッケージをインストールする
   ```
   pacman -S git mingw-w64-cross-gcc mingw-w64-cross-crt-git
   ```
   (すでにインストール済みであれば本手順は不要)

2. PKGBUILD ファイル内の pkgrel の値と、  
   このドキュメント (README.md) 内のパッケージのリビジョンと履歴を更新する

3. プログラムメニューから MSYS2 の MinGW 64bit Shell を起動して、  
   以下のコマンドを実行すると、パッケージファイルが生成される
   ```
   cd /c/work/winpty-fixes-package
   makepkg
   ```

4. GitHub の Release ページでリリースを作成して、  
   生成したパッケージファイルをアップロードする。


## 環境等
- OS
  - Windows 10 (version 1909) (64bit)
  - Windows 8.1 (64bit)
- 環境
  - MSYS2/MinGW-w64 (64bit) (gcc version 10.2.0 (Rev1, Built by MSYS2 project)) (Windows 10)
  - MSYS2/MinGW-w64 (64bit) (gcc version 9.2.0 (Rev2, Built by MSYS2 project)) (Windows 8.1)

## 履歴
- 2020-10-17 v0.4.4-dev-fix0002 のパッケージファイルを作成


(2020-10-18)
