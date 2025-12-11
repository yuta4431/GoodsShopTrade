━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
データベース設計書
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

■ プロジェクト名

GoodsShop&Trade


■ データベース概要

データベース名：goods_shop_trade
文字コード：utf8mb4
照合順序：utf8mb4_unicode_ci


━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
テーブル一覧
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. users（会員）
2. admins（管理者）
3. products（商品）
4. categories（商品カテゴリ）
5. carts（カート）
6. orders（注文）
7. order_items（注文明細）
8. product_favorites（商品お気に入り）
9. posts（掲示板投稿 - トレード募集）
10. post_categories（掲示板カテゴリ）
11. post_likes（トレード投稿いいね）
12. comments（コメント）
13. inquiries（問い合わせ）


━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
テーブル定義
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

【1. users（会員）】

カラム名             型                  NULL    説明
--------------------------------------------------------------------------------
id                  INT UNSIGNED        NO      ユーザーID（主キー、自動採番）
email               VARCHAR(255)        NO      メールアドレス（ユニーク）
password            VARCHAR(255)        YES     パスワード（ハッシュ化）※ソーシャルログインの場合NULL
username            VARCHAR(100)        NO      ユーザー名
twitter_id          VARCHAR(255)        YES     X（Twitter）ID（ソーシャルログイン用）
twitter_token       VARCHAR(255)        YES     Xアクセストークン
is_active           TINYINT(1)          NO      アカウント有効フラグ（1:有効, 0:退会）
created_at          TIMESTAMP           NO      登録日時
updated_at          TIMESTAMP           NO      更新日時

インデックス：
- PRIMARY KEY (id)
- UNIQUE (email)
- INDEX (twitter_id)


【2. admins（管理者）】

カラム名             型                  NULL    説明
--------------------------------------------------------------------------------
id                  INT UNSIGNED        NO      管理者ID（主キー、自動採番）
username            VARCHAR(100)        NO      管理者名（ユニーク）
password            VARCHAR(255)        NO      パスワード（ハッシュ化）
created_at          TIMESTAMP           NO      登録日時
updated_at          TIMESTAMP           NO      更新日時

インデックス：
- PRIMARY KEY (id)
- UNIQUE (username)


【3. categories（商品カテゴリ）】

カラム名             型                  NULL    説明
--------------------------------------------------------------------------------
id                  INT UNSIGNED        NO      カテゴリID（主キー、自動採番）
name                VARCHAR(100)        NO      カテゴリ名
display_order       INT                 NO      表示順序
created_at          TIMESTAMP           NO      登録日時
updated_at          TIMESTAMP           NO      更新日時

インデックス：
- PRIMARY KEY (id)


【4. products（商品）】

カラム名             型                  NULL    説明
--------------------------------------------------------------------------------
id                  INT UNSIGNED        NO      商品ID（主キー、自動採番）
category_id         INT UNSIGNED        NO      カテゴリID（外部キー）
name                VARCHAR(255)        NO      商品名
description         TEXT                YES     商品説明
price               INT UNSIGNED        NO      価格
stock               INT UNSIGNED        NO      在庫数
image_path          VARCHAR(255)        YES     画像パス
is_active           TINYINT(1)          NO      公開フラグ（1:公開, 0:非公開）
created_at          TIMESTAMP           NO      登録日時
updated_at          TIMESTAMP           NO      更新日時

インデックス：
- PRIMARY KEY (id)
- FOREIGN KEY (category_id) REFERENCES categories(id)
- INDEX (category_id)
- INDEX (is_active)


【5. carts（カート）】

カラム名             型                  NULL    説明
--------------------------------------------------------------------------------
id                  INT UNSIGNED        NO      カートID（主キー、自動採番）
user_id             INT UNSIGNED        NO      ユーザーID（外部キー）
product_id          INT UNSIGNED        NO      商品ID（外部キー）
quantity            INT UNSIGNED        NO      数量
created_at          TIMESTAMP           NO      登録日時
updated_at          TIMESTAMP           NO      更新日時

インデックス：
- PRIMARY KEY (id)
- FOREIGN KEY (user_id) REFERENCES users(id)
- FOREIGN KEY (product_id) REFERENCES products(id)
- UNIQUE (user_id, product_id)


【6. orders（注文）】

カラム名             型                  NULL    説明
--------------------------------------------------------------------------------
id                  INT UNSIGNED        NO      注文ID（主キー、自動採番）
user_id             INT UNSIGNED        NO      ユーザーID（外部キー）
total_amount        INT UNSIGNED        NO      合計金額
status              VARCHAR(20)         NO      ステータス（pending/completed/cancelled）
created_at          TIMESTAMP           NO      注文日時
updated_at          TIMESTAMP           NO      更新日時

