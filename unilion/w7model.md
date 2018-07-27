 ## Ruby on rails
 > model_Association

 ### W7

 owner - item

 * migrate파일 item (속해있는거 3개중 하나 아무거나 가능)
 	* t.integer :owner_id
 	* t.reference :owner
 	* t.belongs_to :owner

 * model - rb파일
 	* Item : belongs_to :owner
 	* has_many :items

 * `rails g model Hobby name:string owner:belongs_to`
 * 이런식으로 하면 자동으로 hobby 1:n관계 나타내는것들 생성해줌


