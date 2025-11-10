# SQL_BASIC 6주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_6th_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**6주차 과제는 강의 내용을 정리하는 것과 함께, 프로그래머스에서 제공하는 SQL 문제를 직접 풀어보는 실습도 병행합니다.** 강의에서는 **배운 내용을 정리하고 주요 쿼리 예제를 정리**하며, 프로그래머스 문제는 **직접 풀어본 뒤 풀이 과정과 결과, 배운 점을 함께 기록**해주세요. 완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**(수행 인증샷은 필수입니다.)** 

## SQL_BASIC_6th

### 섹션 6. 다량의 자료를 연결 : JOIN 

### 5-1. Intro

### 5-2. JOIN 이해하기

### 5-3. 다양한 JOIN 방법

### 5-4. JOIN 쿼리 작성하기 

### 5-5. JOIN을 처음 공부할 때 헷갈렸던 부분

### 5-6. JOIN 연습문제 1~2번

### 5-6. JOIN 연습문제 3~5번

### 5-7. 정리



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | ✅         |
| 4주차 | 섹션 **3-4** ~ **4-4** | ✅         |
| 5주차 | 섹션 **4-4** ~ **4-9** | ✅         |
| 6주차 | 섹션 **5-1** ~ **5-7** | ✅         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<!-- 여기까진 그대로 둬 주세요-->

<br>

---

# 1️⃣ 개념정리

## 5-2. JOIN 이해하기

~~~
✅ 학습 목표 :
* JOIN에 대한 정의와 필요성에 대해 설명할 수 있다.
~~~

👉 JOIN: 서로 다른 테이블을 공통 키(Key)를 기준으로 연결하는 것 → 여러 작은 테이블을 합쳐 새로운 큰 테이블을 생성함 

👉 공통 컬럼(주로 id 등 Key)이 있을 때 JOIN 가능하고, 특정 범위 기준(Date 등)으로도 JOIN 가능함

👉 JOIN의 필요성: 관계형 데이터베이스는 정규화를 통해 데이터 중복을 최소화함
→ 테이블이 분리되어 있으므로 필요한 데이터를 보기 위해 JOIN이 필요함

(+) 개발 관점: 데이터 분리(정규화) 선호 / 분석 관점: 미리 JOIN된 형태가 편함



## 5-3. 다양한 JOIN 방법

~~~
✅ 학습 목표 :
* JOIN 방법들의 종류를 설명할 수 있다. 
* 각 JOIN 방법들의 차이점에 대해서 설명할 수 있다. 
~~~

👉 JOIN의 종류 및 특징
* (INNER) JOIN: 두 테이블의 공통된 키 값이 존재하는 행만 연결함
→ 교집합 형태

* LEFT (OUTER) JOIN:
왼쪽 테이블을 기준으로 연결
오른쪽에 없는 값은 NULL로 표시됨 → 왼쪽 전체 + 공통 부분 

* RIGHT (OUTER) JOIN:
오른쪽 테이블을 기준으로 연결
왼쪽에 없는 값은 NULL로 표시됨
→ 오른쪽 전체 + 공통 부분

* FULL (OUTER) JOIN:
양쪽 테이블의 모든 행을 포함해 연결
한쪽에만 있는 값은 NULL 처리됨
→ 합집합 형태

* CROSS JOIN:
두 테이블의 모든 행을 곱하기처럼 결합함
→ 데이터 수 급증, 조심해서 사용해야 함

👉 공부 팁
* 처음에는 LEFT JOIN 중심으로 연습해도 충분
* 이후 INNER JOIN → FULL / CROSS JOIN 순으로 확장하면 됨



## 5-4. JOIN 쿼리 작성하기 

~~~
✅ 학습 목표 :
* JOIN을 사용한 문법에 대해 이해하여 적용할 수 있다.
* JOIN 을 활용한 쿼리를 작성할 수 있다. 
~~~

