 ## Ruby on rails
 > scaffold_app

 ### W8

 * scaffold ����
	* `rails g scaffold Note title:string content:text`
	* '����'�̶�� ��

 * scaffold ��� Ȯ��
 > rake db:migate 
 > ������ ������� /notes�� ������ ������ ����� CRUD ����� ������ �Խ����� �����Ǿ�����.

 #### �����̶� �ٸ���
 * link_to 
 * _form.html.erb 
	* �ߺ��Ǵ� �ڵ� �ϳ��� ����� �� �ְ� ����
 * route.rb �� ����� �ߴ� �͵� `resources :notes` �� �س����� �ٷ� ��
	* ex ` get, post, patch, delete '/notes/:id' => 'notes# ..' `
 
 --- 
 
 ### ���� ������ 
 ` rails g model Article title:string content:text `
 ` rake db:migrate ` 