インデックス：
- PRIMARY KEY (id)
- FOREIGN KEY (user_id) REFERENCES users(id)
- INDEX (user_id)
- INDEX (status)


【7. order_items（注文明細）】

カラム名             型                  NULL    説明
--------------------------------------------------------------------------------
id                  INT UNSIGNED        NO      注文明細ID（主キー、自動採番）
order_id            INT UNSIGNED        NO      注文ID（外部キー）
product_id          INT UNSIGNED        NO      商品ID（外部キー）
quantity            INT UNSIGNED        NO      数量
price               INT UNSIGNED        NO      単価（注文時の価格）
created_at          TIMESTAMP           NO      登録日時

インデックス：
- PRIMARY KEY (id)
- FOREIGN KEY (order_id) REFERENCES orders(id)
- FOREIGN KEY (product_id) REFERENCES products(id)
- INDEX (order_id)


【8. product_favorites（商品お気に入り）】

カラム名             型                  NULL    説明
--------------------------------------------------------------------------------
id                  INT UNSIGNED        NO      ID（主キー、自動採番）
user_id             INT UNSIGNED        NO      ユーザーID（外部キー）
product_id          INT UNSIGNED        NO      商品ID（外部キー）
created_at          TIMESTAMP           NO      登録日時

インデックス：
- PRIMARY KEY (id)
- FOREIGN KEY (user_id) REFERENCES users(id)
- FOREIGN KEY (product_id) REFERENCES products(id)
- UNIQUE (user_id, product_id)


【9. post_categories（掲示板カテゴリ）】

カラム名             型                  NULL    説明
--------------------------------------------------------------------------------
id                  INT UNSIGNED        NO      カテゴリID（主キー、自動採番）
name                VARCHAR(100)        NO      カテゴリ名
display_order       INT                 NO      表示順序
created_at          TIMESTAMP           NO      登録日時
updated_at          TIMESTAMP           NO      更新日時

インデックス：
- PRIMARY KEY (id)


【10. posts（掲示板投稿 - トレード募集）】

カラム名             型                  NULL    説明
--------------------------------------------------------------------------------
id                  INT UNSIGNED        NO      投稿ID（主キー、自動採番）
user_id             INT UNSIGNED        NO      ユーザーID（外部キー）
category_id         INT UNSIGNED        NO      カテゴリID（外部キー）
title               VARCHAR(255)        NO      件名
content             TEXT                NO      本文
image_path          VARCHAR(255)        YES     画像パス
thumbnail_path      VARCHAR(255)        YES     サムネイル画像パス
created_at          TIMESTAMP           NO      投稿日時
updated_at          TIMESTAMP           NO      更新日時

インデックス：
- PRIMARY KEY (id)
- FOREIGN KEY (user_id) REFERENCES users(id)
- FOREIGN KEY (category_id) REFERENCES post_categories(id)
- INDEX (user_id)
- INDEX (category_id)
- INDEX (created_at)


【11. post_likes（トレード投稿いいね）】

カラム名             型                  NULL    説明
--------------------------------------------------------------------------------
id                  INT UNSIGNED        NO      ID（主キー、自動採番）
user_id             INT UNSIGNED        NO      ユーザーID（外部キー）
post_id             INT UNSIGNED        NO      投稿ID（外部キー）
created_at          TIMESTAMP           NO      登録日時

インデックス：
- PRIMARY KEY (id)
- FOREIGN KEY (user_id) REFERENCES users(id)
- FOREIGN KEY (post_id) REFERENCES posts(id)
- UNIQUE (user_id, post_id)


【12. comments（コメント）】

カラム名             型                  NULL    説明
--------------------------------------------------------------------------------
id                  INT UNSIGNED        NO      コメントID（主キー、自動採番）
post_id             INT UNSIGNED        NO      投稿ID（外部キー）
user_id             INT UNSIGNED        NO      ユーザーID（外部キー）
content             TEXT                NO      コメント内容
created_at          TIMESTAMP           NO      投稿日時
updated_at          TIMESTAMP           NO      更新日時

インデックス：
- PRIMARY KEY (id)
- FOREIGN KEY (post_id) REFERENCES posts(id)
- FOREIGN KEY (user_id) REFERENCES users(id)
- INDEX (post_id)


【13. inquiries（問い合わせ）】

カラム名             型                  NULL    説明
--------------------------------------------------------------------------------
id                  INT UNSIGNED        NO      問い合わせID（主キー、自動採番）
name                VARCHAR(100)        NO      名前
email               VARCHAR(255)        NO      メールアドレス
subject             VARCHAR(255)        NO      件名
message             TEXT                NO      問い合わせ内容
created_at          TIMESTAMP           NO      送信日時

インデックス：
- PRIMARY KEY (id)
- INDEX (created_at)
