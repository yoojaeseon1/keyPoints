##### <script> �±׷� �ѷ��� ��ũ��Ʈ ����. 

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

---

##### �Ϲ������� <head> �±� �ȿ��� �ۼ��ϰ� <body> �±׿��� �ۼ��ص� �����ϴ�.

��ġ

1. ���� : <head>���� �Ǵ� <body>���ǿ��� �ۼ�

2. �ܺ� : �Ϲ������� <head>���ǿ� �ۼ��ϰ� �ܺ� ������ ��ũ��Ʈ�� ����� �� �ִ�.
	  ex) <script src="myscript.js"></script>

3. �ζ��� : HTML �±� ���ο� �̺�Ʈ �Ӽ����� �����Ѵ�.
	    ex) onclick�Ӽ� :    <button type="button" onclick="alert('�ݰ����ϴ�.')">��ư�� ��������!</button>


##### JSP���� ���� ������ �� �������� F12�� ���� Console���� Ȯ������(STS�� �ܼ�â������ view���Ͽ��� �߻��� ������ Ȯ���� �� ����.)

##### console

###### console.log

	var a = 1;
	var b = "hello";
	var c = true;

	console.log(a); // �ϳ��� �α�
	
	console.log(a,b,c); // ���� �� ���ÿ� �α�
	
	console.log("idx : ", idx) // �ؽ�Ʈ�� ���� ���� ���
	
	console.log("idx : ", idx, ", val : ", val); // ���� �ؽ�Ʈ/���� ���� ���
	
	console.log("${a}�� ����, ${b}�� ���ڿ�"); // ������ �ؽ�Ʈ ���� ���(�ȵǴµ�?)
	
* ���� ����

��ü�� ��������� �ǽð����� �ݿ��ȴ�.


###### console.dir

��ü�� �α��� ��� �ʵ� ���� �����ؼ� ����Ѵ�.

��ü�� dir, �������� log�� �α��ϸ� ���ϴ�.

###### console.count

����̳� ī��Ʈ�Ǿ����� Ȯ���ϰ� ���� �� ����Ѵ�.

	console.count('ī����1'); // ī����1: 1
	console.count('ī����1'); // ī����1: 2
	console.count('ī����2'); // ī����2: 1
	console.count('ī����2'); // ī����2: 2
	console.count('ī����1'); // ī����1: 3

###### console.time, console.timeEnd

�ڵ��� ����ð��� Ȯ���� �� ����Ѵ�.

	console.time('Ÿ�̸�');
	for (var i = 0; i < 1000000; i++) z = 5;
	console.timeEnd('Ÿ�̸�'); // Ÿ�̸�: 6.76611328125ms


##### JQuery(JavaScript�� ���ϰ� �������� ���̺귯��, �Ȱ��� <script>�±� �ȿ��� �ۼ��Ѵ�.)

###### �� �������� ���

Ŭ���� : $(".�ش�class");

���̵� : $("#�ش�id");

�̸� : $('[name="�ش�name"]');

����(role) : $("form[role='�ش�role']");

###### JQuery�� ����� view���� JSON��ü�� �޴� ���(getJSON(uri,function(data)) �޼ҵ� ���)

$.getJSON("/replies/all/" + bno, function(data) {

	console.log(data.length);	

});

view�̸��� test��� path�� /test�� �������� �� /replies/all/�ش�bno�� �����ؼ� �����͸� �����´ٴ� �ǹ̴�.


##### document.

write(text) : text�� ���������� ����.

getElementById(id) : id�� id�� ��Ҹ� �����´�.


-----

alert(text) : text�� �޼����� �ϴ� ���â�� ȭ�鿡 ���

confirm(text) : text�� �޼����� �ϴ� â�� ��� Ȯ�� / ��Ҹ� ���� �� �ְ� true / false�� ��ȯ�Ѵ�.

-----

prompt(text, defaultText) : dialbox�� ����. ����ڰ� �Է��� �ؽ�Ʈ�� ��ȯ�Ѵ�.

text : �Է�ĭ ���� �ȳ� �޼���

