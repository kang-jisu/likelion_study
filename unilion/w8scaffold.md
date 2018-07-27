 ## Ruby on rails &#128513;
 > scaffold_app

 ### W8

 * scaffold ����
	* `rails g scaffold Note title:string content:text`
	* '����'�̶�� ��
	* rails�� ���� => " DRY don't repeat yourself "

 * scaffold ��� Ȯ��
	* rake db:migate 
	* ������ ������� /notes�� ������ ������ ����� CRUD ����� ������ �Խ����� �����Ǿ�����.

 #### �����̶� �ٸ���
 * &#10003; link_to 
 * &#10003; _form.html.erb 
	* &#10033; �ߺ��Ǵ� �ڵ� �ϳ��� ����� �� �ְ� ����
 * &#10003; route.rb �� ����� �ߴ� �͵� `resources :notes` �� �س����� �ٷ� ��
	* &#10033; ex ` get, post, patch, delete '/notes/:id' => 'notes# ..' `
	* `$ rake routes ` �ϸ� ����� Ȯ�� ���� 
 --- 
 
 ### scaffold ��� ó�� ���� ������ 
 1. ` rails g model Article title:string content:text `
 2. ` rake db:migrate ` 
 3. ` rails g controller Articles new show edit index `
 4. routes.rb�� article ������� ����� `resources :articles `�� �ٲٱ�
 5.  article ��Ʈ�ѷ��� create, update, destroy �׼ǵ� �߰����ֱ�
 6. `@article = Article.find(params[:id])` �� �ʿ��ߴ� �׼���?
	* show, edit, update, destroy
	* index�� `@articles = Article.all `
 7. DRY����!
	* set_article action ����� �� �ڵ� ���°� �� ����
	```
	private 
 	 def set_article
	  @article = Article.find(params[:id])
	 end
	end
	
	```
	* �� ���� ������
   ` before_action :set_article, only: [:show, :edit, :update, :destroy] `
   
 