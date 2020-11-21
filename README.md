# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...

# テーブル設計

## users テーブル

| Column        | Type    | Options     |
| ------------- | ------- | ----------- |
| name          | string  | null: false |
| email         | string  | null: false |
| password      | string  | null: false |
| genre         | string  | null: false |
| grade         | integer | null: false |
| class_number  | integer | null: false |
| student_number| integer | null: false |

### Association

- has_many :room_users
- has_many :rooms, through: room_users
- has_many :messages
- has_many :comments
- has_many :responses
- has_many :agrees, dependent: :destroy




## rooms テーブル

| Column | Type   | Options     |
| ------ | ------ | ----------- |
| name   | string | null: false |

### Association

- has_many :room_users
- has_many :users, through: room_users
- has_many :messages, dependent: :destroy


## room_users テーブル

| Column | Type       | Options                        |
| ------ | ---------- | ------------------------------ |
| user   | references | null: false, foreign_key: true |
| room   | references | null: false, foreign_key: true |

### Association

- belongs_to :room
- belongs_to :user


## messages テーブル

| Column  | Type       | Options                        |
| ------- | ---------- | ------------------------------ |
| content | string     | null: false                    |
| user    | references | null: false, foreign_key: true |
| room    | references | null: false, foreign_key: true |

### Association

- belongs_to :room
- belongs_to :user
- has_many :comments
- has_one_attached :image


## comments テーブル

| Column     | Type       | Options                        |
| ---------- | ---------- | ------------------------------ |
| text       | string     | null: false                    |
| user       | references | null: false, foreign_key: true |
| message    | references | null: false, foreign_key: true |

### Association

- belongs_to :message
- belongs_to :user
- has_many :agrees, dependent: :destroy
- has_many :responses, dependent: :destroy


## agrees テーブル

| Column     | Type       | Options                        |
| ---------- | ---------- | ------------------------------ |
| user       | references | null: false, foreign_key: true |
| comment    | references | null: false, foreign_key: true |

### Association

- belongs_to :user
- belongs_to :comment


## responses テーブル

| Column        | Type       | Options                        |
| ------------- | ---------- | ------------------------------ |
| response_text | string     | null: false                    |
| user          | references | null: false, foreign_key: true |
| comment       | references | null: false, foreign_key: true |

### Association

- belongs_to :comment
- belongs_to :user
