# テーブル設計

## usersテーブル

| Column             | Type    | Options                   |
| ------------------ | ------- | ------------------------- |
| nickname           | string  | null: false               |
| email              | string  | null: false, unique: true |
| encrypted_password | string  | null: false               |
| first_name         | string  | null: false               |
| last_name          | string  | null: false               |
| first_name_reading | string  | null: false               |
| last_name_reading  | string  | null: false               |
| birthday           | date    | null: false               |

### Association
- has_many :items
- has_many :comments


## itemsテーブル

| Column           | Type       | Options                        |
| ---------------- | ---------- | ------------------------------ |
| title            | string     | null: false                    |
| description      | text       | null: false                    |
| category_id      | integer    | null: false                    |
| condition_id     | integer    | null: false                    |
| delivery_fee_id  | integer    | null: false                    |
| prefecture_id    | integer    | null: false                    |
| days_to_ship_id  | integer    | null: false                    |
| price            | integer    | null: false                    |
| user_id          | references | null: false, foreign_key: true |

### Association
- belongs_to :user
- has_many :comments
- has_one :order


## commentsテーブル

| Column  | Type       | Options                        |
| ------- | ---------- | ------------------------------ |
| text    | text       | null: false                    |
| user_id | references | null: false, foreign_key: true |
| item_id | references | null: false, foreign_key: true |

### Association
- belongs_to :user
- belongs_to :item


## ordersテーブル

| Column          | Type       | Options                        |
| --------------- | ---------- | ------------------------------ |
| item_id         | references | null: false, foreign_key: true |
| user_id         | references | null: false, foreign_key: true |

### Association
- belongs_to :item
- belongs_to :user
- has_one :address


## addressテーブル

| Column          | Type       | Options                        |
| --------------- | ---------- | ------------------------------ |
| postal_code     | string     | null: false                    |
| prefecture_id   | integer    | null: false                    |
| city            | string     | null: false                    |
| house_number    | string     | null: false                    |
| building_number | string     |                                |
| phone_number    | string     | null: false                    |
| order_id        | references | null: false, foreign_key: true |

### Association
- belongs_to :order