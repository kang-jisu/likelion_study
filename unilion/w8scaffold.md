 ## Ruby on rails
 > scaffold_app

 ### W8

 * scaffold 생성
	* `rails g scaffold Note title:string content:text`
	* '발판'이라는 뜻

 * scaffold 기능 확인
 > rake db:migate 
 > 서버를 실행시켜 /notes로 들어가보면 기존에 배웠던 CRUD 기능이 구현된 게시판이 생성되어있음.

 #### 기존이랑 다른점
 * link_to 
 * _form.html.erb 
	* 중복되는 코드 하나로 사용할 수 있게 해줌
 * route.rb 에 라우팅 했던 것들 `resources :notes` 로 해놓으면 바로 됨
	* ex ` get, post, patch, delete '/notes/:id' => 'notes# ..' `
 
 --- 
 
 ### 새로 만들어보기 
 ` rails g model Article title:string content:text `
 ` rake db:migrate ` 