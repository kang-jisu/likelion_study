 # Ruby on rails &#128513;
 > scaffold, devies

 ## W9 -1

 #### 주석처리 팁
 - <%# TODO: ~~ %> 라고 해놓으면
 - 터미널 창에 `rake notes` 치면 어디에 뭐적어놨는지 나옴.


 #### view helper < link_to >

 * `<%= link_to '보여지는 말', '이동 경로' %>`

 * index.html.erb
 ```ruby
    <% @articles.each do |article| %>
    <tr>
        <td><%= article.title %></td>
        <td> <%= article.content %></td>
        <td> <%= link_to 'show', article_path(article) %></td> # "articles/#{article.id}"와 같긴함
        <td> <%= link_to 'Edit' , '#' %></td>
        <td> <%= link_to 'Destroy', article_path(article) , 
                method: :delete, data: {confirm: 'Are you sure?'} %> </td>
            
    </tr>
    <% end %>
	
	<%= link_to 'New Article' , new_article_path %>
 ```
 
 #### articles controller
 ```ruby
  def destroy
    @article.destroy
    redirect_to articles_path
  end
  ```
  ```ruby
  def update
    @article.update(article_params)
    @article.save
    
    redirect_to article_url(@article)
  end
  ```
  
 * edit, new에 똑같은 form들어가도 알아서 랜더링, 근데 똑같은코드 들어가는거 DRY위배!!
	* view/articles/_form.html.erb 만듦
	```ruby
	# _form.html.erb
	<%= form_for(article) do |f| %> <!-- article을 위해 존재하는 form태그-->
    <%= f.label :title %>
    <br>
    <%= f.text_field :title , placeholder: '제목을 입력하세요', class: 'hack' %>
    <br>
    <%= f.label :content %>
    <br>
    <%= f.text_area :content %>
    
    <%= f.submit value: '얍'%>
	<% end %>
	```
	* 그러고 원래 form 있던자리에 `<%= render 'form', article: @article %>`
				
				
 ---
 
 ## W9-2 devise <회원관리 기능>
 
 1. gemfile에 ` gem 'devise'` 수정 한 후 `bundle install`
 2. `rails g devise:insatll` 
 3. root_url을 만들어야해서 route.rb에 `root 'articles#index'` 추가
 4. 'user'라는 이름의 devise 모델 생성
 ```ruby
 rails g devise user
 ```
 
 * `  before_action :authenticate_user!` 이거 컨트롤러 맨 위에 입력하면 로그인해야 접속가능
 * 로그아웃할 때
 `<%= link_to 'logout', destroy_user_session_path, method: :delete %>`
 * 로그인 돼있을때만 로그아웃 창 뜨게 하려면
 ```ruby
 <% if user_signed_in? %>
 <p><%= link_to 'logout', destroy_user_session_path, method: :delete %></p>
 <% end %>
 ```
 
 ---
 
 ## W9-3 devise 2
 > user:articles를 1:n 관계로 설정 해 줄것.
 
 1. `rake db:drop`
 2. articles migration파일에 ` t.belongs_to :user `추가
 3. `rake db:migrate`
 4. /models/
	* article.rb 에 `belongs_to :user` `validates :user, presence: true`추가
	* user.rb에 `has_many :articles` 추가
 5. user_id넘겨주기_form
	* _form.html.erb에 `<%= f.hidden_field :user_id, value: current_user.id %>` 추가
	```ruby
	#articles.controller
	def article_params
      params.require(:article).permit(:title, :content, :user_id)
    end
	```
	
 참고
 > rails c 에서 `u = User.find 1` `u.articles` 하면 1:n관계 볼 수 있음
 
 #### edit/destroy가 그 글을 쓴 글쓴이에게만 보이게 하기
 ```ruby
 # index.html 바꿔줌
 <% if article.user ==current_user %>
    <td> <%= link_to 'Edit' , edit_article_path(article) %></td>
    <td> <%= link_to 'Destroy', article_path(article) , 
                method: :delete, data: {confirm: 'Are you sure?'} %> </td>
 <% end %>
 ```
 -> 근데 이러면 주소로는 들어갈 수 있음
 
 ```ruby
  # private에 만들고 controller에 edit, destroy 맨 처음에 check_user추가해줌
  def check_user
      if @article.user != current_user
        redirect_to root_url
      end
  end
 ```
 
 
 