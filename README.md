k-metrics docker container images
================

`rocker` based docker container images for Machine Learning with R.

　

# About this repository

　本リポジトリは [データ分析勉強会](https://sites.google.com/site/kantometrics/2019)
でテキストとして利用している
[『Rによる機械学習』](https://www.shoeisha.co.jp/book/detail/9784798145112)
のサンプルコードを動かせる日本語ロケールのコンテナイメージを作成し公開しています。すべてのコンテナイメージは
[rocker](https://hub.docker.com/u/rocker) をベースとして使用しています。

　なお、公開しているコンテナイメージを使用することによって生じる、いかなる直接的・間接的損害について著作者ならびに勉強会運営者はいかなる責任・サポート義務を負いません。

　

# Container images

　以下のコンテナイメージを公開しています。

| Image      | Base image        |     R3.6.x      |     R4.0.x     | Descriptions                                                                                       |
| ---------- | ----------------- | :-------------: | :------------: | -------------------------------------------------------------------------------------------------- |
| jverse     | rocker/verse      |       Yes       |      Yes       | Localizing into Japanese (Add Japanese fonts and locale)                                           |
| mlwr       | jverse            |       Yes       |      Yes       | Add R packages for [Machine Learning with R](https://www.shoeisha.co.jp/book/detail/9784798145112) |
| tidymodels | mlwr              | Yes<sup>1</sup> |      Yes       | Add `tidymodels` package                                                                           |
| blogdown   | tidymodels        |       Yes       | No<sup>2</sup> | Add `blogdown` package and Hugo executable                                                         |
| keras      | rocker/tensorflow | No<sup>3</sup>  | No<sup>3</sup> | Discontinued                                                                                       |

<sup>1</sup> Build manually  
<sup>2</sup> rocker/verse:4.0.x includes `blogdown` package and Hugo
executable  
<sup>3</sup> rocker/tensorflow no longer update

　

# Usage

　Dockerの導入に関しては省略しますが、使い方は`rocker/*`と同じく **必ずパスワードを指定** してください。

``` bash
sudo docker run -p 8787:8787 -v リンクするローカルパス:/home/rstudio/project \
  -e PASSWORD=パスワード --name コンテナ名 kmetrics/イメージ名:タグ
```

| 設定項目        | 設定例        | 説明                             |
| ----------- | ---------- | ------------------------------ |
| リンクするローカルパス | \~/R       | 任意のローカルパス<sup>4</sup>          |
| パスワード       | password   | 任意のパスワード                       |
| コンテナ名       | tidymodels | 任意のコンテナ名称（`--name`オプションは省略可です） |
| イメージ名       | tidymodels | 実行させたいイメージ名                    |
| タグ          | 3.6.1      | 省略時は`latest`を指定したものと解釈されます     |

<sup>4</sup>
Windowsの場合`/DriveLetter/Directory/...`としてください。`DriveLetter:`というドライブ名は使えません。

　

## ホームディレクトリ

　Dockerのユーザ名は`rocker/*`と同じく`rstudio`ですのでホームディレクトリは`/home/rstudio`になります。ホームディレクトリ配下には以下のサブディレクトリが配置されています。

| サブディレクトリ名 | 用途など                                           |
| --------- | ---------------------------------------------- |
| kitematic | コンテナ管理用ディレクトリ（R3.6.x(RStudio Server 1.2) Only） |
| project   | プロジェクト用ディレクトリ（ローカルパスのリンクポイント）                  |
| sample    | サンプルファイル<sup>5</sup>（スクリプト、データなど）格納ディレクトリ      |

<sup>5</sup> 順次提供予定

　

## 設定ファイル（4.0.x and latest tag Only）

　RStudioの設定はデフォルトから変更してあります。設定ファイル`rstudio-prefs.json`は、好みに応じて変更しイメージをビルドしてください。なお、設定項目の詳細については[こちら](https://docs.rstudio.com/ide/server-pro/1.3.820-1/session-user-settings.html#session-user-settings)を参照してください。

　

# License

  - Dockerfiles are licensed under the GPL 2 or later.  
  - Other documents are licensed under “CC BY-NC-SA 4.0, Sampo Suzuki”
