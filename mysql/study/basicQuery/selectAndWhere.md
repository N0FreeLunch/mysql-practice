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
- 동일한 명칭의 용어가 존재하므로 멤버 테이블의 멤버는 회원이라고 부르고, 걸그룹의 멤버는 멤버라고 부르도록 한다.
- 용어의 혼동을 방지하기 위해 `mem_number`,  `mem_name`은 멤버수와 회원명이라고 부르도록 하자.

#### 멤버 수가 4명인 회원을 조회하라
```
select * from member where mem_number = 4;
```

#### 회원의 멤버 평균 키가 162cm보다 작거나 같은 걸그룹을 조회하라
```
select * from member where height <= 162;
```

#### 회원의 멤버 평균 키가 162 센티 보다 작거나 같은 회원의 멤버 수와 회원명을 조회하라
```
select mem_number, mem_name from member where height <= 162;
```

#### 회원이 사는 지역이 경기, 전남, 경남인 멤버의 회원명과 이름을 조회하라.
```
select mem_name, addr from member where addr = '경기' or addr = '전남' or addr = '전남';
```
```
select mem_name, addr from member where addr in ('경기', '전남', '전남');
```

#### 회원명에 '핑크'가 들어가는 대상을 조회하여라
```
select * from member where mem_name like '%핑크%';
```
