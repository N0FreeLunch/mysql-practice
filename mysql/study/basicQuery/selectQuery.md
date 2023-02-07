## 조건을 포함한 조회
```
select * from member where mem_name = '블랙핑크';
```

## 지정한 열들을 조회
```
select height, debut_date, addr from member;
```

## 열 이름에 별칭 부여하기
```
select height 키, debut_date 데뷔_날짜, addr 주소 from member;
```
- 주의 : 별칭에 띄어쓰기를 쓸 수는 없다.

## Question
### 전제
- 멤버 테이블의 하나의 레코드인 멤버는 하나의 걸그룹을 의미한다.
- 걸그룹을 구성하는 각각의 멤버는 멤버 테이블의 멤버와는 다른 개념이다.
- 동일한 명칭의 용어가 존재하므로 멤버 테이블의 멤버는 걸그룹이라고 부르고, 걸그룹의 멤버는 멤버라고 부르도록 한다.
- 용어의 혼동을 방지하기 위해 `mem_number`,  `mem_name`은 걸그룹 넘버와 걸그룹 이름이라고 부른다.

#### 걸그룹의 멤버 수가 4명인 걸그룹을 조회하라
```
select * from member where mem_number = 4;
```

#### 걸그룹의 멤버 평균키가 162cm보다 작거나 같은 걸그룹을 조회하라
```
select * from member where height <= 162;
```

#### 걸그룹의 멤버 평균 키가 162센티 보다 작거나 같은 회원의 걸그룹 넘버와 멤버 이름만 조회하라
```
select mem_number, mem_name from member where height <= 162;
```