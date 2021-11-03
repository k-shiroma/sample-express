# sample-express
Node.js + express のプロジェクト作成手順を記載するプロジェクトです

## 参考URL
- nodenv インストール
    - [mintsu's blog - Linux(Ubuntu)にnodenvを導入する方法](https://blog.mintsu-dev.com/posts/2020-07-22-install-nodenv-linux/#nodenv-install)
    - [Qiita - @282Haniwa - nodenvの環境構築](https://qiita.com/282Haniwa/items/a764cf7ef03939e4cbb1)

## 開発環境
| 名前 | バージョン |
|-|:-:|
| VirtualBox | 6.1 |
| ubuntu | 20.04.3 server |
| Visual Studio Code | 1.61.0 |
| nodenv | 1.4.0+3.631d0b6 |
| Node.js | 17.0.1 |
| express | 4.17.1 |

## 環境構築
```sh
# 1. nodenv
## apt アップデート
### install の前にはやっておいたほうがいい
### ubuntu20.04.3 だと build-essential インストール時にエラーになる
sudo apt update

## 開発ツールインストール (nodenv ビルド時に使用)
sudo apt install build-essential

## nodenv ダウンロード
git clone https://github.com/nodenv/nodenv.git ~/.nodenv

## nodenv ビルド
cd ~/.nodenv && src/configure && make -C src

## PATHを通す
echo 'export PATH="$HOME/.nodenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(nodenv init -)"' >> ~/.bashrc

## シェル再起動
exec $SHELL -l

## Node.js インストール用プラグイン インストール
git clone https://github.com/nodenv/node-build.git $(nodenv root)/plugins/node-build

## インストール確認
curl -fsSL https://github.com/nodenv/nodenv-installer/raw/master/bin/nodenv-doctor | bash

## こうなっていたらOK
## Checking for `nodenv' in PATH: /home/ubuntu/.nodenv/bin/nodenv
## Checking for nodenv shims in PATH: OK
## Checking `nodenv install' support: /home/ubuntu/.nodenv/plugins/node-build/bin/nodenv-install (node-build 4.9.57)
## Counting installed Node versions: none
##   There aren't any Node versions installed under `/home/ubuntu/.nodenv/versions'.
##   You can install Node versions like so: nodenv install 2.2.4
## Auditing installed plugins: OK

# 2. Node.js
## インストール可能なバージョンのリスト確認
nodenv install -l

## インストール(最新)
nodenv install 17.0.1

## システム全体で使用する Node.js 設定
nodenv global 17.0.1

## 確認
node -v
nodenv versions
```

## 開発手順
本プロジェクトの作成手順です。  
本プロジェクトを動作させたい場合、下記 [実行手順](#実行手順) を行ってください

### 環境構築
```sh
# 3. プロジェクト設定
## プロジェクトルート作成
mkdir ~/sample-express
cd ~/sample-express

## プロジェクトで使用する Node.js 設定
nodenv local 17.0.1

## Node.js バージョン確認
node -v
nodenv versions

## package.json 生成
npm init -y

## express インストール
npm install express
```

### 開発
1. index.js 作成
    ```js
    const express = require('express')
    const app = express()

    app.get('/', (req, res) => {
        res.send('Hello World!')
    })

    app.listen(8080, () => console.log('listening on http://localhost:8080'))
    ```
1. 実行
    1. 起動
        ```sh
        node index.js
        ```
    1. http://localhost:8080 をブラウザで開く

## 実行手順
本プロジェクトを実行する場合、[環境構築](#環境構築) を行った後に下記を実行してください

```sh
# 1. ソース取得
git clone https://github.com/k-shiroma/sample-express.git

# 2. ライブラリ取得
cd sample-express
npm install

# 3. 実行
node index.js
```