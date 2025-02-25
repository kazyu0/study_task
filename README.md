## users
id	       integer	PK	ユーザーID
name	     string	  NOT NULL	        ユーザー名
email	     string	  NOT NULL, UNIQUE	メールアドレス
password   string  	NOT NULL	        パスワード（bcrypt）
role	     string	  DEFAULT: "child"	ユーザーの役割 ("parent" or "child")
created_at datetime	NOT NULL	        作成日時
updated_at datetime	NOT NULL	        更新日時

has_many :tasks
has_many :submissions
has_one :relationship

## tasks
id	        integer	  PK	      宿題ID
title	      string  	NOT NULL  宿題のタイトル
description	text	           -	宿題の詳細
due_date	  date	    NOT NULL	締切日
user_id	    integer  	NOT NULL, foreign_key	担当の子供ID（users.id）
created_at	datetime	NOT NULL	作成日時
updated_at	datetime	NOT NULL	更新日時

belongs_to :user
has_many :submissions

## submissions
id	        integer	PK	提出状況ID
task_id	    integer	NOT NULL, foreign_key	宿題ID（tasks.id）
user_id	    integer	NOT NULL, foreign_key	提出した子供ID（users.id）
submitted	boolean	DEFAULT: false	提出済みかどうか
submitted_at	date	-	提出日（NULLなら未提出）
created_at	datetime	NOT NULL	作成日時
updated_at	datetime	NOT NULL	更新日時

belongs_to :user 
belongs_to :task

## relationships
id	        integer	  PK	  関係ID
parent_id	  integer	  NOT NULL, foreign_key	親のユーザーID（users.id）
child_id	  integer	  NOT NULL, foreign_key	子供のユーザーID（users.id）
created_at	datetime	NOT NULL	作成日時
updated_at	datetime	NOT NULL	更新日時

belongs_to :parent
belongs_to :child,