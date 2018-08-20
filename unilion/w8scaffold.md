 # Ruby on rails &#128513;
 > scaffold_app

 ## W8 -1

 * scaffold 생성
	* `rails g scaffold Note title:string content:text`
	* '발판'이라는 뜻
	* rails의 원리 => " DRY don't repeat yourself "

 * scaffold 기능 확인
	* rake db:migate 
	* 서버를 실행시켜 /notes로 들어가보면 기존에 배웠던 CRUD 기능이 구현된 게시판이 생성되어있음.

	
 #### 기존이랑 다른점
 * link_to 
 * _form.html.erb 
	* 중복되는 코드 하나로 사용할 수 있게 해줌
 * route.rb 에 라우팅 했던 것들 `resources :notes` 로 해놓으면 바로 됨
	* ex ` get, post, patch, delete '/notes/:id' => 'notes# ..' `
	* `$ rake routes ` 하면 라우팅 확인 가능 
 --- 
 
 ### scaffold 기능 처럼 새로 만들어보기 
 1. ` rails g model Article title:string content:text `
 2. ` rake db:migrate ` 
 3. ` rails g controller Articles new show edit index `
 4. routes.rb에 article 라우팅을 지우고 `resources :articles `로 바꾸기
 5.  article 컨트롤러에 create, update, destroy 액션도 추가해주기
 6. `@article = Article.find(params[:id])` 가 필요했던 액션은?
	* show, edit, update, destroy
	* index는 `@articles = Article.all `
 7. DRY원리!
	* set_article action 만들고 이 코드 쓰는거 다 지움
	```ruby
	private # 다른데서 쓸 수 없게, end로 끝내는게아니고 private 밑에는 전부 private처리 위에는 public(생략)
 	 def set_article
	  @article = Article.find(params[:id])
	 end
	
	```
	* 맨 위에 적어줌
	 ```ruby
	 before_action :set_article, only: [:show, :edit, :update, :destroy] 
	 ```
 8. create 액션 
	```ruby
	def create  
		@article = Article.new
		@article.title = params[:title]
		@article.content = params[:content]
		@article.save
		redirect_to articles_url #redirect_to '/Articles' 대신 resoucres처리해준 라우팅으로 해주는 '레일즈 헬퍼'
	end
	```

 ---
 
 ## W8-2
 
 ### params & form 태그
	
 * gemfile에 `gem 'pry-rails` -> 진화한 rails console
 * new.html.erb에 input 태그 name을 article[]로 수정
	```ruby
	 <input type="text" name="article[title]">
     <input type="text" name="article[content]">
	```
		* 이렇게하면 params를 했을때 "article" => { "title", "content"} 로 묶이게됨
		* params.require(:article) 하면 이 묶인거만 가져올수있음.
		* params.require(:article).permit(:title, :content) 하면 title,content만 넣을 수 있게 할 수 있음.
 * private 액션 추가로 생성 
	```ruby
	def artile_params
		params.require(:article).permit(:title, :content)
	end
	```
	
	
 참고 
 > `$ rails c --sandbox ` 하면 콘솔창에서하는거 반영안되게 콘솔 사용할수있음
	
 * create 컨트롤러 변경
	```ruby
	 def create  
		@article = Article.new(article_params)
		@article.save
		#redirect_to articles_url(@article.id) # "artuckes/#{@article.id}"
		#redirect_to article_url(@article)다 같은말
		redirect_to @article
	 end
	```
	
 ---
 
 ## W8-3 
 
 ### view helper : form_for
 - 레일즈에서 지원
 - html 코드 복잡한거 바로 해줌 ex) 토큰 label 
 - 사용법
	- new controller에 `@article = Article.new `
	```ruby
	<%= form_for(@article) do |f| %> <!-- article을 위해 존재하는 form태그-->
    <%= f.label :title %>
    <%= f.text_field :title%>
    
    <%= f.label :content %>
    <%= f.text_field :content %>
    
    <%= f.submit %>
	<% end %>
	```
	- 다른 속성 줄땐 ,로 구분해서 사용 ex)  `<%= f.text_field :title , placeholder: '제목 입력', class: 'hack' %>`
	- `<%= f.sumbit value: '제출' %>` submit은 컴마 말고 그냥 value