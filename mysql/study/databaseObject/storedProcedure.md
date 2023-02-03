## 스토어드 프로시저
- 데이터베이스가 제공하는 구문에 따라 마치 프로그래밍과 비슷하게 쿼리 처리를 할 수 있는 기능을 제공한다. 물론 일반적인 프로그래밍에 비해 할 수 있는 기능이 제한되어 있다.

## 스토어드 프로시저를 쿼리로 만들어 보기
```
// DELIMITER
CREATE PROCEDURE myProc()
BEGINE
    SELECT * FROM member WHERE memeber_name = '나훈아';
    SELECT * FROM product WHERE product_name = '삼각김밥';
END //
DELIMITER;
```
- `// DELIMITER` ... `DELIMITE;`는 저장 프로시저를 묶어주는 약속이다.
- `CREATE PROCEDURE 함수명()` 프로시저 함수를 만들어 주는 명령어를 적는다. `BEGINE`과 `END //`는 함수의 스코프를 의미한다고 보면된다.
- 저장 프로시저를 호출하는 명령은 `CALL 포로시져_함수명();`

## 스토어드 프로시져를 dbeaver로 만들기
- `Database Navigator`에서 만든 데이터베이스를 선택한다. 여기서는 `shop_db`이다. 하위의 `Procedures` 항목을 오른쪽 클릭해서 `Create New Procedure`를 클릭한다.
- 창이 하나 나타나는데 `myProc`로 입력하자. 프로시져의 함수명을 지정한다.
- 오른쪽 하단의 `Source` 탭으로 이동해서 `BEGINE`과 `END` 사이에
```
    SELECT * FROM member WHERE member_name = '나훈아';
    SELECT * FROM product WHERE product_name = '삼각김밥';
```
- 위 쿼리를 입력하도록 하자. 그리고 저장 버튼을 누른 후 프로시져를 만드는 쿼리 문이 뜨면 확인 후 `Persist` 버튼을 눌러서 프로시져를 만든다.
- 기본 쿼리 창으로 가서 `CALL myProc();`를 실행시켜 보자. 이 때 프로시저를 만들 때 입력한 쿼리가 잘못되었다면 에러가 발생한다. 프로시저를 만들 때 에러가 나는 것이 아니므로 주의해야 한다.
- 두 개의 쿼리가 실행되어 오른쪽 하단에 각각의 실행 쿼리의 결과에 대응하는 테이블이 2개가 생성된다.