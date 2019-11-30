# 開発環境を作る

さて、何をするにおいても開発環境が必要です。この章では開発環境の作り方を簡単に解説していきます。

* ターミナル
* テキストエディタ・IDE
* 言語処理系
* Docker

この章ではこれら4つ以外も紹介していますが、ひとまずこの4つは必須だと思っておいた方がいいでしょう。

## ターミナル

文字列を表示する専用のアプリケーションがターミナルです。

WindowsではPowerShellなどを起動すると出てくるのがターミナルです。
macOSではターミナル.appが標準で入っていますが、一部の人にはiTerm2などが人気です。
UNIX/Linuxでは、GUIをオフにして起動していると、全画面がそのままターミナルそのものです。
GUI（X window system）をオンにして起動している場合は、そのOS・ディストリビューションによって、
さまざまなターミナルソフトがインストールされています。

プログラミング開発ではターミナルは避けて通れません。

ターミナルでは主に、シェルと呼ばれるアプリケーションが動作しています。
WindowsではPowerShellが有名でしょう。

macOS/LinuxやWSL（Windows subsystem for Linux）を含むUNIX系OSでは、
sh/csh/bash/zsh/fishなどのシェルがありますが、UNIX系シェルは基本はどれも同じです。

現代ではshとcshはなかなか見かけることはありません。
標準的に使われるものとしてはbashでしょうか。
ただ最近はmacOSではzshが標準になったため今後はzshが標準といわれる日が来るかも知れません。

シェルは、シェルコマンドという少し独特な形式で命令を与えて、
さまざまなアプリケーションを動かします。

ターミナルのみで動くアプリケーションのことをコマンドラインインターフェース（CLI）アプリと呼びます。
CLIアプリは一部の例外を除くと、自動で動かすのに向いています。

シェルはシェル言語と呼ばれる、簡易的なプログラミング言語を搭載しており、
このシェル言語によりさまざまな処理を自動化することができます。

## テキストエディタ・IDE

テキストを編集するときに使われるのがテキストエディタやIDEです。
ワープロなどはテキストを編集するには向いていません。

最近一番有名でソフトウェア開発者の多くが使っているテキストエディタは、
Microsoft社のVisual Studio Code（VSCode / Code）です。
とても軽量・高速動作をするテキストエディタで、しかもIDE機能と呼ばれるものも搭載しています。

IDE（Integrated Development Environment）は日本語に訳すと統合開発環境のことです。
元々Visual StudioやIntelliJ IDEAやEclipseなどが有名ですが、
一般的にはテキストエディタよりは重く、プログラミング開発に特化しているとされています。

VSCodeは、並のテキストエディタと比較しても軽量・高速なのに、
有料のIDEに匹敵するだけの統合開発環境としての機能も有していて、無料で誰でも自由に使えるというものです。

部分的には専門のIDEの方が機能面で有利なときもありますが、
VSCodeは無料かつ設定をしなくても大体使いやすいという利点があり、
元々IDEを使い慣れたチームで無ければ、VSCodeをチームで導入検討すべきです。
もちろん、個人開発でも同じです。

特定のこだわりでも無ければVSCodeを使うのがテッパンです。

また、Debugger for Chromeという拡張機能を使うと、VSCodeでブラウザのJavScriptやTypeScriptのでバッグを行うことが可能です。
Webアプリケーション開発において、ブラウザ上でのJavaScriptのデバッグは非常に重要ですので、おすすめです。

## それぞれの環境のパッケージシステムを使おう

大抵のOSには、OSごとのパッケージシステムというものがあります。

macOSでは、Apple公式ではありませんが、ほぼ公式といっていいほどの普及率を誇るHomebrewがあります。
RedHat系Linuxではyumが使われます。
Debian系Linuxではaptが使われます。

大体どのパッケージシステム・パッケージマネージャも同じような動作をします。

### macOS: Homebrew

https://brew.sh/ にアクセスすると、インストール手順が書かれているので、
ターミナルを開いて書かれているコマンドをコピペするだけでインストールができます。

