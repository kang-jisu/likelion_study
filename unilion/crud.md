## Ruby on rails 

 > CRUD 

 ### W5

 * ���� ������Ѽ� db������
 - gemfile�� gem 'rails_db' ����
 - bundle install

 * ��Ʈ�ѷ����� id�� �޾ƿö�
 - @note = Note.find params[:id]

 ---

 ### W6

 * Http method 4����
	* get (view)
	* post (create)
	* put&patch (update)
	* delete (delete)

 * post 
 - ���� create��
 - form �±� method='POST'�� �ٲ���
 - ��Ʈ�ѷ� new�� 
 ` @token = form_authenticity_token `
 - �信 
 ` <input type="hidden" name='authenticity_token' value="<%=@token %>"> `

 * delete
 - data-method='delete'�� �ٲ��ְ� ����� (��������� ����)

 * update
 - `<input type="hidden" name="_method" value="patch">`

 
