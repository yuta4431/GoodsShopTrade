━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
技術スタック
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

■ プロジェクト名

GoodsShop&Trade


━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
使用技術
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

【バックエンド】

言語
・PHP 8.2

データベース
・MySQL 8.0

アーキテクチャ
・MVC（Model-View-Controller）

データベース操作
・PDO（PHP Data Objects）
・プリペアドステートメント

名前空間管理
・PHP Namespace


【フロントエンド】

マークアップ
・HTML5
・CSS3

JavaScript
・JavaScript (ES6+)
・jQuery

UIフレームワーク
・Bootstrap（レスポンシブ対応）

非同期通信
・Ajax（XMLHttpRequest / Fetch API）


【開発環境・インフラ】

コンテナ
・Docker
・Docker Compose

オーケストレーション
・Kubernetes (k8s)

Webサーバー
・Apache 2.4

バージョン管理
・Git
・GitHub


【外部API・サービス】

ソーシャルログイン・SNS連携
・X (旧Twitter) API
  - OAuth認証（ソーシャルログイン）
  - 投稿連携（トレード募集投稿の共有）

メール送信
・PHPMailer または SMTP


【セキュリティ対策】

・XSS対策（htmlspecialchars等によるエスケープ処理）
・CSRF対策（トークン検証）
・SQLインジェクション対策（PDO、プリペアドステートメント）
・パスワードハッシュ化（password_hash / password_verify）
・reCAPTCHA v3（ボット対策）
・Basic認証（管理画面アクセス制限）


【開発ツール】

エディタ
・Visual Studio Code

ターミナル
・macOS Terminal

データベース管理
・phpMyAdmin

テストデータ生成
・https://testdata.userlocal.jp/


━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
技術選定理由
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

【PHP】
・学習コストが低く、Web開発に特化した言語
・MVCアーキテクチャの実装に適している
・Laravel移植を見据えた学習基盤

【MySQL】
・リレーショナルデータベースとして広く採用されている
・PHPとの親和性が高い
・EC・掲示板のような複雑なデータ構造に適している

【Docker】
・環境構築の再現性が高い
・チーム開発を想定した環境共有が容易
・本番環境との差異を最小化

【MVC】
・責務分離による保守性向上
・PHPとHTMLの完全分離
・Laravelへの移植を見据えた設計

【X API】
・ソーシャルログインによるユーザー登録の簡略化
・トレード募集投稿をXで共有し、サービスの認知度向上
