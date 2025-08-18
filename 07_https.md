# HTTPSでWEBページを表示する

### 現状

現状VPSに設定したHTMLにアクセスはできますが、「http://」でしかアクセスできません。皆さんがWEBサイトを眺めていてよく目にするURLのもう一つは「https://~~~」だと思います。試しに`https`書き換えてみてもエラーになります。

![httpsだとエラー](./assets/07/01.jpg)

httpのURLに再度戻して、chromeであれば左上の方を見ると「保護されていない通信」と表示されています。

![http](./assets/07/02.jpg)

`http`と`https`の違いは一言で言えば「その通信が暗号化されているかどうか」です。第三者に通信を覗かれた場合に、`http`は通信が生の状態で（この状態を「平文」と言います）送受信されますが、`https`だと自分と通信相手のサーバーの間では通信が暗号化されます。つまり`https`の方がセキュアということになります。

今後VPSでWEBサイトを公開していくなら`https`に対応している方が「お、分かってるね」となり格好がつきますので、対応させていきましょう。

### Nginxの設定を更新する
まずnginxの設定を更新していきます。VPSにログインします。

![ssh](./assets/07/03.png)

`vim`でnginxの設定ファイルを開きます。

```bash
sudo vim /etc/nginx/site-enabled/default
```

![vim](./assets/07/04.png)

下にスクロールしていくと`server_name _;`と書かれた箇所があると思います。この`_`の部分をご自身のVPSのホスト名に変更してください。

![server_nameの箇所を見つける](./assets/07/05.jpg)

![server_nameの箇所をホスト名に変更する](./assets/07/06.jpg)

更新できたら`:wq`で変更を保存して`vim`を終了します。

変更を反映させるために`sudo systemctl reload nginx`を実行します。

![nginxのreload](./assets/07/07.png)

何も表示されていなければ成功です。

念の為この状態で元々のWEBサイトが表示できるか確認しておきましょう。

![htmlの表示を確認](./assets/07/08.png)

前と変わらず表示できていればOKです🎉

### 証明書

ここからHTTPS対応を行なっていきますが、そのために必要なものは何かというと「証明書」というものが必要になります。

証明書とは、あなたのサーバーが本物であることを証明するデジタルファイルです。WEBサイトにアクセスする際、ブラウザは「このサーバーは本当に正しいサーバーなのか」を確認する必要があります。

証明書には以下の情報が含まれています：
- このサーバーのドメイン名（例：example.com）
- サーバーの公開鍵（暗号化に使用する）
- 証明書を発行した認証局（CA：Certificate Authority）の署名

証明書があることで：
1. ブラウザがサーバーの身元を確認できる
2. 通信を暗号化するための鍵を安全に交換できる
3. 第三者による通信の盗聴や改ざんを防げる

証明書は認証局（CA）という第三者機関が発行します。Let's Encryptという無料の認証局があり、これを使えば無料でHTTPS証明書を取得できます。

### certbotをインストールする

いきなり専門的な話が出てきて混乱したかもしれませんが、これらのことを簡単に・無料で行える、Let's Encryptの`certbot`というツールを使用します。

VPSにログインします。

![ssh](./assets/07/09.png)

`sudo apt update`と実行し、これからインストールするソフトが最新の状態になるようにします。

![ssh](./assets/07/10.png)

少し時間がかかる可能性がありますがログが最後まで流れたら完了です。

![ssh](./assets/07/11.png)

続いて`sudo apt install snapd`を実行します。

![ssh](./assets/07/12.png)
何か聞かれれば`Y`と入力してEnterでOK。

![ssh](./assets/07/13.png)

`snapd`は、Linuxの「パッケージ管理システム」です。certbotはsnapパッケージとして提供されているため、snapdが必要になります。

`snapd`のインストールが完了したら続いて以下のコマンドを実行してください。

```bash
sudo snap install core; sudo snap refresh core
```

![ssh](./assets/07/14.png)

続いて`sudo snap install --classic certbot`で`certbot`をインストールします。

![ssh](./assets/07/15.png)

最後に`sudo ln -s /snap/bin/certbot /usr/bin/certbot`というコマンドを実行してください。

![ssh](./assets/07/16.png)

### certbotを使って証明書を取得する

それでは実際に証明書を取得していきます。

`sudo certbot --nginx`と入力してください。

![ssh](./assets/07/17.png)

☝️まずemailを尋ねられます。ご自身のメルアドを入力してEnter。

![ssh](./assets/07/18.png)

☝️続いて利用規約への同意を求められます。`Y`と入力してEnter。

![ssh](./assets/07/19.png)

☝️Let's encryptからのお知らせを受け取るか尋ねられています。自分は`N`としました。

![ssh](./assets/07/20.png)

☝️どこドメインに対してHTTPS対応するのか聞かれています。候補にご自身のホスト名が出ているはずですので、それに対応した番号（この画像なら`1`）を入力してEnter。

![ssh](./assets/07/21.png)

`Successfully~~~`と表示されていれば成功です🎉

では実際に`https`でアクセスできるようになっているか確認しましょう。

![ssh](./assets/07/22.png)

`https://{ホスト名}`でアクセスするとアクセスができて、chromeならURLの横のアイコンを押すと「この接続は保護されています」と表示されています🎉