Homebrew は `brew` コマンドで、パッケージのインストールや削除、メンテナンスなどを行います。

```sh
$ brew install anyenv
```

これは anyenv という便利アプリをインストールするためのコマンドです。

macOSで何かを動かすときは、大抵Homebrewでインストールを行うためインストールしておきましょう。

## anyenv

anyenv は最近プログラミング言語（処理系もいいます）をインストールするときの定番ツールです。

正確には、anyenv は、それぞれの言語ごとの処理系インストールをインストールする汎用ツールです。

1. anyenv をインストールする
2. 言語に合わせた *env をインストールする（例: Node.jsを扱う為の nodenvや、Pythonのpyenv）
3. nodenv を使って、Node.jsをインストールしたり、バージョン選択を行う

## Pythonの開発環境を作る

世の中には様々なプログラミング言語があり、様々な開発環境が存在します。
開発環境の選定を間違うと、非常に効率の悪い開発を行うことになりかねません。
この章では、個人的なおすすめのPythonの開発環境について記述します。

### Pythonのインストール

まず、Python本体のインストールを行います。
インストール方法は環境OS(Mac OSかWindowsか)によって異なりますが、重要なことは、
Pythonのバージョン管理を簡単に行うことができるように設定をすることです。

Python本体をOS上に直接インストールしてしまうと、バージョンの更新が非常に難しくなってしまいます。
執筆時点(2019年10月)のPythonのStableバージョンは3.8.0ですが、例えば3.9.0がリリースされた場合、
バージョンを更新するためには、OS上のPython環境を依存している設定ファイルなどを含めてすべて上書きする必要があります。

では、そもそもなぜPythonのバージョンを変更する必要があるのでしょうか。
Pythonに限らずプログラミング言語のバージョンアップでは、便利な記法の追加やパフォーマンスの向上、
バグの修正などが実施されていることが多いです。
なので、特別な理由がない限りは、最新の安定バージョンを利用するほうがメリットが多いのです。

Pythonのインストールは、バージョン管理ツールを介して行うことをおすすめします。
Pythonのバージョン管理ツールを介してPythonをインストールすることで、コマンド一つでPythonのバージョンを切り替えることも、
新しいバージョンのPythonをインストールする事もできます。

Pythonのバージョン管理を行うことができるツールとして大きく分けると下記2つが挙げられるかと思います。

* Anaconda
* pyenv

ざっくりとそれぞれの特徴について解説します。
AnacondaはMac OSとWindowsの両方に対応しています。
また、機械学習で利用するライブラリのデフォルトインストール、依存関係の解決などを行ってくれますので、
機械学習を利用する場合は、便利に利用することができます。
また、GUIが付属しておりますので、GUIでライブラリの追加やPythonの環境の作成などを行うことができます。
ただし、Anaconda自体が少しサイズが大きく、最小限の環境を構築したい、という用途には向きません。

pyenvはコマンドラインで使用するツールとなっており、GUIで操作することはできません。
また、Windowsには対応しておりません。
ですが、Mac OSの場合はhomebrewで簡単にインストールすることができ、pyenv自体のサイズも小さいため、
Macユーザーにとっては便利に利用することができるツールです。

最後に、クラウドの開発環境についても言及しておきます。
例えば、PythonであればGoogle　ColaboratoryやWanboxなどを利用すると、ローカルマシンにPythonをインストールすることなく、
Pythonのコードを実行することができます。
もちろん、クラウド開発環境には制限などはありますが、試しにコードを実行したい、という用途に関しては、
クラウドの開発環境でも十分だと思います。


### Pythonの開発で必要なツールたち

Python自体のインストールが環境すれば、Pythonのコードを書くことはできます。
ですが、チーム開発、プロダクションのコードを開発する上で、便利なツールを使うことで、
開発効率・品質の向上を達成することができます。
いくつかおすすめのツールについてご紹介いたします。

**Pylint**

