## Ruby on rails 

 > CRUD 

 ### W5

 * 서버 실행시켜서 db보려면
 - gemfile에 gem 'rails_db' 수정
 - bundle install

 * 컨트롤러에서 id로 받아올때
 - @note = Note.find params[:id]

 ---

 ### W6

 * Http method 4가지
	* get (view)
	* post (create)
	* put&patch (update)
	* delete (delete)

 * post 
 - 순수 create용
 - form 태그 method='POST'로 바꿔줌
 - 컨트롤러 new에 
 ` @token = form_authenticity_token `
 - 뷰에 
 ` <input type="hidden" name='authenticity_token' value="<%=@token %>"> `

 * delete
 - data-method='delete'로 바꿔주고 라우팅 (레일즈에서만 가능)

 * update
 - `<input type="hidden" name="_method" value="patch">`

 
