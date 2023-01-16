# 機能設計書

## 機能一覧表

| 機能名                   | 説明                                                                              |
| ------------------------ | --------------------------------------------------------------------------------- |
| Blocto ログイン 機能     | コントラクトウォレットを作成する機能                                              |
| IDQ トークン発行機能     | IDQ トークンを発行する機能                                                        |
| IDQ トークン送信機能     | IDQ トークンを送金する機能                                                        |
| IDQ トークン購入機能     | IDQ トークンを購入する機能                                                        |
| DID 登録機能             | 新規ログイン時に DID を発行し、スマコンに登録する機能                             |
| DID 関連データの登録機能 | DID と紐づく情報(VC)をIPFSに登録する機能                                          |
| DID 関連情報表示機能     | DID と紐づく情報を表示する機能                                                    |
| 共通資金プール作成機能   | 共通資金プールであるマルチシグコントラクトを作成する機能                          |
| 共通資金プール送金機能   | マルチシグコントラクトから目的のアドレスへ送金する機能                            |
| 共通資金プール送金機能   | 共通資金プール送金のために承認する機能                                            |
| deposit 機能             | IDQ トークンを使ってマルチシグコントラクトにネイティブトークンを deposit する機能 |

## 画面一覧

| 画面名                  | 概要                                                            |
| ----------------------- | --------------------------------------------------------------- |
| ログイン画面            | blocto SDK の機能を使って IDQ にログインする画面                |
| Home 画面               | DID と保有している IDQ トークン・DID と紐づく情報を表示する画面 |
| 送金画面                | 指定した DID に対して送金する画面                               |
| 購入画面                | IDQトークンを購入する画面                               |
| DID 関連情報検証画面     | 自身のDIDに紐づくVCを表示・検証するための画面                        |
| MultiSigWallet 画面     | Wallet を管理する画面。deposit 機能が使える                     |
| create Transaction 画面 | トランザクションデータを作成する画面                            |
| Transation 管理画面     | MultiSigWallet が管理するトランザクションデータを操作する画面   |

## 変数一覧

| コントラクト名 | 変数名           | 型                         |  内容    |
| -------------- | ---------------- | ------------------------------- | ----- |
| MyToken    | tokenName        | string  | トークンの名前          |
| MyToken    | tokenSymbol      | string    | トークンのシンル  |
| WalletFactoryV4  | wallets       | [MultiSigWallet]  |  MultiSigWallet型の配列を保持する変数 |
| WalletFactoryV4  |  maxLimit     | uint256 | 関数から返すことのできる最大値 |
| WalletFactoryV4 | owner  | address  | WalletFactoryV4 コントラクトのowner アドレス  |
| WalletFactoryV4   | isRegistered    | mapping(address => bool)        | コントラクトウォレットアドレスに紐づくDIDが生成されているチェックするためのmap  |
| WalletFactoryV4   | dids        | mapping(address => string) | DIDとコントラクトウォレットのアドレスを格納するMap (アドレスからDIDを求めるためのmap)   |
| WalletFactoryV4  | addrs    | mapping(string => address)     | DIDとコントラクトウォレットのアドレスを格納するMap (DIDからコントラクトウォレットのアドレスを求めるためのmap)   |
| WalletFactoryV4   | vcs | mapping(address => string)  | コントラクトウォレットとVCまでのURLを格納するMap   |
| MultiSigWallet   | Transaction  | struct    | トランザクションデータ用の構造体       |
| MultiSigWallet   | walletName  | string    | マルチシグウォレットの名前       |
| MultiSigWallet   | owners      | [address]    | Ownerのアドレスを格納する配列       |
| MultiSigWallet   | required    |  uint256   | 閾値       |
| MultiSigWallet   | transactions     | [Transaction ]  | トランザクションデータを格納する配列       |
| MultiSigWallet   | isOwner      | mapping(address => bool)    | アドレスとowner権限の有無を紐付けるmap       |
| MultiSigWallet   | approved      | mapping(uint256 => mapping(address => bool))    | トランザクションID毎にonwerの承認状況を紐づけるmap      |
|    |        | | |

## メソッド一覧

| コントラクト名 | メソッド名            | 内容                         |
| -------------- | --------------------- | ---------------------------- |
| MyToken        | pause                 | トークンを停止するための関数 |
| MyToken        | unpause               | 停止状態を解除するための関数 |
| MyToken        | mint                  | トークンを発行する関数       |
| MyToken        | burnToken             | トークンを償却する関数       |
| MyToken        | \_beforeTokenTransfer | トークン移転用の関数         |
| MyToken        | \_afterTokenTransfer  | トークン移転用の関数         |
| MyToken        | \_mint                | 発行用の関数                 |
| MyToken        | \_burn                | 償却用の関数                 |
| WalletFactoryV4  |  walletsCount |  MultiSigWalletのインスタンス数を取得する関数     |
| WalletFactoryV4  | createWallet       |  MultiSigWalletのインスタンス生成関数     |
| WalletFactoryV4| getWallets|  作成済みウォレットの情報を取得するメソッド |
| WalletFactoryV4 | register                      |  DIDとコントラクトウォレットのアドレスを紐づけるためのメソッド    |
| MultiSigWallet | receive()  |  入金用のメソッド |
| MultiSigWallet |submit   |トランザクションデータを作成するメソッド  |
| MultiSigWallet |approve   |指定したIDのトランザクションを承認するメソッド |
| MultiSigWallet |_getApprovalCount   | 指定してIDのトランザクションの承認数を取得する。  |
| MultiSigWallet |execute   | トランザクションをブロードキャストするメソッド  |
| MultiSigWallet |revoke   | トランザクションの承認を削除するメソッド  |
| MultiSigWallet |getName   | ウォレットの名前を取得するメソッド  |
| MultiSigWallet |getRequired   |  ウォレットの閾値を取得するメソッド |
| MultiSigWallet | getOwnersCount  | ownerのアドレス数を取得するメソッド  |
| MultiSigWallet | getTxs  |トランザクションデータを全て取得するメソッド   |
|                |                       |                              |


## API 一覧

| メソッド種類 | API 名              | 概要                                         |
| ------------ | ------------------- | -------------------------------------------- |
| POST         | /api/mintIDQ        | IDQToken を発行する API                      |
| POST         | /api/burnIDQ        | IDQToken を償却する API                      |
| GET          | /api/balance/IDQ    | IDQToken の残高を取得する API                |
| POST         | /api/send           | IDQToken を送金する API                      |
| POST         | /api/create         | DID を作成する API                           |
| GET          | /api/resolve        | DID ドキュメントを検索する API               |
| POST         | /api/excute/factory | FactoryWallet のメソッドを実行するための API |
| POST         | /create-payment-intent   |  stripeのPayment elementを使うためのAPI    |
| POST         | /api/registerIpfs   | VCを生成し、IPFSに登録するAPI   |
|              |                     |                                              |
