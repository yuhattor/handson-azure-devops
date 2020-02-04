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
今回は ASP.NET で作られた 仮のショッピングサイトのアプリケーションを Azure DevOps でデプロイします。

1. 下準備として、Azure DevOps の Azure Repos にアプリケーションのソースコードをストアします。GitHub のページから ```git clone``` して Azure Repos にプッシュする方法でもいいですが、既存のリポジトリをインポートする方法があります。今回は GitHub に公開されているリポジトリをインポートするところから始めます。
![](./Screenshots/11.png)

1. Azure Repos に下記のリポジトリをインポートします。
https://github.com/yuhattor/DevOpsHandson
![](./Screenshots/12.png)

1. インポートが完了するとインポートされたリポジトリに自動でリダイレクトされます。
![](./Screenshots/13.png)

1. リポジトリが正しくインポートされたことを確認します。
![](./Screenshots/14.png)

1. 次に Azure Pipelines の基本的な CI/CD の設定を確認していきます。Azure Pipelines のメニューより 新しいパイプラインを作成します。
![](./Screenshots/15.png)

1. Azure Pipelines の最初の設定として、パイプラインを動かす際にトリガーとなるリポジトリを選定します。規定の設定だと、これらのリポジトリに何か変更が加えられるとパイプラインが起動するようになります。先ほどアプリケーションのソースコードをインポートした Azure Repos を選択します。
![](./Screenshots/16.png)

1. リポジトリを選択します。
![](./Screenshots/17.png)

1. このリポジトリには Azure Pipelines の定義の雛形が入っています。 Azure Pipelines では一般的な言語・フレームワークのビルドパイプラインのテンプレートを多く用意しています。一から yaml ファイルを書き始めるのではなく、テンプレートを使うと便利です。
また、これらの yaml ファイルの設定には GUI のアシスタントを使うことができます。右上の Show Assistant ボタンでアシスタントを呼び出します。
![](./Screenshots/18.png)

1. 試しに Bash のコマンドをビルドパイプラインのタスクとして追加します。検索ボックスに bash と打ち込み検索をします。
![](./Screenshots/19.png)

1. 単純な echo コマンドを追加します。これらのタスクから ```az``` コマンドを呼び出すことで パイプラインの機能を強化することも可能です。
このハンズオンでは 35 行目に Add でこれらのタスクを追加します。単純に追加してインデントが合わない場合、Azure Pipelines のエディタがエラーを吐くため、 tab キーを押してインデントを追加します。Azure Pipelines のエディタを用いて編集することにより、最低限の構文チェックをすることができます。
![](./Screenshots/20.png)
![](./Screenshots/21.png)

1. 続いて、既存のタスクを GUI エディタで編集します。VSTest@2 の ```Settings``` をクリックし、アシスタントを呼び出します。
Collect advanced diagnostic in case of catastrophic failures のチェックをオンにし、致命的なエラーが起こった場合の診断ログを取得する設定にします。チェックをつけ終わったら Add で更新します。
![](./Screenshots/22.png)

1. もとのタスクが更新されました。これでビルドの設定は終了です。
![](./Screenshots/23.png)

1. Save and run で構築したビルドが動くか確認します。
![](./Screenshots/25.png)

1. Azure Pipelines の定義ファイルは ソースコードリポジトリに保存されるため、この Save とは、リポジトリに commit して、既存の azure-pipelines.yml ファイルを更新することをさします。
![](./Screenshots/26.png)

1. ビルドが走り出します。
![](./Screenshots/27.png)

1. (Optional) ビルドの次に Bash のタスクを定義した結果もこの画面から確認することができます。
![](./Screenshots/32.png)

---
## 5. Azure Pipelines にリリースパイプラインを追加し、基本的な CI/CD を実現する
1. 続いて、リリースパイプラインを構築していきます。
リリースパイプラインは Pipelines 配下の Releases から設定します。New pipeline でパイプラインを新規作成します。
![](./Screenshots/28.png)

1. 今回は、ビルドした成果物を App Service のうえにデプロイするため、Azure App Service deployment の雛形を使います。
![](./Screenshots/29.png)

1. まずは、検証環境の staging という名前のリリースパイプラインを作ります。この Staging には、前の画面で選択した Azure App Service deployment の雛形が適用されており、アプリを App Service にデプロイするための初期設定が完了しています。
1job 1task をクリックして、デプロイ先の設定を開始します。
![](./Screenshots/30.png)

1. Azure DevOps から Azure のサービスにアプリケーションをデプロイする際には Azure DevOps と Azure の環境を紐付ける必要があります。紐付けたいサブスクリプションを選んだら Authorize ボタンより、紐付けを行います。
![](./Screenshots/31.png)

1.  サブスクリプションの連携が完了したら Resource Group と App Service を選択します。これでビルドされたアプリを App Service にデプロイする準備が整いました。
パイプラインの  View に戻り、続きの設定を行います。
![](./Screenshots/33.png)

1. こまで Build パイプライン、Release パイプラインをそれぞれ作成しました。一方でこれらの パイプラインは必要に応じて複数作ることができるため、これらの2つのパイプラインは n:n の関係を持つ可能性があります。 そのため、どの Build パイプライン と Release パイプラインが繋がるべきなのか Azure Pipelines は知らないため、関連付けの設定をする必要があります。
ここでは、Pipeline View より、Build が完了した際のバイナリファイルやzipファイルを取得する設定をします。Add an artifact より前段階で設定した Build Pipelines の成果物を追加します。
![](./Screenshots/34.png)