Pythonのコード解析ツールになります。
Pythonらしくないコードの警告表示や、エラー表示などを行うことができます。
Pylintを使うことで、コードを書いている最中に、文法的におかしい部分やエラーの指摘が表示されるので、
開発効率・品質の向上が期待できます。
どうしても必要な記述に警告が出る場合は、ソースコード内に`#pylint: disable=`に警告を非常時にしたいルールを記述し、
その後`#pylint: enable=`に非表示にしたルールを再度有効にする設定をします。
これによって、コード内の一部のみPylintのルールを適用外に設定することが可能です。

**mypy**

Pythonは動的型付言語ですが、明示的に型情報をつけることも可能です。
ただし、型情報は実行時には評価されません。(例えば、int型で定義した変数にfloat型の値を代入しても実行時エラーにはなりません)
Python自体には型情報を評価する仕組みがないので、外部ツールを使って型情報の評価を行う必要があります。
そのためのツールとしてmypyの利用をおすすめします。
変数が定義されている型以外の値が代入されると、警告を表示することができます。

**black**

Pythonのコードフォーマッターになります。
複数人で開発をしていると、改行のタイミングがバラバラであることはよくあります。
ソースコードの書き方は統一されているべき、という考えに沿って、ソースコードを自動的に整形してくれるツールになります。
注意点として、以下2点を挙げておきます。

* Pythonコードがエラーの場合はコードの整形が実施されない
* blackのコードの整形ルールとPylintのルールが衝突する事があり、blackでコード整形後にPylintで警告が出ることがある


**pytest**

プロダクションのソースコードには、テストコードを書くことが望ましいとされています。
Pythonでテストコードを書く際に利用するツールとして、pytestがおすすめです。
pytestは他のテストツールと比較して、エラーの表示がわかりやすい、fixturesなどの便利な機能がある、
といったメリットがあります。
Pythonコードの単体テストを記述する際には、pytestの利用をおすすめします。


**Visual Studio Code(VSCode)**

テキストエディタではなく、統合開発環境として利用します。
上述した、「Pylint」、「mypy」、「black」をVSCodeに設定することで、VSCode上でコードの整形、警告の表示などを行うことが可能です。
また、jupyter notebookの直接編集・実行やPythonコードのデバッグ実行なども可能です。
Anacondaやpyenvで作成したPythonのバージョンを、VSCode内のPython環境に適用することも可能です。
Pythonをローカル環境で開発するためには、なくてはならないツールかと思います。


## Node.jsの開発環境を作る

この章では個人的におすすめのNode.jsの開発環境について説明します。

### Node.jsのインストール

Pythonの開発環境構築の節でも言及しましたが、Node.jsも同様にバージョン管理ができるように設定することが重要です。
特にNode.jsは約1年周期でメジャーバージョンのアップデートが行われるため、頻繁にバージョンを更新する機会が訪れます。
Node.jsのバージョン管理を行うツールは様々ありますが、執筆時点(2019年10月)でのおすすめはnvmを使用する方法です。
anyenvを使う場合はnodenvを使うのが標準的です。

ただし、注意点としてWindowsには対応しておらずUNIX系OSのみの対応となります。
Windowsの場合は、Nodistが選択肢に入るかと思います。

Node.jsの他の言語と同様に、バージョンアップごとに機能改善やパフォーマンス改善が実施されておりますので、
最新の安定版を使用することを推奨します。
執筆時点の安定版はNode.js 12系となります。

### Node.jsの開発で必要なツールたち

Node.jsの開発において、便利なツールについて紹介します。

**ESLint**

コードのチェックツールです。
コード規約に違反している記述がないかどうかをチェックすることができます。

**prettier**

コード整形ツールです。
複数人で開発する場合、コードの記述方法がバラバラだと非常に可読性の低いコードとなってしまいます。
コードの記述方法を統一するために、コードの整形ツールの利用をおすすめします。

**Jest**

