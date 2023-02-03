## 뷰
- 테이블을 셀렉트하는 결과로 마치 테이블 처럼 사용할 수 있게 만든 대상
- 보통 뷰를 만들 때는 뷰 이름 뒤에 `_view`라고 붙여준다.

## 뷰를 만들어 보자
```
select * from member;
```
- 위 쿼리 문을 뷰로 만들어 보자.
- 창 왼쪽을 분할하고 있는 `Database Navigator`에서 `databases` 하단의 데이터베이스 `shop_db` 하단의 `Tables` 항목을 더블클릭한다.
- 오른쪽을 분할하고 있는 창의 상단 탭의 `properties`탭의 하단 창의 `Views` 항목을 클릭한다. 오른쪽의 텅 빈 영역에서 오른쪽 클릭을 하고 `Create New Views`를 선택한다.
- 또는 창 왼쪽을 분할하고 있는 `Database Navigator`에서 `databases` 하단의 데이터베이스 `shop_db` 하단의 `Tables` 아래의 `Views`항목을 오른쪽 클릭하거나 더블클릭해서 오른쪽 창의 `Views` 탭의 영역에서 오른쪽 클릭 해서 `Create New Views`를 선택한다.
- `Database Navigator` 영역의 `Views` 항목 하위에 `NewView`라는 대상이 생성되고 더블클릭 후 오른쪽 영역 하단 영역에서 `Source` 부분을 클릭한다. 이 부분에 위 쿼리를 적은 후 우하단의 `Save` 버튼을 누르면 `View`를 생성하는 쿼리를 보여주고 뷰를 만들 것인지 물어보는 창이 뜬다.
```
CREATE OR REPLACE VIEW shop_db.NewView
AS -- shop_db.NewView source
select * from member;
```
- 뷰의 이름을 `member_view`로 바꾸주기 위해 `Open Editor` 버튼을 누르고 `NewView` 부분을 바꾸준다.
- 그리고 이 쿼리를 실행하기 위해 쿼리 실행 버튼(주황색의 재생버튼 모양)을 클릭한다.
- 만약 쿼리가 실행되지 않는다면 다음과 같이 바꿔 주었는지 확인하자.
```
CREATE OR REPLACE VIEW shop_db.member_view
AS -- shop_db.NewView source
select * from shop_db.member;
```
- 쿼리로 실행한 경우에는 `Database Navigator`의 `Views`항목 하위에 뷰가 갱신되지 않기 때문에 해당 영역을 오른쪽 클릭해서 '새로고침'을 클릭 해 준다.
- `Open Editor` 버튼을 클릭하지 않고 만들기 위해서는 오른쪽 상단 `properties`탭 영역의 `View Name`부분에서 이름을 지정한다. 여기서는 `member_view`로 이름을 지어주고 하단의 `Source` 탭으로 가서 `Save` 버튼을 눌러준다. `persist`버튼을 눌러주면 에러가 발생하는데 쿼리문의 디비의 데이터베이스명을 지정하지 않아서 생기는 문제이다.
```
select * from shop_db.member
```
- 위의 쿼리로 변경하여 실행하자.

