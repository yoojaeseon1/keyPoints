##### JQuery(JavaScript�� ���ϰ� �������� ���̺귯��, �Ȱ��� <script>�±� �ȿ��� �ۼ��Ѵ�.)

<script> �±׷� �ѷ��� ��ũ��Ʈ ����. 

jQuery ���̺귯���� �������� <script>�±׸� ���� ���ְ� �� �ؿ� �ڵ带 �ۼ��ϴ� <Script>�±׸� ����(�׷��� �Ѵ� �ν��Ѵ�.)

ex)

<head>
<script src="/resources/plugins/jQuery/jQuery-2.1.4.min.js"></script> // ���̺귯���� �������� �±׸� ���� �Է� ��
<script>
	var bno=10;
	
	$.getJSON("/replies/all/"+bno, function(data) {
		console.log(data.length);
	});
</script>								// �ڵ带 �ۼ��ϴ� �±� �Է�

�Ϲ������� <head> �±� �ȿ��� �ۼ��ϰ� <body> �±׿��� �ۼ��ص� �����ϴ�.

��ġ

1. ���� : <head>���� �Ǵ� <body>���ǿ��� �ۼ�

2. �ܺ� : �Ϲ������� <head>���ǿ� �ۼ��ϰ� �ܺ� ������ ��ũ��Ʈ�� ����� �� �ִ�.
	  ex) <script src="myscript.js"></script>

3. �ζ��� : HTML �±� ���ο� �̺�Ʈ �Ӽ����� �����Ѵ�.
	    ex) onclick�Ӽ� : <button type="button" onclick="alert('�ݰ����ϴ�.')">��ư�� ��������!</button>


-----

##### �� �������� ���

Ŭ���� : $(".�ش�class");

���̵� : $("#�ش�id");

�̸� : $('[name="�ش�name"]');

����(role) : $("form[role='�ش�role']");

-----

##### ���� ���̴� �޼���

###### $("#�ش�id").val();

 : �ش� id�� �Էµ� ��(input �±��� ��)�� �����´�.

ex)

var replyer = $("#newReplyWriter").val();


-----

###### $("#�ش�id").val(data);

 : ���̵� �ش�id�� ����� ���� data�� ���Ѵ�.

-----

###### $("#testId").html() 

: �ش� id�� ������ �±��� �ڽ��±��� ���� �����´�(�±� ����, �ڽ��±� ���� �ش� �±��� ���� ������ �� ���� �����´�.)

ex) <div class="test">haha</div>

console.log($(".test").html); // output : haha

<div>
   <button>test button</button>
</div>

console.log($(".test").html); // output : <button>test button</button>



$("#testId").html(html data) : �ش� id�� ������ �±��� ������ ������ ������ �ٲ۴�.


$("#testId").text() : �ش� id�� ������ �±��� ���� �����´�(�±� �����ϰ� �±� ���� ����) 

-----

.val()�� .text()�� ���� : val()�� ����ڰ� �Է��� input�±��� ���� ��������, text()�� �̹� �����Ǿ� �ִ� text�� ���� �����´�.


-----

$(class or id or name).on(event, selector, data);

event : Ȱ��ȭ �Ǵ� �̺�Ʈ(ex) "click")

select : ���� �� �±�

data : �̺�Ʈ�� ���� �� �� ���޵Ǵ� data(function(data)) �� ���� data�� ����� ���� ������ ���� ���� �ִ�.




-----


$(class or id or name).attr(tag's name)

�ش� �±��� ���� �����´�.


-----

##### JQuery�� ����� view���� JSON��ü�� �޴� ���(getJSON() �޼ҵ� ���)

$.getJSON("/replies/all/" + bno, function(data) {

	console.log(data.length);	

});

view�̸��� test��� path�� /test�� �������� �� /replies/all/�ش�bno�� �����ؼ� �����͸� �����´ٴ� �ǹ̴�.

-----

##### Ajax ���� ���� 

: jquery�� �񵿱� ���۹�� �� �Ѱ�($.ajax(), $.get(), $.post() �� 3������ �ִ�.)

headers���� content-Type(context-Type���� �򰥷Ⱦ���. ��������)

ex)

