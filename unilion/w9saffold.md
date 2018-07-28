 # Ruby on rails &#128513;
 > scaffold_4

 ## W9 -1

 #### 주석처리 팁
 - <%# TODO: ~~ %> 라고 해놓으면
 - 터미널 창에 `rake notes` 치면 어디에 뭐적어놨는지 나옴.


 ###view helper < link_to >

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
 
 * articles controller
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
	* 
	```ruby
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
				
 