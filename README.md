k-metrics docker container images
================

`rocker` based docker container images for Machine Learning with R.

　

## About this repository

本リポジトリは [データ分析勉強会](https://sites.google.com/site/kantometrics/2019)
でテキストとして利用している
[『Rによる機械学習』](https://www.shoeisha.co.jp/book/detail/9784798145112)
のサンプルコードを動かせる日本語ロケールのコンテナイメージを作成し公開しています。すべてのコンテナイメージは
[rocker](https://hub.docker.com/u/rocker)
をベースとして使用しています。

　

なお、公開しているコンテナイメージを使用することによって生じる、いかなる直接的・間接的損害について著作者ならびに勉強会運営者はいかなる責任・サポート義務を負いません。

　

## Container images

公開しているコンテナイメージは以下の通りです。なお、automated
buildに関しては予告なく停止する場合があります。

| image      | base image                  | descriptions                               | build     |
| ---------- | --------------------------- | ------------------------------------------ | --------- |
| jverse     | rocker/verse:3.6.1          | Japanized base image                       | automated |
| mlwr       | jverse                      | Add R packages for Machine Learnign with R | automated |
| tidymodels | mlwr                        | Add tidymodels related packages            | automated |
| blogdown   | tidymodels                  | Add blogdown package and Hugo executable   | automated |
| keras      | rocker/tensorflow:3.6.1     | Japanized image                            | automated |
| keras-gpu  | rocker/tensorflow-gpu:3.6.0 | keras w/ GPU support                       | automated |
| ml         | rocker/ml:3.6.1             | tensorflow + h2o, greta. Japanized image   | automated |
| ml-gpu     | rocker/ml-gpu:3.6.0         | ml w/ GPU support                          | automated |

　

### jverse

[rocker/verse](https://hub.docker.com/r/rocker/verse) をベースに以下を追加しています。

1.  日本語ロケールの追加
2.  日本語フォント（IPA and Noto）の追加
3.  Rパッケージに必要なOSライブラリ群の追加
4.  Java環境の追加と設定

　

### mlwr

`kmetrics/jverse`をベースに
[『Rによる機械学習』](https://www.shoeisha.co.jp/book/detail/9784798145112)
のサンプルコードを動かすために必要なRパッケージをインストールしています。

　

### tidymodels

`kmetrics/mlwr`をベースに`tidymodeks`関連パッケージをインストールしています。`tidymodels`パッケージは依存関係により関連パッケージとしてインストールされる`rstan`パッケージがDockerHub環境ではビルドできないため不完全な形でのインストールになっています。。

  - `tidymodels` imports `tidyposterior`  
  - `tidyposterior` imports `rstanarm`  
  - `rstanarm` imports
`rstan`

`tidymodels`パッケージを完全な形でインストールしたい場合はローカルビルドしてください。

　

### blogdown

`kmetrics/tidymodels`をベースに`blogdown`パッケージとHugoの実行環境をインストールしています。Hugoテーマはインストールしていませんので別途`blogdown::install_theme`関数を利用してインストールしてください。  
なお、`C50`パッケージにはプロット関連のバグがあるため暫定的にGitHubの開発版をインストールしています。

　

### keras/keras-gpu

ディープラーニング用にKeras/Tensorflowを利用するための [rocker/tensorflow
<i class="fa fa-external-link"></i>](https://hub.docker.com/r/rocker/tensorflow),
[rocker/tensorflow-gpu
<i class="fa fa-external-link"></i>](https://hub.docker.com/r/rocker/tensorflow-gpu)
をベースに`kmetrics/blogdown`と同じパッケージ群をインストールしています。

　

### ml/ml-gpu

GPU環境（nvidia CUDA）を利用するための [rocker/ml
<i class="fa fa-external-link"></i>](https://hub.docker.com/r/rocker/ml),
[rocker/ml-gpu
<i class="fa fa-external-link"></i>](https://hub.docker.com/r/rocker/ml-gpu)
をベースに`kmetrics/blogdown`と同じパッケージ群をインストールしています。別途、nvidiaのランタイムが必要です。

　

## Usage

Dockerの導入に関しては省略しますが、使い方の基本は`rocker/*`と同じく **必ずパスワードを指定** してください。

``` bash
sudo docker run -p 8787:8787 -v リンクさせたいローカルパス:/home/rstudio \
  -e PASSWORD=パスワード --name コンテナ名 kmetrics/イメージ名:タグ
```

| 設定項目          | 設定例          | 説明                                |
| ------------- | ------------ | --------------------------------- |
| リンクさせたいローカルパス | /home/user/R | 任意のローカルパス、Windowsの場合“/C/…”となる点に注意 |
| パスワード         | password     | 任意のパスワード                          |
| コンテナ名         | tidymodels   | 任意のコンテナ名称                         |
| イメージ名         | tidymodels   | 実行させたいイメージ名を指定                    |
| :タグ           | :3.6.1       | 省略時は:latest                       |

　

## License

  - Dockerfiles are licensed under the GPL 2 or later.  
  - Other documents are licensed under “CC BY-NC-SA 4.0, Sampo Suzuki”