defautText(����) : �Է�ĭ�� �ʱ� �޼��� ���

-----

���(Elements) : 

HTML���� ���� �±׿� �����±׷� �̷���� ��� ��ɾ���� �ǹ��մϴ�.

�±�(Tag) : 

���(Elements)�� �Ϻη� ���� �±׿� ���� �±� �� ������ �ֽ��ϴ�.

�Ӽ�(Attributes) : 

����� ���� �±� �ȿ��� ���Ǵ� ������ �� �� ��üȭ�� ��ɾ� ü�踦 �ǹ��մϴ�.

section : http://webdir.tistory.com/310

------

for/in loop

for(���� in ��ü) {} : ������ ��ü�� ��� �Ӽ��� �ϳ��� ���ԵǸ鼭 �ݺ��Ѵ�.


------

self.location = "path";

: �ش� path�� redirection �Ѵ�.

------


##### JSTL

<C:ooo> �±׸� ����ϴ� ���̺귯��

ex) 

<c:forEach></c:forEach> : <c:forEach items="${list}" var="boardVO"> �Ǵ� <c:forEach begin="startNum" end="endNum"></c:forEach>


<c:if></c:if> : <c:if test="���ǹ�"> true�ϰ�� ���� </c:if>

<c:out></c:out> : <c:out value="����� ��(3�� ������ ��밡��)"></c:out>

-----

�޼��� ����

var methodName = function(params) {

	// executed statement

}

�޼��带 �����ϱ� ���ؼ��� ���� ���� �����ؾ� �Ѵ�.


-----

modal : ������� �Է��� �����ϴ� UI(�˾�â)

modality : modal�� Ư��


-----


DOM(Document Object Model) : Java Script�� ����� �۾��� �̷������ ���. Java Script�� �ϴ� �۾� = DOM API

ex)

// view code

<div id="container"></div>

// Java Script code

<script>
  var container = document.getElementById("container");
  container.innerHTML = "New Content!";
</script>


// �������� ���� ��

<div id="container">New Content!</div>  // �̰� DOM

���� view������ �ڵ�ʹ� �ٸ���.



-----

parent.�޼ҵ��

: ���� �������� ���� �ٷ� �� ������(jsp����)�� ���ǵǾ� �ִ� �޼ҵ带 ȣ���Ѵ�.


-----

<script> �±��� ������ ��ġ


�ܼ� java script : <body> ���ϴ�

jQuery : <head>

CSS : <head>

������ ã�Ƽ� Ȯ������


-----
js ���� ���� ���(java script�� �ҽ��� ����� �ִ� ����)

new > Java Script Source File ����


-----

js �Ǵ� css������ �� ���������� �ٷιٷ� ������� ���� ��

<script>�� �Է��ϴ� ����� �������� "?ver=1"�� �߰����ش�.(���ڴ� �ƹ��ų� �ص� ��� ����.)

�������� ���� ĳ���� �ִ� ���ϰ� �ٸ� ���Ϸ� �ν��ؼ� ������ ������ �ٷ� ����ȴ�.

ex)

<script type="text/javascript" src="/resources/js/upload.js?ver=1"></script>

�׷��� �ȵ� ���

\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp1\work\Catalina\localhost\ROOT\org\apache\jsp\WEB_002dINF\views

views �����ȿ� �ִ� ���� ������ ��� �����Ѵ�.

-----

$(document).ready(function{

// �� �ȿ� �ۼ��ϴ� ������ ó�� �������� �̵����� ���� ����ǰ�

click ���� �̺�Ʈ�� �߻����� �� ����Ǵ� ������ ������� �ʴ´�.

});

�ٵ� �� ���� �ֳ�..?(�ȵ� ���� ���� ������...)

-----

event.preventDefault();

: �ش� �̺�Ʈ(ex) Ŭ��)�� ���� �� default�� �����Ǿ� �ִ� ���� ������ ������� �ʵ��� ���ش�.

ex) �̹��� Ŭ�� : �������� �̵��Ͽ� �ش� �̹����� Ȯ���ؼ� �����ش�.

-----