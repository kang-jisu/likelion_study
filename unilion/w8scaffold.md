 ## Ruby on rails &#128513;
 > scaffold_app

 ### W8

 * scaffold 생성
	* `rails g scaffold Note title:string content:text`
	* '발판'이라는 뜻
	* rails의 원리 => " DRY don't repeat yourself "

 * scaffold 기능 확인
	* rake db:migate 
	* 서버를 실행시켜 /notes로 들어가보면 기존에 배웠던 CRUD 기능이 구현된 게시판이 생성되어있음.

 #### 기존이랑 다른점
 * &#10003; link_to 
 * &#10003; _form.html.erb 
	* &#10033; 중복되는 코드 하나로 사용할 수 있게 해줌
 * &#10003; route.rb 에 라우팅 했던 것들 `resources :notes` 로 해놓으면 바로 됨
	* &#10033; ex ` get, post, patch, delete '/notes/:id' => 'notes# ..' `
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
	```
	private 
 	 def set_article
	  @article = Article.find(params[:id])
	 end
	end
	
	```
	* 맨 위에 적어줌
   ` before_action :set_article, only: [:show, :edit, :update, :destroy] `
   
 