 ## Ruby on rails
 > model_Association

 ### W7

 owner - item

 * migrate���� item (�����ִ°� 3���� �ϳ� �ƹ��ų� ����)
 	* t.integer :owner_id
 	* t.reference :owner
 	* t.belongs_to :owner

 * model - rb����
 	* Item : belongs_to :owner
 	* has_many :items

 * `rails g model Hobby name:string owner:belongs_to`
 * �̷������� �ϸ� �ڵ����� hobby 1:n���� ��Ÿ���°͵� ��������


