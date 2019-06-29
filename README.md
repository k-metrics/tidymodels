k-metrics docker container images
================

`rocker/verse` based docker images for Machine Learning with
R.

## About

本リポジトリは[rocker/verse](https://hub.docker.com/r/rocker/verse)をベースに日本語環境で[データ分析勉強会](https://sites.google.com/site/kantometrics/2019)におけるテキストである[『Rによる機械学習』](https://www.shoeisha.co.jp/book/detail/9784798145112)のサンプルコードが動かせるコンテナイメージを作成し公開しています。  
　  
なお、公開しているコンテナイメージを使用することによって生じる、いかなる直接的・間接的損害について著作者ならびに勉強会運営者はいかなる責任・サポート義務は負いません。

## About container images

公開しているコンテナイメージは以下の通りです。

| image      | base         | descriptions                               | build     |
| ---------- | ------------ | ------------------------------------------ | --------- |
| jverse     | rocker/verse | Japanized base image                       | automated |
| mlwr       | jverse       | Add R packages for Machine Learnign with R | automated |
| tidymodels | mlwr         | Add tidymodels and tidytext package        | local     |

### kmetrics/jverse

[rocker/verse](https://hub.docker.com/r/rocker/verse)をベースに以下を追加しています。

1.  日本語ロケールの追加
2.  日本語フォント（IPA and
Noto）の追加
3.  Rパッケージに必要なOSライブラリ群の追加
4.  Java環境の追加と設定

### kmetrics/mlwr

`kmetrics/jverse`をベースに[『Rによる機械学習』](https://www.shoeisha.co.jp/book/detail/9784798145112)のサンプルコードを動かすのに必要なRパッケージなどを追加しています。

### kmetrics/tidymodels

`kmetrics/mlwr`をベースに`tidymodels`パッケージならびに`tidytext`パッケージを追加していいます。関連パッケージとしてインストールされる`rstan`パッケージがdockerhub環境ではビルドできないため、ローカルビルドしたものをpushしています。

## Licencs

Dockerfiles are licensed under the GPL 2 or later.  
Other documents are licensed under “CC BY-NC-SA 4.0, Sampo Suzuki”