👉 쿼리 작성 흐름
- (1) 테이블 확인: 각 테이블에 어떤 컬럼과 데이터가 있는지 확인
- (2) 기준 테이블 정의: 가장 중심이 될, 많이 참고할 테이블을 기준으로 설정
- (3) JOIN Key 찾기: 여러 테이블을 연결할 공통 키(ON 조건)를 파악
- (4) 결과 예상하기: 최종 결과 테이블의 형태를 손이나 엑셀로 미리 그려보기(정답지처럼)
- (5) 쿼리 작성 / 검증: 실제 쿼리 실행 후 예상한 결과와 일치하는지 확인

👉 JOIN 쿼리 기본 구조
* `FROM` 절 밑에 `JOIN` 작성
* `JOIN` 종류 명시 후, `ON`으로 연결 기준(Key) 지정
* `CROSS JOIN`만 `ON` 생략 가능

(1) **INNER JOIN** – 두 테이블의 공통 키만 연결
```
SELECT 
  col
FROM table_a AS A
INNER JOIN table_b AS B
ON A.key = B.key;
```
(2) **LEFT / RIGHT JOIN** – 기준 테이블 한쪽 전체 포함
```
SELECT 
  col
FROM table_a AS A
LEFT JOIN table_b AS B
ON A.key = B.key;
```
(※ RIGHT JOIN도 동일 구조, 단 기준 테이블이 오른쪽)

(3) **FULL JOIN** – 양쪽 테이블 모두 포함
```
SELECT 
  col
FROM table_a AS A
FULL JOIN table_b AS B
ON A.key = B.key;
```
(4) **CROSS JOIN** – 모든 행 조합(ON 불필요)
```
SELECT 
  col
FROM table_a AS A
CROSS JOIN table_b AS B;
```



## 5-6. JOIN 연습문제 1~5번 

~~~
✅ 학습 목표 :
* 연습문제(3문제 이상) 푼 것들 정리하기
~~~
**(1) 트레이너가 보유한 포켓몬들은 얼마나 있는지 알 수 있는 쿼리를 작성해주세요.**

~~~
SELECT 
  kor_name,
  COUNT(tp.id) AS pokemon_cnt
FROM (
SELECT 
  id,
  trainer_id,
  pokemon_id,
  status 
FROM basic.trainer_pokemon
WHERE 
  status IN ("Active", "Training")
) AS tp
LEFT JOIN basic.pokemon AS p  
ON tp.pokemon_id = p.id
GROUP BY
  kor_name 
ORDER BY 
  pokemon_cnt DESC 
~~~
👉새롭게 알게 된 점
* (1) `WHERE`로 먼저 필터링해서 row 수 줄인 다음에 `JOIN`하는 게 효율적임
* (2) 오류 메시지 `Column name id is ambiguous` 뜨면 컬럼 이름이 겹친다는 뜻임
→ JOIN한 테이블들 중 같은 컬럼명 있으면 `table_name.column_name`으로 구체적으로 써야 함
* (3) SQL 실행 순서 생각할 때
: SELECT
→ FROM
→ **"JOIN"**
→ WHERE
→ GROUP BY
순서로 흘러감

**(2) 각 트레이너가 가진 포켓몬 중에서 'Grass' 타입의 포켓몬 수를 계산해주세요. (단, 편의를 위해 type1 기준으로 계산해주세요.)**
~~~
SELECT
  p.type1,
  COUNT(tp.id) AS pokemon_cnt
FROM (
  SELECT 
    id, 
    trainer_id,
    pokemon_id,
    status 
  FROM basic.trainer_pokemon 
  WHERE 
    status IN ("Active", "Training") 
) AS tp
LEFT JOIN basic.pokemon AS p 
ON tp.pokemon_id = p.id 
WHERE 
  type1 = "Grass"
GROUP BY 
  type1
ORDER BY
  2 DESC 
