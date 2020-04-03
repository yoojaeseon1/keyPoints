##### LIMIT

SELECT 문을 통해 나오는 튜플의 개수를 제한한다.

ex)

	SELECT * FROM reviewimages ORDER BY reviewIndex DESC LIMIT 10;
	
나오는 결과 값에서 처음부터 10개의 튜플만 반환한다.

	SELECT * FROM reviewimages ORDER BY reviewIndex DESC LIMIT 3, 10;
	
나오는 결과 값에서 4(3+1)번째부터 10개의 튜플을 반환한다.

---

