# さくらVPS（ubuntu）チュートリアル

このチュートリアルでは、さくらVPSを使用してWebサーバーを構築し、HTTPSでWEBページを表示するまでの手順を学習できます。

## 目次

1. [Ubuntuサーバーのセットアップ](./01_setup_vps.md)
   - VPSの購入
   - VPSの起動・ログイン

2. [Linuxの基本的な使い方](./02_how_to_use_linux.md)
   - ディレクトリ操作（pwd, cd, mkdir, ls）
   - ファイル操作（touch, less, vim）

3. [Nginxのインストール](./03_install_nginx.md)
   - Webサーバーについて
   - Nginxのインストール
   - パケットフィルター設定

4. [独自のHTMLを表示する](./04_create_html.md)
   - HTMLファイルの作成
   - Nginxの設定ファイルの理解
   - ファイル所有者の変更

5. [SSH接続する](./05_connect_ssh.md)
   - パスワードでSSHログイン
   - 公開鍵認証の設定
   - セキュリティの向上

6. [HTTPSでWEBページを表示する](./07_https.md)
   - HTTPS化の必要性
   - SSL証明書について
   - certbotを使用した証明書取得

7. [デプロイ（Mac・WSL）](./06_deploy.md)
   - ローカルでのファイル作成
   - rsyncを使用したデプロイ

## 前提条件

- さくらVPSのアカウントを持っていること
- 基本的なコマンドライン操作の知識があること（学習しながらでも大丈夫です）

## 対象者

- Webサーバーの構築を学びたい初心者
- LinuxやVPSの基本的な操作を覚えたい方