~~~
👉새롭게 알게 된 점
* (1) LEFT JOIN 쓸 때는 어떤 테이블을 왼쪽에 둘지가 중요함
→ 계속 문제 풀어보면서 감 잡는 게 좋음
→ 내가 중점적으로 봐야 하는 정보, 구하고자 하는 데이터가 어디 테이블에 있는지 먼저 확인해야 함
* (2) 보통 JOIN할 수 있는 key가 많이 보이는 테이블을 왼쪽(LEFT)에 두는 경우 많음
→ 예외도 있음 (항상 그런 건 아님)

**(3) 트레이너의 고향(hometown)과 포켓몬을 포획한 위치(location)를 비교하여, 자신의 고향에서 포켓몬을 포획한 트레이너의 수를 계산해주세요.**
~~~
SELECT
  COUNT (DISTINCT tp.trainer_id) AS trainer_uniq,
FROM basic.trainer AS t 
LEFT JOIN basic.trainer_pokemon AS tp 
ON t.id = tp.trainer_id
WHERE 
  location IS NOT NULL 
  AND t.hometown = tp.location
~~~
👉새롭게 알게 된 점
* DISTINCT 써서 고유값 확인하는 습관 들이기
→ 중복 있는지, 데이터 제대로 정제됐는지 볼 때 유용함（항상 염두에 두고 쓰면 데이터 이해도 높아짐）

**(4) Master 등급인 트레이너들은 어떤 타입의 포켓몬을 제일 많이 보유하고 있을까요?**
~~~
SELECT
  type1,
  COUNT(tp.id) AS pokemon_cnt
FROM ( 
SELECT 
  id,
  trainer_id,
  pokemon_id, 
  status 
FROM basic.trainer_pokemon 
WHERE 
  status IN ("Active", "Training")
) AS tp 
LEFT JOIN basic.pokemon AS p 
ON tp.pokemon_id = p.id 
LEFT JOIN basic.trainer AS t
ON tp.trainer_id = t.id 
WHERE 
  t.achievement_level = "Master"
GROUP BY 
  type1
ORDER BY
  2 DESC
LIMIT 1  
~~~
👉새롭게 알게 된 점
* LEFT JOIN은 여러 번 연속해서 쓸 수 있음 (LEFT JOIN 2번, 3번, N번 가능함)
→ 기준 테이블(왼쪽 테이블)은 계속 유지되고, 오른쪽 테이블만 새로 붙는 구조임

**(5) Incheon 출신 트레이너들은 1세대, 2세대 포켓몬을 각각 얼마나 보유하고 있나요?**
~~~

~~~
👉새롭게 알게 된 점
* 



<br>

<br>

---

# 2️⃣ 확인문제 & 문제 인증

## 프로그래머스 문제 

https://school.programmers.co.kr/learn/courses/30/lessons/164673

> 조건에 부합하는 중고거래 댓글 조회하기 (JOIN)

https://school.programmers.co.kr/learn/courses/30/lessons/144854

> 조건에 맞는 도서와 저자 리스트 출력하기 (JOIN)

<!-- 정답을 맞추게 되면, 정답입니다. 이 부분을 캡처해서 이 주석을 지우시고 첨부해주시면 됩니다. --> 



---

# 3️⃣ 참고자료

JOIN 에 대해서 그림으로 쉽게 이해할 수 있는 자료들도 있어서 첨부합니다. 아래의 블로그도 학습할 때 같이 참고해주세요.

1. https://data-marketing-bk.tistory.com/entry/SQL-JOIN-%ED%95%9C-%EB%B0%A9%EC%97%90-%EC%A0%95%EB%A6%AC-%EA%B0%9C%EB%85%90%EB%B6%80%ED%84%B0-%EC%BD%94%EB%93%9C%EA%B9%8C%EC%A7%80-%EC%9D%B4%EA%B2%83%EB%A7%8C-%EB%B3%B4%EC%9E%90



2. https://velog.io/@wijoonwu/JOIN

<br>

### 🎉 수고하셨습니다.