1. Build を選択し、先ほど設定した Build Pipeline がソースになっているか確認します。このハンズオンようにプロジェクトを作成している場合、初期設定から変える必要はありません。
![](./Screenshots/35.png)

1. 追加したら続いて、トリガーの設定に移ります。この段階では Build パイプラインと Release パイプライン が紐づいただけですが、次は Azure Pipelines 側に "いつ" このリリースパイプラインを起動させるか知らせる必要があります。
Continuous deployment trigger を enabled にし、ビルドが終わり、成果物ができた瞬間に Release パイプラインを起動するようにします。
![](./Screenshots/36.png)

1. 設定したら Save で保存します。
![](./Screenshots/37.png)

1. パイプラインの変更を保存します。
![](./Screenshots/38.png)

1. ここまでの設定で、Repository の master ブランチに何か変更を加えた際に Build パイプラインが動き出し、それが終了したら Release パイプラインが起動する設定になりましたが。
まずは Release パイプラインが正しく動くか確認するため、手動で新規アプリケーションを App Service にデプロイします。Create release は特定のアプリケーションの Build ID に紐づく成果物(バイナリ) を指定して、Release パイプラインを動かし、リリースするための方法です。
![](./Screenshots/39.png)

1. 先ほど Build は終了しているはずなので、該当する Version がリリースされることを確かめ、Release パイプラインを起動します。
![](./Screenshots/40.png)

1. リリースが開始されたら、リアルタイムでステータス確認が可能です。
![](./Screenshots/41.png)
![](./Screenshots/42.png)

1. リリースが成功したら、Web App のページにアクセスし、サンプルアプリケーションがデプロイされていることを確認します。
![](./Screenshots/43.png)
![](./Screenshots/44.png)



---
## 6. Azure Pipelines のリリースパイプラインに Staging 環境へのデプロイプロセスを追加

1. これまでのプロセスで一番基本的な CI/CD のパイプラインが作成されました。次はそれをもう少し高度なものにしていきます。
この章では 該当アプリケーションがまず Staging 環境にデプロイされ、内部ユーザーが挙動を確認したのち、承認プロセスを経てプロダクション環境にデプロイされるような設定をします。
まずは Edit より Release パイプラインの設定を再度開始します。
![](./Screenshots/47.png)

1. これまで設定してきた Release パイプラインが表示されたら、Staging にデプロイするための設定を複製します。Clone ボタンを使うことで、既存の設定を流用して楽に新しい環境へのデプロイ設定が定義的ます。
![](./Screenshots/48.png)

1. 複製されたら、ステージの名前も変更します。staging -> prod の順番でデプロイされる設定にするため、複製したステージの名前は "prod" にします。
![](./Screenshots/49.png)

1. この段階では、Azure Pipelines 側には staging と prod の設定が定義されましたが、一方でまだ Azure 側には １つの環境しかありません。デプロイ先の App Service にも staging と prod が必要ですので、Azure 側でも新しい環境を作ります。
App Service で新しい環境を作るのはとても簡単です。スロット を追加することで全く同じ設定の複製環境を作ることができます。
App Service のメニューから スロットを追加します。
![](./Screenshots/52.png)

1. 新しく staging スロットを作ります。2個目をつくることで、この App Service は staging と prod の区別をつけてアプリケーションをデプロイすることができるようになります。
スロット作成の際に、アプリケーションの設定を複製するようにします。この設定には Web.config や 環境変数が定義されています。
![](./Screenshots/53.png)

1. スロットの作成に成功したら、staging スロットの Azure Portal の設定をみてみます。
![](./Screenshots/54.png)
![](./Screenshots/56.png)

1. staging / prod の環境はほぼ一緒なので一見区別がつきにくいですがg、大きな違いは URL です。staging と名付けたスロットの URL には、 -staging の名前空間が postfix として追加されます。
![](./Screenshots/57.png)

1. この URL にアクセスすると 空のアプリケーションが表示されます。
![](./Screenshots/58.png)

1. これで Azure 側の環境は整いました。Azure DevOps の設定に戻り、staging の環境にまずアプリがデプロイされ、その後の承認を経て prod の環境にアプリがデプロイされる設定の続きをします。
![](./Screenshots/50.png)

1. staging ステージのパイプラインの設定を開き、 Deploy Azure App Service のタスクの Deploy to Slot のチェックをオンにし、続いて対象スロットも staging に設定します。値が更新されない場合は右の更新ボタンから値を更新します。
![](./Screenshots/51.png)
![](./Screenshots/60.png)

1. 設定が終了したら Pipelines の View に戻ります。この段階で、Release パイプラインの staging ステージからは App Service の staging スロットにデプロイされ、Release パイプラインの prod ステージからは App Service の prod (何にも設定していない規定のスロット) にデプロイされるようになっています。
![](./Screenshots/61.png)

1. この段階では、まだ承認プロセスの設定をしていないので、staging にデプロイが完了した直後に prod へのデプロイも開始してしまう設定になっています。
Pre-deployment 承認者の設定により、prod のデプロイプロセスが承認なしでは起動しないようにします。
Pre-deployment approval のトグルをオンにし、 Approvers にユーザーを追加します。このハンズオンでは Approver は自分に設定します。
![](./Screenshots/62.png)

1. 設定が完了したら Save します。
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