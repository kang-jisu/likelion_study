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
 * link_to 
 * _form.html.erb 
	* �ߺ��Ǵ� �ڵ� �ϳ��� ����� �� �ְ� ����
 * route.rb �� ����� �ߴ� �͵� `resources :notes` �� �س����� �ٷ� ��
	* ex ` get, post, patch, delete '/notes/:id' => 'notes# ..' `
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
	```ruby
	private # �ٸ����� �� �� ����, end�� �����°Ծƴϰ� private �ؿ��� ���� privateó�� ������ public(����)
 	 def set_article
	  @article = Article.find(params[:id])
	 end
	
	```
	* �� ���� ������
	   ```ruby
	   before_action :set_article, only: [:show, :edit, :update, :destroy] 
	   ```
 8. create �׼� 
	```ruby
	def create  
		@article = Article.new
		@article.title = params[:input_title]
		@article.content = params[:input_content]
		@article.save
		redirect_to articles_url #redirect_to '/Articles' ��� resoucresó������ ��������� ���ִ� '������ ����'
	end
	```