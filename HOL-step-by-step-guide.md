### 参考情報
- [名前付け規則を定義する](https://learn.microsoft.com/ja-jp/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming)
- [Azure リソースの種類に推奨される省略形](https://learn.microsoft.com/ja-jp/azure/cloud-adoption-framework/ready/azure-best-practices/resource-abbreviations)

<br />

### Contents

- [Exercise 1: リソースグループ、仮想ネットワーク作成、ストレージアカウントの作成](#exercise-1-リソースグループ、仮想ネットワーク作成、ストレージアカウントの作成)

- [Exercise 2: 仮想マシンの展開と構成](#exercise-2-仮想マシンの展開と構成)

- [Exercise 3: Bastion を使用した仮想マシンへの接続](#exercise-3-bastion-を使用した仮想マシンへの接続)

- [Exercise 4: 仮想マシンのバックアップ](#exercise-4-仮想マシンのバックアップ)

- [Exercise 5: 仮想マシンのリストア](#exercise-5-仮想マシンのリストア)

- [（Option）: ファイルとフォルダーのバックアップ](#Option-ファイルとフォルダーのバックアップ)

<br />

## Exercise 1: リソースグループ、仮想ネットワーク作成、ストレージアカウントの作成

<img src="images/main-exercise-1.png" />

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

<br />


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
  
  <br />


### Task 3: ストレージアカウントの作成

- Azureポータルで **ストレージアカウント** と検索し、**作成** をクリック

  <img src="images/ex03-0019.png" />

- ストレージアカウントの作成

  - 基本情報

    - サブスクリプション：（ハンズオン用に用意されるもの）

    - リソースグループ：（作成したリソースグループ）

    - ストレージアカウント名：一意の名前

    ※その他デフォルトのまま

      <img src="images/ex03-0020.png" />
  
  <br />



## Exercise 2: 仮想マシンの展開と構成

<img src="images/main-exercise-2.png" />

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


## Exercise 3: Bastion を使用した仮想マシンへの接続

  <img src="images/main-exercise-3.png" />

### Task 1:Bastion 作成
- Azure ポータルで最初に作成した仮想マシンの画面を開く

- 「Bastion」ページから Bastion 作成

  <img src="images/ex02-0001.png" />


### Task 2:Bastion 経由で接続（Azure ポータル）

- Azure ポータルで最初に作成した仮想マシンの画面を開く

- 「概要」ページにある [接続]-[Bastion] を選択

  <img src="images/ex02-0002.png" />


- ユーザー名、パスワードを入力して「接続」

    (*) クリップボードへの接続許可アラートが出てくるので「許可」にする

    <img src="images/ex02-0003.png" />

- 新しくブラウザが立ち上がって接続できればOK
  <img src="images/ex02-0004.png" />

- 画面左の **》** をクリックし、クリップボード アクセス ツール パレットを表示

  ※ ローカル コンピューターからテキストをコピーした場合、クリップボード アクセス ツール パレットに自動表示

- 仮想マシンの画面を全画面表示する際は **Fullscreen** をクリック

  <img src="images/ex02-0005.png" />
  
  ※ 全画面表示を解除する際は **Esc** キーを押下

<br />

- エクスプローラーを起動、C ドライブ直下に新しいフォルダを作成し、フォルダ内に新しいテキスト ファイルを作成

  <img src="images/ex02-0006.png" />

  ※ テキスト ファイル内には現在の時刻など任意の文字列を記述し保存

<br />


## Exercise 4: 仮想マシンのバックアップ

<img src="images/main-exercise-4.png" />


### Task 1: Recovery Services コンテナの作成と構成

- Azure ポータルのトップ画面の検索バーに **ビジネス継続性センター** と入力し、表示される候補の **ビジネス継続性センター** を選択

  <img src="images/ex03-0001.png" />

- [管理] > [コンテナー] を選択し、 **＋ コンテナー** をクリック

  <img src="images/ex03-0002.png" />

- コンテナーの種類で **Recovery Services vault** を選択し、**続行** をクリック

  <img src="images/ex03-0003.png" />

- Recovery Services コンテナーの作成

  - **基本**

    - **プロジェクトの詳細**

      - **サブスクリプション**: ワークショップで使用中のサブスクリプション

      - **リソース グループ**: ワークショップで使用中のリソース グループ

    - **インスタンスの詳細**

      - **資格情報コンテナー名**: 任意

      - **リージョン**: 仮想マシンを展開したリージョン1

        <img src="images/ex03-0004.png" />

        <br />

  - **冗長**

    - **リージョンをまたがる復元**： オン

      <img src="images/ex03-0005.png">

    <br />
  
  - **暗号化**

    - 既定の設定のまま

      <img src="images/ex03-0006.png">

    <br />


  - **コンテナーのプロパティ**

    - **不変性を有効にする**: オン

      <img src="images/ex03-0007.png" />

      <br />

  - **ネットワーク**

    - **接続方法**: すべてのネットワークからのパブリック アクセスを許可する

      <img src="images/ex03-0008.png" />

      <br />

- **確認および作成** をクリック、指定した内容を確認し **作成** をクリック

  <img src="images/ex03-0009.png" />

  <br />

### Task 2: ビジネス継続性センターの作成

- ビジネス継続性センターへ移動、**＋ ポリシー** をクリック

  <img src="images/ex03-0010.png" />

- **データソースの種類** で **Azure 仮想マシン** を選択し、**コンテナーの選択** をクリック

  <img src="images/ex03-0011.png" />

- 作成した Recovery Services コンテナーを選択し **選択** をクリック

  <img src="images/ex03-0012.png" />

- **続行** をクリック

  <img src="images/ex03-0013.png" />

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

      <img src="images/ex03-0014.png" />

      <br />

- **作成** をクリックし、ポリシーを作成

<br />

### Task 3: バックアップの構成

- ビジネス継続性センターへ移動、**＋ バックアップ** をクリック

  <img src="images/ex03-0015.png" />

- ワークロード、バックアップ対象を選択し **バックアップ** をクリック

  - **ワークロード**: Azure
  
  - **データソースの種類**: Azure 仮想マシン

    <img src="images/ex03-0016.png" />

    <br />

- バックアップの構成で、**バックアップの有効化** をクリック

  - **ポリシーのサブタイプ**: Standard

  - **バックアップ ポリシー**: 作成したバックアップ ポリシーを選択

  - **仮想マシン**: 追加をクリックし、展開済みの仮想マシンを選択

    <img src="images/ex03-0017.png" />

    <br />

- 仮想マシンの管理ブレードから、**バックアップ** を開き、**今すぐバックアップ** をクリック（バックアップの保持期限はデフォルトの値のままでOK）

  ※ バックアップが有効化されている仮想マシンではオンデマンドでバックアップも可

    <img src="images/ex03-0018.png" />

<br />

- エクスプローラーを起動、C ドライブ直下に先ほど作成したフォルダ内のテキストファイルに、現在の時刻など任意の文字列を記述し保存

  <img src="images/ex02-0006.png" />

<br />

## Exercise 5: 仮想マシンのリストア

  <img src="images/main-exercise-4.png" />


### Task 1: バックアップの復元

- 仮想マシンの管理ブレードから、 **バックアップ** を開き、 **VMの復元** をクリック

  <img src="images/ex03-0021.png" />

  - 復元ポイントの選択先：先ほど取得した復元ポイントを選択して、**OK** をクリックし、**復元**をクリック

    - 復元の種類：**新しい仮想マシンの作成** を選択

    - 仮想マシン名：（任意名）

    - サブスクリプション：（ハンズオン用に用意されるもの）

    - リソースグループ：（作成したリソースグループ）

    - 仮想ネットワーク：（作成した仮想ネットワーク）

    - サブネット：（作成したサブネット）

    - ステージングの場所：（作成したストレージアカウント）

      <img src="images/ex03-0022.png" />
  
  <br />


### Task 2: バックアップの変更履歴の確認

- Azureポータルで **仮想マシン** と検索し、リストアで作成した新規仮想マシンを確認

  <img src="images/ex04-0001.png" />
  
  <br />

- 新規作成した仮想マシンの画面を開き、「概要」ページにある[接続]-[Bastion] を選択

  <img src="images/ex04-0002.png" />

  <br />

- ユーザ名、パスワードを入力して「接続」

  <img src="images/ex04-0003.png" />

  <br />

- バックアップ前に作成したファイルを開き、バックアップが正常に行われているか確認

  <img src="images/ex04-0004.png" />

  <br />


## （Option） ファイルとフォルダーのバックアップ



### Task 1: MARS エージェントのインストールとサーバーの登録

- 仮想マシンへ Bastion を使用して接続し、Azure ポータルへアクセス

- Recovery Services コンテナーの管理ブレードへ移動し、**プロパティ** を選択

- **Recovery Services Agent** の **ダウンロード** をクリックし、任意の場所へ保存

- **Backup の資格情報** ‐ **最新の Recovery Services Agent を既に使用している** にチェック、

  **ダウンロード** をクリックし、資格情報ファイルを任意の場所へ保存

  <img src="images/option-task1-001.png" />

  <br />

- ダウンロードした MARS エージェントのインストーラーを起動

- **Installation Settins** でインストール先、キャッシュ場所 (送信前データの格納先) を指定し **Next** をクリック

  <img src="images/option-task1-002.png" />

  <br />

- **Proxy Configuration** は設定を行わないので、**Next**： をクリック

  <img src="images/option-task1-003.png" />

  <br />

- **Microsoft Update Opt-In** は **Use Microsoft Update when I check for updates** を選択し **Next** をクリック

  <img src="images/option-task1-004.png" />

  <br />

- **Install** をクリックし、MARS エージェントのインストールを実行

  <img src="images/option-task1-005.png" />

  <br />

- インストール完了後、**Proceed to Registration** をクリック

  <img src="images/option-task1-006.png" />

  <br />

- サーバー登録ウィザードが起動

  ダウンロードした資格情報ファイルを指定し **Next** をクリック

  <img src="images/option-task1-007.png" />

  <br />

- **Encryption Setting** で **Generate Passphrase** をクリックし、パスフレーズを生成

  生成したパスフレーズ ファイルを指定する任意の場所を指定

  <img src="images/option-task1-008.png" />

  <br />

  ※ パスフレーズ ファイルの保存先にローカルを指定した際は警告が表示

  ※ 次の手順に進む場合は Yes をクリック

- サーバーの登録が正常に完了することを確認

  **Launch Microsoft Agent Recovery Services Agent** にチェックを付け **Close** をクリック

  <img src="images/option-task1-009.png" />

<br />

### Task 2: バックアップ ポリシーの作成

- エージェント コンソールを起動

  スタート メニューで Microsoft Azure Backup を検索、またはデスクトップ上のショートカットをダブルクリック

- **Action** メニューから **Schedule Backup** を選択

- バックアップのスケジュール ウィザードが起動、**Next** をクリック

  <img src="images/option-task2-001.png" />

  <br />

- バックアップする項目の選択で **Add Items** をクリック

  <img src="images/option-task2-002.png" />

  <br />

- **項目の選択** ボックスで、バックアップする項目を選択し **OK** をクリック

  <img src="images/option-task2-003.png" />

  ※ Bastion から仮想マシンに接続時に C ドライブ直下に作成したフォルダと追加したドライブを選択

- 選択したフォルダ、ドライブが追加されていることを確認し **Next** をクリック

  <img src="images/option-task2-004.png" />

  <br />

- **バックアップのスケジュール選択** で、バックアップの実行時間を指定

  - **Schedule a backup every**: Day

  - **At following times**: 11:30 PM

    <img src="images/option-task2-005.png" />

    <br />

- **保持ポリシーの選択** で、保存する復旧ポイントと保持期間を設定

  - **Daily Retention Policy**: 既定で選択（変更不可）、7 日

  - **Weekly Retention Policy**: オン（Saturday, 11:30 PM, 2 Weeks）

    <img src="images/option-task2-006.png" />

    <br />

- **初期バックアップの種類の選択** で **Online** を選択し **Next** をクリック

  <img src="images/option-task2-007.png" />

  <br />

- 指定した内容を確認し **Finish** をクリック

  <img src="images/option-task2-008.png" />

  <br />

- バックアップ スケジュールの作成の完了を待ち **Close** をクリック

  <img src="images/option-task2-009.png" />

<br />

### Task 3: オンデマンド バックアップの実行

- エージェント コンソールを起動

- **Action** メニューから **Back Up Now** を選択

- **バックアップ アイテムの選択** で **Files and Folders** を選択し **Next** をクリック

  <img src="images/option-task3-001.png" />

  <br />

- **バックアップアイテム（詳細）の選択** で対象のフォルダを選択し **Next** をクリック

  <img src="images/option-task3-002.png" />

  <br />


- **バックアップの保持期間** でカレンダーから日付を選択し **Next** をクリック

  <img src="images/option-task3-003.png" />

  <br />

- バックアップ ポリシー作成時に選択した項目が表示されることを確認し **Backup** をクリック

  <img src="images/option-task3-004.png" />

  <br />

- バックアップ ジョブが開始

  <img src="images/option-task3-005.png" />

  <br />

- **Close** をクリックし、ウィザードを終了（バックアップ ジョブはバックグラウンドで実行を継続）

<br />

### Task 4: ファイルの復元

- バックアップを取得したファイルの内容を変更、または削除

  <img src="images/option-task4-001.png" />

  <br />

- エージェント コンソールを起動

- **Action** メニューから **Recover Data** を選択

- **Getting Started** で **This server** を選択し **Next** をクリック

  <img src="images/option-task4-002.png" />

  <br />

- **回復地域の選択** で **Primary Region** を選択

  <img src="images/option-task4-003.png" />

  <br />


- **回復モードの選択** で **Indivisual files and folders** を選択

  <img src="images/option-task4-004.png" />

  <br />

- **ボリュームと日付の選択** で復元するファイルを含むボリュームを選択

  カレンダーから太字で表示される日付を選択、 **Time** から特定の復旧ポイントを選択し、**Mount** をクリック

  <img src="images/option-task4-005.png" />

  <br />

- **ファイルの参照と回復** で **Browse** をクリック

  <img src="images/option-task4-006.png" />

  <br />

- エクスプローラーが起動、復元するファイルをコピーし、元の場所へ貼り付け

  <img src="images/option-task4-007.png" />

  ※ 更新（削除）前の状態にファイルが復元されたことを確認

  <br />

- **Unmount** をクリック、メッセージが表示されるので **Yes** を選択し、ボリュームをマウント解除

  <img src="images/option-task4-008.png" />

  ※ 回復ボリュームは 6 時間マウント、ファイル コピーが継続中は最大 7 日間までマウント時間を延長

<br />