JavaScriptやTypeScript、ReactやVue.jsなどの単体テストを記述する際に利用するツールです。
JavaScriptなどの関数の単体テストだけでなく、Reactなどのフレームワークにも対応している、
非常に人気のあるテストツールです。






## Docker

Dockerは環境構築の面倒さを全て引き受けてくれる救世主です。
プログラミング開発で一番最初から最後までつきまとう困りごとは、環境構築です。
手作業で手順書にしたがってインストール作業をすると、大抵細かい差違が生じます。
手順書があればまだいい方という環境も多いでしょう。
そもそもOSによっては、手順すら別物になります。

Dockerでは統一的な手順で、設定ファイルがあれば全自動で環境が構築可能です。
そのため、Docker登場後は、環境構築が完全に別物になりました。

チームに参加した場合も、Dockerが整備してあれば、Dockerに任せれば、
ほぼ自動で環境ができあがります。なんと素晴らしいことでしょうか。

さて、WindowsやmacOSでは、公式サイトからDockerをダウンロードしてきてインストールするのが手っ取り早いでしょう。
場合によってはインストールしている別のアプリケーション（主にWindowsでは仮想環境）と衝突することもある点は注意しましょう。

Linuxでは、OSとDockerのバージョンによって割と面倒な手順を踏む必要があります。
アップデートが面倒なことも度々あります。
残念ながら、その時代に合った最新版をクリーンインストールするのがもっとも確実です。

### NVIDIA Docker

Dockerの最新開発版ではそこそこDocker自体に取り込まれているようですが、
Dockerの亜種に、NVIDIA Dockerというものがあります。

NVIDIA Dockerでは、NVIDIA GPUをコンテナの中で利用できます。
主に、機械学習などGPGPU目的で使われます。

NVIDIAドライバーやDockerのインストール手順は時代によって一気に変わるため、大抵の手順は古くなってしまいます。
必ず、その時点の最新の手順を調べた上で、クリーンインストールをしましょう。

古い手順や、古いLinuxをアップデートしていくやり方は決してオススメできません。

#### [column] Docker や NVIDIAのインストールが極めて面倒な理由

LinuxでDockerをインストールするのは大抵面倒です。NVIDIAのドライバその他をインストールするのも同様です。
これはなぜでしょうか？OSS版DockerはDocker CEと呼ばれるバージョンのものですが、
大抵ディストリビューションパッケージのリポジトリとは別管理だからです。

そのため、Docker専用のリポジトリの追加などの工程を踏む必要があります。
ディストリビューションにDockerが入っている事例もありますが、大抵はメンテナンス不足で問題しか生じないので、
素直にDockerリポジトリから取ってくることが最善手となります。

NVIDIAは、元々OSS部分がほとんどないため、OSSやフリーソフトウェアにこだわるLinuxディストリビューションとは相性が悪いです。
そのため、インストール手順が大体面倒なことになりがちです。

最近のUbuntuなどは、DockerやNVIDIAドライバを簡単にインストールできる仕組みがある程度整ってきていますが、
クリーンインストール以外では大体苦労するので、大抵のケースでは、クリーンインストールせざるを得ないのです。

こういったものはやはり、WindowsやMacの方が遙かに楽です。

もっとも最近のMacはNVIDIAではなくRadeon GPUを搭載しているため、GPGPUにおいては致命的に問題も多いのが困りものです。

#### [/column]


<!--
### Radeon Open Compute
書ける人いたら是非！！！！
-->


## 開発環境のインフラはどう作る

#### Infrastrucure as Code

Infrastrucure as Codeとは、サービスを手動で作成するのではなく、何かしらのテンプレートファイルからサービスを自動的に作成する、という考え方です。
例えば、AWSのEC2を作成することを考えてみましょう。EC2の作成には、インスタンスタイプの選択から、VPCの作成、OSの選定やネットワークの設定など、設定すべき項目がたくさんあります。本来であれば、マネジメントコンソールと呼ばれるWeb画面から手動で設定を選択肢、EC2を作成する必要があります。ですが、AWSのCloudformationというサービスを利用することで、YML形式のファイルにEC2の設定(インスタンスタイプやVPCの設定など)を記述すると、作成したYMLファイルから自動的にEC2を作成してくれます。

