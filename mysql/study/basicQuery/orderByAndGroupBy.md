## ORDER BY
### syntax
```
select * from 테이블명 [조건문] order by 정렬할_컬럼명 ASC_또는_DESC;
```
- `[조건문]`은 생략 가능하다.
- `ASC` 오름차순, 위의 레코드에서 위쪽 레코드로 가면서 수치가 증가한다.
- `DESC` 내림차순, 위의 레코드에서 아래 레코드로 가면서 수치가 감소한다.

## Question

#### 멤버의 평균 키가 164센티 이상인 회원의 아이디, 이름, 데뷔일, 평균키를 조회하되 평균키의 순서는 키가 높은 순으로 나열되도록 하라
```
select mem_id, mem_name, debut_date, height from member where height >= 164 order by height desc;
```
- 키가 높은 순이라는 것은 수치가 점점 감소하는 것이므로 `desc`에 해당한다.

#### 위의 결과에서 평균키가 동일하다면 데뷔일이 빠른 순으로 나열되도록 하라.
```
select mem_id, mem_name, debut_date, height from member where height >= 164 order by height desc, debut_date asc;
```
- 데뷔일이 빠른 순이라는 것은 수치가 점점 증가하도록 되어야 하므로 `asc`에 해당한다.

#### 데뷔일이 빠른 순대로 멤버 3명의 이름과 데뷔일을 조회하라.
```
select mem_name, debut_date from member order by debut_date asc limit 3;
```

#### 데뷔일이 3번째로 빠른 멤버와 그 다음으로 빠른 멤버 둘의 이름과 데뷔일을 조회하라
```
select mem_name, debut_date from member order by debut_date asc limit 3, 2;
```

## distinct
### syntax
```
select distinct 대상컬럼 from 테이블명;
```
- 대상컬럼 앞에 `distinct`라는 키워드를 사용한다.

#### 회원이 거주하고 있는 지역의 리스트를 중복없이 조회하라
```
select distinct addr from member;
```