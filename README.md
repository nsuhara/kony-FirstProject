# はじめに

*(Mac環境の記事ですが、Windows環境も同じ手順になります。環境依存の部分は読み替えてお試しください。)*

この記事を最後まで読むと、次のことができるようになります。

- Kony AppPlatformの概要について理解する
- Kony AppPlatformの開発環境を構築する
- Kony AppPlatformを使って簡単なiOS/Androidアプリを作成/実行する

開発環境のイメージ画像  
<img width="400" alt="スクリーンショット 2018-12-16 23.18.28.png" src="https://qiita-image-store.s3.amazonaws.com/0/326996/6c0c11b9-93f6-2735-4fc9-6df77b18d782.png">  

アプリのイメージ画像  
<img width="200" alt="IMG_0402.PNG" src="https://qiita-image-store.s3.amazonaws.com/0/326996/eb066bc7-a5f5-85ca-c09e-aee5eeb32383.png">&nbsp;->&nbsp;<img width="200" alt="IMG_0403.PNG" src="https://qiita-image-store.s3.amazonaws.com/0/326996/020dd5fe-f5ea-398b-ef90-c9e629469e84.png">

# 関連する記事

- [Kony AppPlatformで作成したiOS/AndroidアプリのAuto Layoutについて学ぶ](https://qiita.com/nsuhara/items/a52abd9861c51823ecec)
- [Kony AppPlatformで作成したiOS/AndroidアプリとSalesforceをデータ連携する](https://qiita.com/nsuhara/items/756120f1bddc6f8fe78b)
- [Kony AppPlatformで作成したiOS/Androidアプリのコーディングについて学ぶ](https://qiita.com/nsuhara/items/bf0e8884a7efc3c55176)

# 実行環境

- macOS Mojave 10.14.1
- Kony Visualizer 8.3.10

# ソースコード

実際に実装内容やソースコードを追いながら読むとより理解が深まるかと思います。是非ご活用ください。

[GitHub](https://github.com/nsuhara/kony-FirstProject)

# Kony AppPlatformとは

米Kony, Inc.により展開されるモバイル開発向けサービス(※MADP)。一般的にMADPは、異なるOS/デバイスで利用できるクロスプラットフォームのアプリを開発するためのフレームワークを含んでおり、1つのコード(例:JavaScript)からiOS、Android、Windowsなど異なるOS/デバイスのアプリを開発できる。そのため開発者は、複数のプログラミング言語を習得したり、OS/デバイスごとにアプリを個別に開発したりといったことに時間を割く必要がなくなる。  
※ Mobile Application Development Platform

>ソフトバンクモバイルは2015/4/15、法人向けに米Kony, Inc.のMADP製品(※1)を使ったモバイルアプリケーション開発プラットフォーム「ホワイトクラウド Kony Mobility Platform」の提供を開始。

この記事では、米Kony, Inc.のサービスを対象としており、ホワイトクラウド Kony Mobility Platformのサービスは使用しません。

# 開発環境の構築

1. ライセンスについて  
    Konyライセンスは**Visualizer Starter**と**Visualizer Enterprise**の2種類から選ぶことができます。ライセンス費用、サポート機能に違いがあります。例えばVisualizer StarterはXcodeを使用してアプリ(アイコン)の生成ができないなど。  
    [Explore editions & pricing](https://www.kony.com/products/visualizer/editions/)  
    <img width="500" alt="スクリーンショット 2018-12-16 21.05.39.png" src="https://qiita-image-store.s3.amazonaws.com/0/326996/b87fa846-38ed-5b81-deb7-e66e28a3bd23.png">  
    今回はフリーライセンスの**Visualizer Starter**を使用します。  

1. インストール手順(for MacOS)  
    [Explore editions & pricing](https://www.kony.com/products/visualizer/editions/)から**Visualizer Starter**の**Download for free**をクリックします。  
    次に**Visualize the Possibilities**に遷移するので**Email**を入力して**Download for free**をクリックします。  
    次にインストーラ(約1.3GB)がダウンロードされます。インストーラを解凍して実行します。  
    **Next**をクリックします。  
    <img width="500" alt="スクリーンショット 2018-12-16 21.30.45.png" src="https://qiita-image-store.s3.amazonaws.com/0/326996/08ac4a42-da7d-b3e1-9fa7-ad92839dc0ad.png">  
    **Next**をクリックします。  
    <img width="500" alt="スクリーンショット 2018-12-16 21.45.48.png" src="https://qiita-image-store.s3.amazonaws.com/0/326996/027dca13-7da4-49b0-9e66-b5d5f2c21930.png">  
    **I accept**を選択して**Install**をクリックします。  
    <img width="500" alt="スクリーンショット 2018-12-16 21.47.04.png" src="https://qiita-image-store.s3.amazonaws.com/0/326996/f195106e-726f-a874-4636-c5e9647daba9.png">  
    **Done**をクリックして完了します。  
    <img width="500" alt="スクリーンショット 2018-12-16 21.48.56.png" src="https://qiita-image-store.s3.amazonaws.com/0/326996/4052ab50-09bd-eb75-4f70-79f8026a252b.png">

# iOSアプリの作成

開発プロジェクト(FirstProject)を作成して、画面1(Form1)と画面2(Form2)で構成するアプリを作成します。

- 画面1にラベルとボタンを配置します。
- 画面2にラベルとテキストボックスを配置します。
- 最後に画面1のボタンで画面2を表示します。

1. プロジェクト作成
    **kony Visualizer.app**を起動します。  
    **New Project**をクリックします。  
    **Create Custom App**を選択して**Choose**クリックします。
    <img width="500" alt="スクリーンショット 2018-12-16 22.24.27.png" src="https://qiita-image-store.s3.amazonaws.com/0/326996/1452fdfd-1f0d-417b-d90d-131d3adc2ec8.png">  
    **Project Name**を入力して**Kony Reference Architecture**を選択して**Create**をクリックします。  
    <img width="500" alt="スクリーンショット 2018-12-16 22.31.43.png" src="https://qiita-image-store.s3.amazonaws.com/0/326996/377dffcf-ae0f-7d08-2e10-6b609f63660a.png">  
    開発環境がセットアップされます。  
    <img width="500" alt="スクリーンショット 2018-12-16 22.33.58.png" src="https://qiita-image-store.s3.amazonaws.com/0/326996/02ef00e5-0ec2-d90a-70ae-dad75576c3c4.png">

1. フォーム作成  
    Projectタブ -> Mobile -> Forms -> 右クリック -> **New Form**をクリックします。こちらをForm1とします。  
    <img width="200" alt="スクリーンショット 2018-12-16 22.40.56.png" src="https://qiita-image-store.s3.amazonaws.com/0/326996/0ef5deca-0287-0f1c-35fe-ca7125e13412.png">  
    同じ手順でもう1つFormを追加します。こちらをForm2とします。

1. ラベル/テキストボックス/ボタン作成  
    Projectタブ -> Mobile -> Forms -> **Form1**を選択します。  
    **Default Library**から**Label**を検索します。  
    <img width="200" alt="スクリーンショット 2018-12-16 23.03.13.png" src="https://qiita-image-store.s3.amazonaws.com/0/326996/b4297b4e-af5a-efd8-060a-4ff250311972.png">  
    検索結果の**Label**を**Form1**へドラッグ&ドロップして追加します。続けてLabelをダブルクリックして**Form1**に編集します。  
    <img width="500" alt="スクリーンショット 2018-12-16 23.08.57.png" src="https://qiita-image-store.s3.amazonaws.com/0/326996/079457e7-f496-33c8-c617-1d8f2dbca534.png">  
    同じ手順で**Button**を検索して**Form1**へ追加します。  
    <img width="500" alt="スクリーンショット 2018-12-16 23.18.28.png" src="https://qiita-image-store.s3.amazonaws.com/0/326996/6c0c11b9-93f6-2735-4fc9-6df77b18d782.png">  
    **Form2**も同じ手順で**Label**と**TextBox**を追加します。  
    <img width="500" alt="スクリーンショット 2018-12-16 23.20.13.png" src="https://qiita-image-store.s3.amazonaws.com/0/326996/83803f8e-b061-8b5e-177b-a3116809fe05.png">

1. 画面遷移  
    Projectタブ -> Mobile -> Forms -> Form1 -> **Button**を右クリックして**Action: onClick**をクリックします。  
    <img width="500" alt="スクリーンショット 2018-12-16 23.25.57.png" src="https://qiita-image-store.s3.amazonaws.com/0/326996/2e0e12a5-0fa8-44ed-82b6-178432ec435b.png">  
    Navigationの**Navigate to Form**をクリックして**Form2**を選択します。  
    <img width="500" alt="スクリーンショット 2018-12-16 23.30.37.png" src="https://qiita-image-store.s3.amazonaws.com/0/326996/6f31688f-5983-ee36-bd93-cc3667835463.png">

# iOSアプリの実行

iPhone端末でアプリの動作を確認します。

1. 事前準備   
    Kony Visualizer -> **Preferences**をクリックします。Functional Previewの**iOS Mobile**にチェックを入れます。  
    <img width="500" alt="スクリーンショット 2018-12-17 9.06.51.png" src="https://qiita-image-store.s3.amazonaws.com/0/326996/472f2bdb-0f13-73ad-1926-cb6002b28ea5.png">  
    iPhoneのApp Storeから**Kony Visualizer**を検索してiPhone端末にシミュレータをインストールします。

1. ビルド  
    Runをクリックしてコンパイルします。  
    <img width="200" alt="スクリーンショット 2018-12-16 23.31.49.png" src="https://qiita-image-store.s3.amazonaws.com/0/326996/4c6a37c9-fddc-50c3-64a9-25b641a73953.png">

1. アプリ実行  
    iPhoneをPCと同じネットワーク環境(LAN/テザリング)に接続します。  
    iPhoneの**Kony Visualizer**を起動してWiFiタブの**SCAN QR CODE**からビルド結果の**QRコード**を読み取ります。  
    <img width="500" alt="スクリーンショット 2018-12-17 0.10.22.png" src="https://qiita-image-store.s3.amazonaws.com/0/326996/1731a783-849f-1af6-8b8f-5f244ae9e566.png">  
    <img width="200" alt="IMG_0401.PNG" src="https://qiita-image-store.s3.amazonaws.com/0/326996/e131815d-76d5-945f-3142-f3a8e2b8792e.png">

1. アプリ操作  
    Form1のButtonをクリックします。  
    <img width="200" alt="IMG_0402.PNG" src="https://qiita-image-store.s3.amazonaws.com/0/326996/eb066bc7-a5f5-85ca-c09e-aee5eeb32383.png">  
    Form2へ遷移します。TextBoxを入力します。  
    <img width="200" alt="IMG_0403.PNG" src="https://qiita-image-store.s3.amazonaws.com/0/326996/020dd5fe-f5ea-398b-ef90-c9e629469e84.png">
