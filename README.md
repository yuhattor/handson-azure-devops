# Microsoft Azure DevOps Handson
Updated: 2020/02/04

---
このハンズオンでは、Azure DevOps と Azure Web App を使い、Microsoft が提供している DevOps プロセスを一貫して体験いただきます。

## 目次

1. 準備
2. Azure Web App を Azure にプロビジョ二ング
3. Azure DevOps のプロジェクトを作成
4. Azure Pipelines にビルドパイプラインを作成
5. Azure Pipelines にリリースパイプラインを追加し、基本的な CI/CD を実現する
6. Azure Pipelines のリリースパイプラインに Staging 環境へのデプロイプロセスを追加
7. Azure Repository からコードを変更し、コミットをトリガーに CI/CD が走り出すことを確認
8. Azure Web App の機能で遊ぶ


## 概要
# TBD

---

## 1. 準備

#### 用意するもの
- Azure Subscription

#### ハンズオンで使用するページ
- 当ハンズオン資料
https://github.com/yuhattor/DevOpsHandson
- Azure Portal
https://portal.azure.com
- Azure DevOps
https://dev.azure.com/

---

## 2. Azure Web App を Azure にプロビジョ二ング

### 手順

1. Azure Portal (https://portal.azure.com) にアクセスします。
![](./Screenshots/1-1.png)

1. ホームページに App Service があるので、作成していきます。
![](./Screenshots/1-3.png)

1. 追加/Add ボタンから 新しい App Service を追加します。
![](./Screenshots/1-4.png)

1. リソースグループを追加します。リソースグループの名前は任意の名前で良いですが、同一サブスクリプションの中でかぶらないようにします。当ハンズオン では、例として XX の値を置いておりますが、XX はご自身の ID や ニックネームなどで置き換えてください。
![](./Screenshots/1-5.png)

1. Web App の名前を定義します。また、デプロイモデルは コード/Code を選びます。Web App における最も簡単なデプロイ方法の一つで、.NET や Java など、様々な言語・フレームワークのアプリケーションをそのまま配置することができます。今回のハンズオンでは OS は Windows を選びましょう。
![](./Screenshots/1-6.png)

1. App Service Plan を作成します。この App Service Plan とは、 Web App など、App Service にデプロイされるインスタンスの課金単位になります。
![](./Screenshots/1-7.png)
1. App Service Plan の値を入力したら、モニタリングの設定に移ります。
![](./Screenshots/1-8.png)
1. Application Insights をデプロイするための設定に移ります。
Application Insights とは開発者や DevOps プロフェッショナル向けの拡張可能なアプリケーション パフォーマンス管理 (APM) サービスです。
初期設定で 値が入っていますが、任意の名前と場所を決定したら OK で確定します。入力する値は以上ですので、この後は入力内容の確認に移ります。
![](./Screenshots/1-11.png)
1. 表示された内容で間違いがない場合、Web App をデプロイします。
![](./Screenshots/1-12.png)
1. 数十秒待つと Web App がデプロイされますので、デプロイされたリリースを確認しにいきます。
![](./Screenshots/1-14.png)
1. Web App の画面に到達したらホーム画面にある URL をクリックして、デプロイされたものを確認します。
![](./Screenshots/1-15.png)
1. Web App の初期画面 が表示されたことを確認します。
![](./Screenshots/1-16.png)

### この章で作ったもの
# TBD

### 備考/参考URL
- App Service / Web App とは？
  https://azure.microsoft.com/ja-jp/services/app-service/web/

- Resource Group とは
  https://tech-blog.cloud-config.jp/2019-06-06-evening-azure-challenge-002/

- App Service と App Service Plan の違いって？
  https://www.cloudou.net/app-service/app001/

- Application Insights とは？
  https://docs.microsoft.com/ja-jp/azure/azure-monitor/app/app-insights-overview


---

## 3. Azure DevOps のプロジェクトを作成

1. Azure DevOps のページにログインします (https://dev.azure.com)
![](./Screenshots/1.png)
1. 初回ログインの際には名前を入力する必要があります。
![](./Screenshots/2.png)
1. Continue で初回登録を完了します。すると、初期 Organization が設定されます。
![](./Screenshots/3.png)
1. プロジェクトを作成する画面に映りますので、最初のプロジェクトを作成しましょう。プロジェクト名は任意です。
プロジェクトは Private か Public を選ぶことができます。
![](./Screenshots/4.png)
1. プロジェクトができたらクリックしてプロジェクトページにアクセスします。
![](./Screenshots/9.png)
![](./Screenshots/10.png)

**既存の組織がある場合**
1. もし既存の組織がある、また以前に Azure DevOps を使っていた場合は、ログイン後そのまま該当の組織において新しいプロジェクトを作ります。
また、新しく組織を作る場合は New Organization から新しい組織を作ります。
![](./Screenshots/5.png)
1. Continue で先に進み必要事項を記入します。
![](./Screenshots/7.png)
1. 組織名を入力する必要がありますが、この値はユニーク値にする必要があります。
![](./Screenshots/8.png)



---
## 4. Azure Pipelines にビルドパイプラインを作成
![](./Screenshots/11.png)
![](./Screenshots/12.png)
![](./Screenshots/13.png)
![](./Screenshots/14.png)
![](./Screenshots/15.png)
![](./Screenshots/16.png)
![](./Screenshots/17.png)
![](./Screenshots/18.png)
![](./Screenshots/19.png)
![](./Screenshots/20.png)
![](./Screenshots/21.png)
![](./Screenshots/22.png)
![](./Screenshots/23.png)
![](./Screenshots/24.png)
![](./Screenshots/25.png)
![](./Screenshots/26.png)

---
## 5. Azure Pipelines にリリースパイプラインを追加し、基本的な CI/CD を実現する

![](./Screenshots/27.png)
![](./Screenshots/28.png)
![](./Screenshots/29.png)
![](./Screenshots/30.png)
![](./Screenshots/31.png)
![](./Screenshots/32.png)
![](./Screenshots/33.png)
![](./Screenshots/34.png)
![](./Screenshots/35.png)
![](./Screenshots/36.png)
![](./Screenshots/37.png)
![](./Screenshots/38.png)
![](./Screenshots/39.png)
![](./Screenshots/40.png)
![](./Screenshots/41.png)
![](./Screenshots/42.png)
![](./Screenshots/43.png)
![](./Screenshots/44.png)
![](./Screenshots/45.png)


---
## 6. Azure Pipelines のリリースパイプラインに Staging 環境へのデプロイプロセスを追加

![](./Screenshots/46.png)
![](./Screenshots/47.png)
![](./Screenshots/48.png)
![](./Screenshots/49.png)
![](./Screenshots/50.png)
![](./Screenshots/51.png)
![](./Screenshots/52.png)
![](./Screenshots/53.png)
![](./Screenshots/54.png)
![](./Screenshots/55.png)
![](./Screenshots/56.png)
![](./Screenshots/57.png)
![](./Screenshots/58.png)
![](./Screenshots/59.png)
![](./Screenshots/60.png)
![](./Screenshots/61.png)
![](./Screenshots/62.png)
![](./Screenshots/63.png)


---
## 7. Azure Repository からコードを変更し、コミットをトリガーに CI/CD が走り出すことを確認
![](./Screenshots/64.png)
![](./Screenshots/65.png)
![](./Screenshots/66.png)
![](./Screenshots/67.png)
![](./Screenshots/68.png)
![](./Screenshots/69.png)
![](./Screenshots/70.png)
![](./Screenshots/71.png)
![](./Screenshots/72.png)

---
## 8. Azure Web App の機能で遊ぶ

![](./Screenshots/73.png)
![](./Screenshots/74.png)
![](./Screenshots/75.png)
![](./Screenshots/76.png)
![](./Screenshots/77.png)
![](./Screenshots/78.png)
![](./Screenshots/79.png)