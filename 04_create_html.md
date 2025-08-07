# 独自のHTMLを表示する

自分で作成したhtmlファイルをWebサーバーで表示させたいと思います。

### htmlファイルの作成

`cd /var/www/html`と入力し、ディレクトリを移動してください。

![/var/www/htmlへ移動](./assets/04/01.jpg)

`touch index.html`と入力し、htmlファイルを作成。

![index.htmlを作成](./assets/04/02.jpg)

`sudo vim index.html`でvimを起動し、以下のコードをindex.htmlに書き込む。

```html
<!DOCTYPE html>
<html lang="ja">
    <head>
        <meta charset="UTF-8">
    <title>さくらVPS チュートリアル</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 50px;
            background-color: #f0f0f0;
        }
        .container {
            background-color: white;
            padding: 30px;
            border-radius: 10px;
            max-width: 500px;
            margin: 0 auto;
        }
        h1 {
            color: #2c3e50;
        }
        .success {
            color: #27ae60;
            font-size: 18px;
            margin: 20px 0;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>さくらVPS チュートリアル</h1>
        <div class="success">
            ✅ Webサーバーが正常に動作しています！
        </div>
        <p>おめでとうございます！</p>
    </div>
</body>
</html>
```

ファイルを更新できたら再度VPSのURLにアクセスしてみてください。表示される画面が上で更新したhtmlの内容になっていれば成功です。

![htmlが表示される](./assets/04/03.jpg)

### なぜ表示されるのか