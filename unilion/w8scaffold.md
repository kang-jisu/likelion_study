 # Ruby on rails &#128513;
 > scaffold_app

 ## W8 -1

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
		@article.title = params[:title]
		@article.content = params[:content]
		@article.save
		redirect_to articles_url #redirect_to '/Articles' ��� resoucresó������ ��������� ���ִ� '������ ����'
	end
	```

 ---
 
 ## W8-2
 
 ### params & form �±�
	
 * gemfile�� `gem 'pry-rails` -> ��ȭ�� rails console
 * new.html.erb�� input �±� name�� article[]�� ����
	```ruby
	 <input type="text" name="article[title]">
     <input type="text" name="article[content]">
	```
		* �̷����ϸ� params�� ������ "article" => { "title", "content"} �� ���̰Ե�
		* params.require(:article) �ϸ� �� ���ΰŸ� �����ü�����.
		* params.require(:article).permit(:title, :content) �ϸ� title,content�� ���� �� �ְ� �� �� ����.
 * private �׼� �߰��� ���� 
	```ruby
	def artile_params
		params.require(:article).permit(:title, :content)
	end
	```
	
	
 ���� 
 > `$ rails c --sandbox ` �ϸ� �ܼ�â�����ϴ°� �ݿ��ȵǰ� �ܼ� ����Ҽ�����
	
 * create ��Ʈ�ѷ� ����
	```ruby
	 def create  
		@article = Article.new(article_params)
		@article.save
		#redirect_to articles_url(@article.id) # "artuckes/#{@article.id}"
		#redirect_to article_url(@article)�� ������
		redirect_to @article
	 end
	```
	
 ---
 
 ## W8-3 
 
 ### view helper : form_for
 - ������� ����
 - html �ڵ� �����Ѱ� �ٷ� ���� ex) ��ū label 
 - ����
	- new controller�� `@article = Article.new `
	```ruby
	<%= form_for(@article) do |f| %> <!-- article�� ���� �����ϴ� form�±�-->
    <%= f.label :title %>
    <%= f.text_field :title%>
    
    <%= f.label :content %>
    <%= f.text_field :content %>
    
    <%= f.submit %>
	<% end %>
	```
	- �ٸ� �Ӽ� �ٶ� ,�� �����ؼ� ��� ex)  `<%= f.text_field :title , placeholder: '���� �Է�', class: 'hack' %>`
	- `<%= f.sumbit value: '����' %>` submit�� �ĸ� ���� �׳� value