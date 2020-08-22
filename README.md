# アプリケーション情報
アプリケーション概要
フリーマーケットのアプリケーションを作成しました。
接続先情報
http://18.176.184.85
ID/Pass
ID: admin
Pass: admin9999
テスト用アカウント等
購入者用
メールアドレス:buy@buy.com
パスワード: buybuy
購入用カード情報
番号：4242424242424242
期限：12月20年
セキュリティコード：123
出品者用
メールアドレス名: sell@sell.com
パスワード: sellsell
Githubリポジトリ
https://github.com/xxxxxx/freemarket_sample_40a

# 開発状況
開発環境
Ruby/Ruby on Rails/MySQL/Github/AWS/Visual Studio Code
開発期間と平均作業時間
開発期間：約4週間
1日あたりの平均作業時間：約9時間
開発体制
人数：4名
アジャイル型開発（スクラム）
Trelloによるタスク管理

# 動作確認方法
Chromeの最新版を利用してアクセスしてください。
ただしデプロイ等で接続できないタイミングもございます。その際は少し時間をおいてから接続してください。
接続先およびログイン情報については、上記の通りです。
同時に複数の方がログインしている場合に、ログインできない可能性があります。
出品方法は以下の手順で確認できます
テストアカウントでログイン→トップページから出品ボタン押下→商品情報入力→商品出品
購入方法は以下の手順で確認できます
テストアカウントでログイン→トップページから商品検索→商品選択→商品購入

確認後、ログアウト処理をお願いします。



# フリマアプリ DB設計
## Usersテーブル
|Column|Type|Options|
|------|----|-------|
|nickname|string|null: false|
|email|string|null: false, unique: true|
|password|string|null: false|
### Association
- has_one :profile
- has_one :address
- has_many :products
## Profileテーブル
|Column|Type|Options|
|------|----|-------|
|user|references|null: false,foreign_key: true|
|first_name|string|null: false|
|last_name|string|null: false|
|first_name_kana|string|null: false|
|last_name_kana|string|null: false|
|birth_year|integer|null: false|
|birth_month|integer|null: false|
|birth_date|integer|null: false|
### Association
- belongs_to :user

## Addressテーブル
|Column|Type|Options|
|------|----|-------|
|user|references|null: false, foreign_key: true|
|first_name|string|null: false|
|last_name|string|null: false|
|first_name_kana|string|null: false|
|last_name_kana|string|null: false|
|zip_code|integer(7)|null: false|
|prefecture|integer|null: false|
|city|string|null: false|
|street_number|string|null: false|
|apartment|string||
|telephone|integer||
### Association
- belongs_to :user
## Productsテーブル
|Column|Type|Options|
|------|----|-------|
|user|references|null: false, foreign_key: true|
|name|string|null: false|
|introduction|text|null: false|
|category|references|null: false, foreign_key: true|
|brand|references|null: false, foreign_key: true|
|product_condition|references|null: false, foreign_key: true|
|shipping_payer|references|null: false, foreign_key: true|
|shipping_region|references|null: false, foreign_key: true|
|preparation_term|references|null: false, foreign_key: true|
|price|integer|null: false|
### Association
- belongs_to :user
- has_many :images
- belongs_to :category
- belongs_to :brand
- belongs_to :product_condition
- belongs_to :preparation_term
- belongs_to :shipping_region
- belongs_to :shipping_payer
## imageテーブル
|Column|Type|Options|
|------|----|-------|
|image|string|null: false|
|product|references|null: false, foreign_key: true|
### Association
- belongs_to :products
## categoryテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|
|ancestry|string|
### Association
- has_many :products
## brandテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
### Association
- has_many :products
## product_conditionテーブル
|Column|Type|Options|
|------|----|-------|
|condition|integer|null:false|
### Association
- has_many :products
### Condition
1:新品、未使用
2:未使用に近い
3:目立った傷た汚れなし
4:やや傷や汚れあり
5:傷や汚れあり
6:全体的に状態が悪い
## preparation_termテーブル
|Column|Type|Options|
|------|----|-------|
|term|integer|null:false|
### Association
- has_many :products
### term
1:1-2日
2:2-3日
3:4-7日
## shipping_regionテーブル
|Column|Type|Options|
|------|----|-------|
|region|integer|null:false|
### Association
- has_many :products
## shipping_payerテーブル
|Column|Type|Options|
|------|----|-------|
|buyer|integer|null:false|
|seller|integer|null:false|
### Association
- has_many :products
