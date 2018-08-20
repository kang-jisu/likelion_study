

 ### 그냥 기록용~~ 대충씀
## w10 Bootstrap_setting

 rails g controller front_pages home help about contact
 gemfile에 gem 'bootstrap'
 gem 'jquery-rails'도 필요 (보통 이미 있음)

 <div class="container">

 asset-stylesheet-application.css 에 있는거는 주석처리 돼있지만 지우면안됨
 asset-javascript 도

 asset>stylesheet에 custom.scss 파일 새로 생성
 @import 'bootstrap';

 asset>javascript>application.js에
 ```
 //= require jquery3
 //= require jquery_ujs
 //= require turbolinks
 //= require popper
 //= require bootstrap-sprockets
 //= require_tree .
 ```
 
 bundle update
 
 ---
 
 fake gem 추가해야함
 gemfile에
 gem 'faker'
 gem 'pry-rails'
 
 <%= link_to "Sign up now!", "#" %>
 
 home.html.erb 전체 div로 묶고 class주며 꾸며볼것

 ```ruby
	<div class="jumbotron">
	<h1 class="display-4"> Welcome to the layout App</h1>

	<p class="lead"> This is the home page for the likelion 6th layout project</p>
	<hr class="my-4">

	<%= link_to "Sign up now!", "#" , class: 'btn btn-lg btn-primary', role: 'button'%>

	</div>
 ```
 
 help.html.erb about, contact도 일단 해놓기
 
 rails c 해서
 Faker::Lorem.paragraph 2
 그냥 있어보이는 문장 만들어내는 gem인듯??
 
 link_to 쓸때 만드는 사이트와 관련있는 링크는 link_to로
 아예 외부페이지는 href로 쓰는게 좋음 
 
 ---
 ## w10-3 Layout Header & Footer
 application.erb에
 
 ```ruby
   <header class="navbar navbar-dark bg-dark navbar-expand-lg fixed-top">
    <div class="container">
      <%= link_to "Layout App", root_path, id: 'logo' , class: 'navbar-brand' %>
      <!-- Toggle Button -->
      <button class="navbar-toggler"
              type="button"
              data-target="#navbarNav"
              data-toggle="collapse"
              aria-controls = "navbarNav"
              aria-label="Toggle navigation"
              aria-expaned="false">
        <span class="navbar-toggler-icon"></span>
      </button>
      
      <!--navbar-->
    </div>
  </header>
  <div class="container">
 ```
 
 nav.collapse.navbar-collapse#navbarNav 이런식으로 쓰고 텝누르면
 <nav class="collapse navbar-collapse" id="navbarNav"></nav> 이렇게 바뀜
 link_to 주고
 
 footer도
  
 전체코드보기
 ```ruby
 <body>
  
  <header class="navbar navbar-dark bg-dark navbar-expand-lg fixed-top">
    <div class="container">
      <%= link_to "Layout App", root_path, id: 'logo' , class: 'navbar-brand' %>
      <!-- Toggle Button -->
      <button class="navbar-toggler"
              type="button"
              data-target="#navbarNav"
              data-toggle="collapse"
              aria-controls = "navbarNav"
              aria-label="Toggle navigation"
              aria-expanded="false">
        <span class="navbar-toggler-icon"></span>
      </button>
      
      <!--navbar-->
        <nav class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav ml-auto">
            <li class="nav-item"><%=link_to 'Home', root_path, class: 'nav-link'%></li>
            <li class="nav-item"><%=link_to 'Help',front_pages_help_path, class: 'nav-link'%></li>
            <li class="nav-item"><%=link_to 'login', '#', class: 'nav-link'%></li>
          </ul>
          
        </nav>
        
        
    </div>
  </header>
  <div class="container">

<%= yield %>
    
  </div>
  
  <footer class="container">
    <hr class="my-1">
      <small>
        <a href="https://github.com/kang-jisu">Jisu's Github</a>
        <a href="https:/likelion.net">likelion Homepage</a>
      </small>
      
      <nav>
        <ul>
          <li><%= link_to 'About', front_pages_about_path %></li>
          <li><%= link_to 'Contactt', front_pages_contact_path %></li>
          <li><%= link_to 'Log in', '#'%></li>
        </ul>
      </nav>
  </footer>
</body>
 ```
 
 이제 custom.scss 꾸며볼것
