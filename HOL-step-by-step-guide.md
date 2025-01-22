### 参考情報
- [名前付け規則を定義する](https://learn.microsoft.com/ja-jp/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming)
- [Azure リソースの種類に推奨される省略形](https://learn.microsoft.com/ja-jp/azure/cloud-adoption-framework/ready/azure-best-practices/resource-abbreviations)

<br />

### Contents

- [Exercise 1: リソースグループ、仮想ネットワーク作成](#exercise-1-リソースグループ、仮想ネットワーク作成)

- [Exercise 2: 仮想マシンの展開と構成](#exercise-2-仮想マシンの展開と構成)

- [Exercise 3: Bastion を使用した仮想マシンへの接続](#exercise-3-bastion-を使用した仮想マシンへの接続)

- [Exercise 4: 仮想マシンのバックアップ](#exercise-4-仮想マシンのバックアップ)

- [Exercise 4: 仮想マシンのリストア](#exercise-4-仮想マシンのリストア)

## Exercise 1: リソースグループ、仮想ネットワーク作成

<img src="images/mcw-exercise-2.png" />

### Task 1: リソースグループ作成

- Azureポータル上部の検索窓から **「リソースグループ」** を検索

  <img src="images/ex01-0001.png" />

- **リソースグループ** の **作成** をクリック

  <img src="images/ex01-0002.png" />

- リソースグループの作成
    - 基本
        - サブスクリプション：（ハンズオン用に用意されるもの）
        - リソースグループ：（任意名）
        - リージョン：`japan east`

          <img src="images/ex01-0003.png" />
    - タグ
    
      特に指定はせず次へ
    
    - 確認及び作成

      内容を確認して作成


### Task 2: 仮想ネットワーク作成

- Azure ポータル上部の検索窓で **「仮想ネットワーク」** を検索して選択
  
  <img src="images/ex01-0004.png" />

- 「作成」を選択
  
  <img src="images/ex01-0005.png" />


- 仮想ネットワークを作成
    - 「基本ページ」で以下を設定して次へ
        - サブスクリプション：（ハンズオンで利用予定のもの）
        - リソースグループ：（作成済みのもの）
        - 名前：（任意、仮想ネットワークの名前）
        - 地域：`Japan East`

            <img src="images/ex01-0006.png" />
    
    - 「IPアドレス」ページで以下を設定して次へ
        - IPv4アドレス空間：（任意。プライベートIPアドレス空間推奨）
        - サブネット：（任意。仮想マシン用のサブネットを定義）
          
          <img src="images/ex01-0007.png" />

    - セキュリティ
        
        特に指定なし
    
    - タグ

        特に指定なし

    - 確認および作成

        内容を確認して「作成」



## Exercise 2: 仮想マシンの展開と構成

<img src="images/mcw-exercise-2.png" />

### Task 1: 仮想マシンの展開

- **リソースの作成** をクリック

  <img src="images/ex1-addresource.png" />

- **仮想マシン** の **作成** をクリック

- 仮想マシンの作成

  - **基本**

    - **プロジェクトの詳細**

      - **サブスクリプション**: ワークショップで使用中のサブスクリプション

      ‐ **リソース グループ**: ワークショップで使用中のリソース グループ

    - **インスタンスの詳細**

      - **仮想マシン名**: 任意

      - **地域**: 仮想ネットワークを展開した地域を選択

      - **可用性オプション**: インフラストラクチャ冗長は必要ありません

      - **セキュリティの種類**: Standard

      - **イメージ**: Windows Server 2022 Datacenter - x64 Gen2

      - **VM アーキテクチャ**: x64

      - **サイズ**: 任意（2 vcpu 数のサイズを選択）

    - **管理者アカウント**

      - **ユーザー名**: 任意

      - **パスワード**: 英大文字・小文字、数字、特殊文字の 3 つを含む 1 ～ 20 文字

    - **受信ポートの規則**

      - **パブリック受信ポート**: なし

      <img src="images/ex01-0008.png"/>

<br />

  - **ディスク** 

    - **OS ディスク**

      - **OS ディスクの種類**: Standard SSD

      - **VM と共に削除**: オン

      <img src="images/ex01-0009.png" />

<br />

  - **ネットワーク**

    - **ネットワーク インターフェイス**

      - **仮想ネットワーク**: 作成した仮想ネットワークを選択

      - **サブネット**: 仮想ネットワーク内のサブネットを選択

      - **パブリック IP**: なし

      - **NIC ネットワーク セキュリティ グループ**: なし

      - **VM が削除されたときに NIC を削除する**: オン
    
    - **負荷分散**

      - **負荷分散のオプション**: なし

      <img src="images/ex01-0010.png" />

<br />

  - **管理**

    既定の設定のまま

    <img src="images/ex01-0011.png" />

<br />

  - **監視**

    既定の設定のまま

    <img src="images/ex01-0012.png" />

<br />

  - **詳細**

    既定の設定のまま

    <img src="images/ex01-0013.png" />

- **確認および作成** をクリック、指定した内容を確認し **作成** をクリック

  <img src="images/ex01-0014.png" />

<br />

### Task 2: 静的 IP アドレスの割り当て

- 作成した仮想マシンの管理ブレードへ移動し、**ネットワーク/ネットワーク設定** を選択

- ネットワーク インターフェイスをクリック

  <img src="images/ex01-0015.png" />
  
- **IP 構成** を選択し **ipconfig1** をクリック

  <img src="images/ex01-0016.png" />

- **IP 構成の編集** の **プライベート IP アドレスの設定** ‐ **割り当て** で **静的** を選択

  任意のプライベート IP アドレスを指定（現在割り当て中のものでも OK）

  <img src="images/ex01-0017.png" />

- **保存** をクリックし、プライベート IP アドレスの割り当てが静的に変更されたことを確認

  <img src="images/ex01-0018.png" />

<br />

### Task 3: ディスクの追加

- 仮想マシンの管理ブレードで **ディスク** を選択、**＋ 新しいディスクを作成し接続する** をクリック

  <img src="images/ex01-0019.png" />

- ディスク名を入力し、種類とサイズを指定

  <img src="images/ex01-0020.png" />

  ※ 新しいディスクの初期化は、後の手順で仮想マシンに接続して設定

<br />

### Task 4:仮想マシン サイズの変更

- 仮想マシンの管理ブレードで **サイズ** を選択

- 利用可能なサイズの一覧から新しいサイズを選択し **サイズの変更** をクリック

  <img src="images/ex01-0021.png" />

  ※ 仮想マシンが実行中の場合、サイズを変更した際は再起動を実施

<br />

## Exercise 2: Bastion を使用した仮想マシンへの接続

### Task 1:Bastion 作成
1. Azure ポータルで最初に作成した仮想マシンの画面を開く

1. 「Bastion」ページから Bastion 作成

![](images/ex04-0006.png)

### Task 2:Bastion 経由で接続（Azure ポータル）

1. Azure ポータルで最初に作成した仮想マシンの画面を開く

1. 「概要」ページにある [接続]-[Bastion] を選択

    ![](images/ex04-0009.png)

1. ユーザー名、パスワードを入力して「接続」

    (*) クリップボードへの接続許可アラートが出てくるので「許可」にする

    ![](images/ex04-0010.png)

1. 新しくブラウザが立ち上がって接続できればOK


## Exercise 3: 仮想マシンのバックアップ

<img src="images/mcw-exercise-6.png" />

### Task 1: Recovery Services コンテナの作成と構成

- Azure ポータルのトップ画面の検索バーに **バックアップ センター** と入力し、表示される候補の **バックアップ センター** を選択

  <img src="images/recovery-services-vault-01.png" />

- **＋ コンテナー** をクリック

  <img src="images/recovery-services-vault-02.png" />

- コンテナーの種類で **Recovery Services vault** を選択し、**続行** をクリック

  <img src="images/recovery-services-vault-03.png" />

- Recovery Services コンテナーの作成

  - **基本**

    - **プロジェクトの詳細**

      - **サブスクリプション**: ワークショップで使用中のサブスクリプション

      - **リソース グループ: ワークショップで使用中のリソース グループ

    - **インスタンスの詳細**

      - **資格情報コンテナー名**: 任意

      - **リージョン**: 仮想マシンを展開したリージョン1

        <img src="images/recovery-services-vault-04.png" />

        <br />

  - **コンテナーのプロパティ**

    - **不変性を有効にする**: オン

      <img src="images/recovery-services-vault-05.png" />

      <br />

  - **ネットワーク**

    - **接続方法**: すべてのネットワークからのパブリック アクセスを許可する

      <img src="images/recovery-services-vault-06.png" />

      <br />

- **確認および作成** をクリック、指定した内容を確認し **作成** をクリック

  <img src="images/recovery-services-vault-07.png" />

  <br />

- 展開完了後、作成した Recovery Services コンテナーの管理ブレードへ移動

- **プロパティ** を選択、**バックアップ構成** の **更新** をクリック

  <img src="images/recovery-services-vault-08.png" />

- リージョンをまたがる復元で **有効にする** を選択し **保存** をクリック

  <img src="images/recovery-services-vault-09.png" />

<br />

### Task 2: バックアップ ポリシーの作成

- バックアップ センターへ移動、**＋ ポリシー** をクリック

  <img src="images/backup-center-summary.png" />

- **データソースの種類** で **Azure 仮想マシン** を選択し、**コンテナーの選択** をクリック

  <img src="images/backup-policy-01.png" />

- 作成した Recovery Services コンテナーを選択し **選択** をクリック

  <img src="images/backup-policy-02.png" />

- **続行** をクリック

  <img src="images/backup-policy-03.png" />

- ポリシーの作成

  - **ポリシーのサブタイプ**: Standard

  - **Standard 保護**

    - **ポリシー名**: 任意

  - **バックアップ スケジュール**

    - **頻度**: 毎日

    - **時間**: 0:00

    - **タイムゾーン**: (UTC+9:00) 大阪、札幌、東京

  - **インスタント復元**

    - **インスタント回復スナップショットの保有期間**: 1 日

  - **保持期間の範囲**

    - **毎日のバックアップ ポイントの保有期間**: 7 日

    - **毎週のバックアップ ポイントの保有期間**: オン（日曜日、4 週）

    - **毎月のバックアップ ポイントの保有期間**: オン（週ベース、最終日曜日、6 月）

      <img src="images/backup-policy-04.png" />

      <br />

- **作成** をクリックし、ポリシーを作成

<br />

### Task 3: バックアップの構成

- バックアップ センターへ移動、**＋ バックアップ** をクリック

  <img src="images/backup-center-summary.png" />

- バックアップ対象、Recovery Services コンテナーを選択し **続行** をクリック

  - **データソースの種類**: Azure 仮想マシン
  
  - **コンテナーの種類**: Recovery Services vault

  - **コンテナー**: 作成した Recovery Services コンテナーを選択

    <img src="images/backup-configuration-01.png" />

    <br />

- バックアップの構成

  - **ポリシーのサブタイプ**: Standard

  - **バックアップ ポリシー**: 作成したバックアップ ポリシーを選択

  - **仮想マシン**: 追加をクリックし、展開済みの仮想マシンを選択

    <img src="images/backup-configuration-02.png" />

    <br />

- 仮想マシンの管理ブレードから、**バックアップ** を開き、**バックアップの有効化** をクリック（バックアップの保持期限はデフォルトの値のままでOK）

  ※ バックアップが有効化されている仮想マシンではオンデマンドでバックアップも可

    <img src="images/backup-recovery-01.png" />

<br />

## Exercise 4: 仮想マシンのリストア
