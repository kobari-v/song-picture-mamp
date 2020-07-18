## 機能一覧
- 曲一覧表示機能

- 歌詞詳細機能

- ユーザー一覧表示機能

- 管理ユーザー認証機能(/admin でアクセスする)=>わかりやすいように遷移できるボタンつけました。

- 管理画面から曲を投稿できる

- ユーザー認証機能

- ページネーション機能

- 検索機能

- 画像投稿機能

- 匿名コメント機能

- ユーザー認証コメント機能

- １つの曲に対して、タグを紐づける機能（多対多）

- いいね機能(Vue/Ajax)

- ページネーション機能

- CircleCIでテストの自動化（テストコードは現在追記中）

# トップページ
詳細ページで歌詞を閲覧できます。
![スクリーンショット 2020-06-25 5 33 33](https://user-images.githubusercontent.com/51937772/85625242-187ea200-b6a6-11ea-914e-f7054c18d92c.png)

# 管理画面
ここから歌詞データを登録する
![スクリーンショット 2020-06-25 5 34 52](https://user-images.githubusercontent.com/51937772/85625345-48c64080-b6a6-11ea-94d7-a8f7d3295b8b.png)

# 使用技術一覧

* HTML

+ CSS

- Javascript / Vue.js / Ajax

* PHP 7.2 

+ Laravel 5.5

- MySQL

- Linux(各種コマンド操作)

- Nginx(Web Server)

- Git/GitHub(pull request, Issues 等による擬似チーム開発)

-  CircleCI

- AWS 
  - EC2/RDS/VPC/IAM/Route53/ELB
  
# その他

1. github の issue,pullRequest 活用

# インフラ構成図

<img width="700" alt="https.png" src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/439295/995098d0-ef70-e0d8-1110-49a166d18862.png">

# 作った目的と意識したこと
1. Laravelの理解度を向上させる

· これを作ろうとした当時はCRUD機能をどう実装すればいいのか分からないレベルでした。
６割ほど完成しましたが、基本的なPHP/Laravelの理解度は格段に深まったと思います。
なので、UI部分はそこまで意識せずテンプレートを使いまわしながら少し変えています。

2. 閲覧者、採用者の手間を減らす。

· 認証機能を最低限のものでかつメアドやパスワードを初めから表示してEnterを押すだけにしたり、決済機能や外部サービス認証など確認するのが面倒な機能は避けるようにして、見る人の工数を少なくできるよう工夫しています。
インフラにAWSを使って読み込みを早くしているのもそのためです。

# インストール方法

```
composer install

npm install

php artisan serve

npm run watch

php artisan migrate --seed
```

# やりたいこと
1. ファットコントローラー防止
2. 意味のある単体テストを記述
3. ８GBで使用するとメモリ不足で重くなったので（ https://github.com/masal9pse/docker-laravel-apache ）、16GBを買ったらローカルでDocker,docker-composeを使用する。
4. UI/UX を整える
5. テストコードをさらに追記する。