Infrastrucure as Codeのサービスを利用することで、一つのテンプレートファイルから、全く同じ環境を複数作成することが可能となります。サービスの作成作業を自動化することで、人的ミスを防ぐことができますし、開発環境と本番環境で設定が異なる、という事象を防ぐことができます。

では、もう少し具体的に見ていきましょう。
下記コードがAWSのサービスをserverless frameworkというツールで作成するための、
テンプレートファイルになります(ファイル名はserverless.yml)。

```
service: serverless-demo

custom:
  tableName:
    dev: 'dev_test_table'
    prod: 'test_table'

provider:
  name: aws
  runtime: python3.7
  stage: ${opt:stage, 'dev'}
  region: ap-northeast-1

functions:
  hello:
    handler: handler.hello
    name: ${self:provider.stage}-lambdaName
    environment:
      TABLE_NAME: ${self:custom.tableName.${self:provider.stage}}
    events:
      - http:
          path: users/create
          method: get
```

上記のテンプレートファイルを用いると、`sls deploy`というコマンドを実行するだけで、
API Gateway + Lambdaの構成を作ることが可能です。
Infrastrucure as Codeの便利なところは、コマンド一つで、複数のサービスを自動で作成することができる点です。

上記のテンプレートは、開発環境と本番環境の両方に対応しています。
`sls deploy --stage dev`としてコマンドを実行すると下記名前でサービスがデプロイ(作成)されます。

* API Gateway: dev-serverless-demo
* Lambda: dev-lambdaName

また、`sls deploy --stage prod`としてコマンドを実行すると、下記名前でサービスがデプロイ(作成)されます。

* API Gateway: prod-serverless-demo
* Lambda: prod-lambdaName

また、開発環境と本番環境で参照するテーブル名はLambdaの環境変数として関数に渡しているため、
Lambdaのコードは開発環境と本番環境で同じものを使いながら、参照先テーブルを変える、ということができます。
開発環境のLambdaはdev_test_tableテーブルを参照し、本番環境のLambdaはtest_tableテーブルを参照します。

Infrastrucure as Codeで、開発環境と本番環境を構築する際に重要となるのは、
サービスを作成するテンプレート内に変数を埋め込み、開発環境と本番環境を同じテンプレートから作成できるようにすることです。
また、Lambdaなどのコード部分は、環境変数などでテーブル名を渡すようにし、開発環境と本番環境で同一のソースコードを利用することです。
これにより、開発環境と本番環境で限りなく同じ環境を作ることができるため、事前のテスト、デバッグがしやすくなります。

**注意事項：**

上記のserverless.ymlを実際に利用してサービスの構築をしないようにお願いします。
認証なしのAPIが作成され非常に危険であり、Lambdaに必要な権限があたっていないため、
全く役に立たないLambda関数が作成されるためです。

#### [column] オンプレミスでもInfrastrucure as Codeは利用していこう

ここではAWS（クラウドサービス）を利用した方法が記載されていました。
しかし、オンプレミスなサーバを構築する場合においてもInfrastrucure as Codeは積極的に利用するようにしていきましょう。

どんなに完璧な手順書があっても、人間が操作する以上はミスも起こすし、何より手間と時間がかかります。
chefやansibleといったプロビジョニングツールを利用するも良し、最悪はシェルスクリプトで実施するも良し。
まずは構築手順をコードに落とし、構築作業を人間の手から離れるようにしていきましょう。

また、作成したサーバ環境は、Serverspecを利用することで予想通りに構築されているかを確認できます。
構築対象のサーバの初期状態についても、VirtualBox+Vagrantの利用で簡単に用意できます。
VirtualBox＋Vagrant、プロビジョニングツール、Serverspecを組み合わせれば、サーバ構築手順の自動テストだって可能です。

#### [/column]