$.ajax({
type : 'post',
url : '/replies',
headers : {
	"Content-Type" : "application/json"
	"X-HTTP-Method-Override" : "POST"
},
dataType : 'text',
data : JSON.stringify({
	bno : bno,
	replyer : replyer,
	replyText : replytext
}),
success : function(result) {
	if(result == 'SUCCESS') {
		alert("��ϵǾ����ϴ�.")
	}
}
   }); // ajax end
});


data���� JSON�������� ���� ���� {VO��ü�� �ʵ� : ���� ��}���� �ؾ� �ȴ�.

-----


##### ajax �������

type : ���۹��

url : �Է��� url�� data�� ����

headers : ���� �� �𸣰ڴ�.

dataType : ������ �������� Ÿ��

data : �����ϰ��� �ϴ� ������

success : �������� �� ������ ����

processData

- �����͸� �Ϲ����� query string���� ��ȯ�� �������� ����

- �⺻�� : 'application / x-www-form-urlencoded'

- �ٸ� ������ �����͸� ������ ���� �ڵ� ��ȯ�ϰ� ���� ���� ��� false�� �����ϸ� �ȴ�.

contentType

- �⺻�� : 'application / x-wwwform-urlencoded'

- ������ ��� multipart/form-data ������� �����ϱ� ���� false�� �����ؾ� �Ѵ�.




-----

##### Ajax�� ������ �϶�

<sciprt>�±׸� <body>�±� �ȿ���

view���� �±׸� ��� �ۼ��ϰ� �Ʒ����� ���ش�.

-----

api : https://api.jquery.com/jquery.getjson/

$.getJSON(URL, function(data) {

			$(data.list).each(function() {
				str += "<li data-rno='"+this.rno+"' class='replyLi'>"
				+ this.rno+":"+this.replyText+
				"<button>MOD</button></li>";
			});
			
			$("#replies").html(str);

});

data : uri�� ���� ���� �� Controller���� mapping�Ǵ� �޼����� return ���� ���� �� �ִ�.

data.list : �������� Controller���� mapping�Ǵ� �޼����� ���� ���� map�ε� key������ list�� �־ �ٷ� ������ �ݺ����� ������ ���̴�.



-----

$.getJSON(URL, function(data)
$.each(data, fucntion(key,value))

�� ���� jQuery�� ù ��° ���ڿ��� ��ȯ�ϴ� �����͸� function�� ���ڷ� ���� �� �ִ�.
(���� ���ڸ� �־���� �ϴ� ���� �ƴ϶� ù ��° ���ڿ��� function�� ���ڷ� �˾Ƽ� �ν��Ѵ�.)


-----

$(document).ready(function(){
   
   executed statement

});


������Ʈ�� �����԰� ���ÿ� ����Ǵ� �κ�

Java Script��

window.onload = function(){

   executed statement

}

�� ������ ����� ������ window.onload���� document�� ���� ����ȴ�.(1.document > 2.window.onload)



-----

ex) 

that.parent("div").remove();


: that �� <small> �±׿��� ��� <small>�±� �ٱ���(�θ�)���� ���� ������ �ִ� <div>�±׸� ����� ����� �Ѵ�.


-----

##### jQuery�� ����ϴ� <script>�� <body> ���ϴܿ� �ۼ�����(<head>���� �ۼ��ϸ� �ν����� ���ϴ� ��찡 �ִ�.)

-----
$(".class b") : �ش� class���� ������ �±� ������ b �±�(id �Ǵ� class) 


$(".uploadedList li").each(function(index) {
			arr.push($(this)("data-src"))
		});

�� ��� class���� uploadedList�� �±� �ȿ� ����Ǿ� �ִ� li�±׿� ���� �����ϴ� �Լ���.

-----



