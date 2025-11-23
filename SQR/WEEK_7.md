# SQL_BASIC 7주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_7th_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**7주차 과제는 강의 내용을 정리하는 것과 함께, 프로그래머스에서 제공하는 SQL 문제를 직접 풀어보는 실습도 병행합니다.** 강의에서는 **배운 내용을 정리하고 주요 쿼리 예제를 정리**하며, 프로그래머스 문제는 **직접 풀어본 뒤 풀이 과정과 결과, 배운 점을 함께 기록**해주세요. 완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**(수행 인증샷은 필수입니다.)** 

**(마지막 주차입니다. 조금만 더 힘내주세요~!!!)**

## SQL_BASIC_7th

### 섹션 7 데이터 결과 검증, 가독성 있는 쿼리 작성하기

### 6-1. Intro

### 6-2. 가독성을 챙기기 위한 SQL 스타일 가이드

### 6-3. 가독성을 챙기기 위한 WITH 문 & 파티션

### 6-4. 데이터 결과 검증 정의

### 6-5. 데이터 결과 검증 예시

### 6-6. 정리 



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | ✅         |
| 4주차 | 섹션 **3-4** ~ **4-4** | ✅         |
| 5주차 | 섹션 **4-4** ~ **4-9** | ✅         |
| 6주차 | 섹션 **5-1** ~ **5-7** | ✅         |
| 7주차 | 섹션 **6-1** ~ **6-6** | ✅         |

<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 개념정리

## 6-2. 가독성을 챙기기 위한 SQL 스타일 가이드

~~~
✅ 학습 목표 :
* 데이터 결과 검증하기 전에 실수가 발생하는 원인을 설명할 수 있다.
* SQL 쿼리를 가독성 있게 작성할 수 있다. 
~~~

👉 실수가 발생하는 순간

① 문법을 잘못 알고 있는 경우
→ 문법 공부를 하거나, 오류 메시지를 참고해 문법을 바로잡기

② 데이터를 제대로 파악하지 않고 쿼리를 작성하는 경우
→ 데이터 구조와 컬럼 value 설명을 미리 정리해두기

③ 쿼리가 지나치게 복잡한 경우
→ 쿼리를 단순화하고 적절히 분리해 가독성 있게 작성하기

👉 참고할 만한 가이드
Mozilla(Firefox)의 SQL 스타일 가이드
🔗 https://docs.telemetry.mozilla.org/concepts/sql_style.html

👉 **Firefox의 대표 스타일**

① SELECT, FROM, WHERE 등 예약어는 대문자로 작성한다.

② 컬럼 이름은 snake_case로 작성한다. (무엇보다 일관성이 중요)
- ※ snake_case: 언더바(_)로 단어를 구분하는 방식 ※

③ Alias(별칭)는 의미가 드러나는 명시적 이름을 사용한다.

④ 기본적으로 왼쪽 정렬을 기준으로 작성한다.

⑤ 예약어나 컬럼은 한 줄에 하나씩 적는 것을 권장한다.

⑥ 쉼표는 컬럼명 바로 뒤에 붙인다.



## 6-3. 가독성을 챙기기 위한 WITH문 & 파티션

~~~
✅ 학습 목표 :
* SQL 쿼리를 가독성 있게 작성할 수 있다. 
* WITH문과 파티션을 활용해서도 가독성을 챙길 수 있다. 
~~~

👉 SQL 쿼리 작성 시 발생하는 문제점

쿼리를 다른 곳에서도 재사용해야 하면 복붙을 하게 되고, 이 과정에서 중복이 늘고 쿼리가 점점 복잡해지는 문제가 생긴다.
→ 이를 해결하기 위해 <a>**WITH 구문**</a>을 사용할 수 있다!

👉 WITH 구문이란?

- CTE(Common Table Expression) 라고 부르며, SELECT 구문에 이름을 붙여주는 것과 같다.

- 쿼리 안에서 반복적으로 재사용할 수 있는 장점이 있다.

👉 WITH 구문 사용 예시
~~~
WITH name_a AS (
  SELECT
    col
  FROM table1
), name_b AS (
  SELECT
    col2
  FROM table2
)

SELECT 
  col
FROM name_a  -- 앞서 정의한 CTE를 여기에서 바로 사용할 수 있음
~~~

👉 Partition이란?

* 하나의 큰 테이블을 특정 컬럼 기준으로 여러 조각으로 나누어 저장하는 방식.

* 즉, 테이블을 물리적으로 어떻게 저장·분리할지 결정하는 구조적 옵션이다.

👉 Partition을 사용하면 좋은 점
(※ 가독성도 중요하지만, 특히 비용 측면에서 매우 중요!)

① 쿼리 성능 향상 : 
전체를 스캔하는 대신, 필요한 파티션만 읽으면 돼서 훨씬 빠르다.

② 데이터 관리 용이성 : 
특정 날짜의 데이터를 일괄 수정하거나 삭제해야 할 때, 해당 파티션만 처리하면 된다.

③ 비용 절감 : 
파티션 범위에 포함되는 데이터만 스캔하므로 불필요한 스캔 비용을 줄일 수 있다.
(BigQuery는 스캔한 데이터 용량에 비례해 과금하기 때문에 효율적인 저장 구조가 매우 중요)


## 6-4. 데이터 결과 검증 정의 

~~~
✅ 학습 목표 :
* 데이터 결과 검증이 어떤 과정인지 설명할 수 있다. 
* 데이터 결과 검증에 대한 예시를 이해할 수 있다.  
~~~

👉 데이터 결과 검증이란?
SQL 쿼리 실행 후 얻은 결과가 내가 예상한 결과와 일치하는지 확인하는 과정으로, 분석의 정확성과 신뢰성을 확보하기 위해 필수적이다.

* 검증 과정 :
① 기대하는 예상 결과 정의 → ② 쿼리 작성 → ③ 실제 결과와 비교

* 핵심 포인트 : 문제를 명확하게 정의하고, 도메인의 특수성을 충분히 이해한 상태에서 검증하기

👉 데이터 결과 검증의 전체 흐름

① 문제 정의 확인

* 구체적으로 어떤 문제인지 다시 점검

* 필요한 조건이 있는지, 요청 사항은 무엇인지 명확히 파악

② Input / Output 설계

* 사용할 데이터(Input)와 최종적으로 얻고 싶은 결과(Output)를 미리 손으로, 혹은 엑셀로 구체화

* 단순히 Input → Output일 수도 있지만, Input → (중간 결과) → Output 처럼 단계가 생길 수 있기 때문에 중간 결과도 함께 생각해야 한다

③ 가독성을 고려한 쿼리 작성

* 논리 흐름이 명확하고 다시 봐도 이해되는 형태로 작성하기

④ 결과 비교

* 예상과 실제가 일치하는지 확인
* 오류가 있다면 쿼리를 다시 수정하거나 문제 정의를 재확인하는 식으로 피드백 루프를 반복

* 오류가 없다면 검증 완료!

👉 데이터 결과 검증 시 자주 사용하는 SQL 패턴

① COUNT(*)

* 행 수 확인
* 의도한 데이터 개수와 맞는지 검증

② NOT NULL 검사

* 특정 컬럼에 NULL이 존재하는지 확인
* 필수값이 비어 있는지 점검

③ DISTINCT

* 고유값을 확인해 중복 여부를 파악

④ IF문 / CASE WHEN

* 조건이 예상과 일치하면 TRUE, 아니면 FALSE 등으로 검증 로직 만들 때 사용

⑤ COUNT vs COUNT(DISTINCT)

* COUNT(DISTINCT col) 과 COUNT(col) 개수를 비교
* 두 값이 같다면 중복 없음

👉 데이터 결과 검증 예시 문제

* 각 트레이너가 진행한 배틀의 승리 비율을 계산해야 하며,배틀에 참여한 횟수가 9회 이상인 경우만 계산한다.

👉 문제 풀이 전반적 흐름

① **전체 데이터(raw 데이터) 파악**

② **특정 user_id 선정**

③ **승률을 직접 COUNT하여 예상 값 기록**

④ **쿼리 작성**

⑤ **실제 결과와 비교**

⑥ **일치한다면 특정 유저 조건 제거 → 전체 유저에게 확대 적용**

👉 구체적인 문제 풀이

① 기본 데이터 파악

* 테이블에는 player1_id, player2_id가 존재함.

② 특정 유저 선택

* 예시로 trainer/player_id가 7인 유저를 선정.
~~~sql
SELECT
  *
FROM `basic.battle`
WHERE 
  (player1_id = 7) OR (player2_id = 7);
~~~
③ 예상 승률 계산
* player 7은 총 9번 배틀 중 5번 승리
→ 예상 승률 = 5 / 9 = 0.555556
(※ 이런 값을 별도로 주석 또는 노트로 기록해두기✏️)

④ 쿼리 작성 → 통합 테이블 생성 (trainer_id 기준으로 펼치기)
* `player1_id`와 `player2_id`로 나뉘어 있어 바로 집계가 어렵기 때문에,
두 플레이어를 하나의 `trainer_id`로 통합한 테이블을 만든다.
~~~sql
SELECT 
  *
FROM (
  SELECT 
    id AS battle_id,
    player1_id AS trainer_id,
    winner_id
  FROM `basic.battle`
  UNION ALL
  SELECT 
    id AS battle_id,
    player2_id AS trainer_id,
    winner_id
  FROM `basic.battle`
)
ORDER BY battle_id;
~~~
* trainer_id = 7의 총 배틀 횟수 확인
~~~sql
WITH battle_basic AS (
  SELECT 
    id AS battle_id,
    player1_id AS trainer_id,
    winner_id
  FROM `basic.battle`
  UNION ALL
  SELECT 
    id AS battle_id,
    player2_id AS trainer_id,
    winner_id
  FROM `basic.battle`
)

SELECT 
  trainer_id,
  COUNT(*) AS total_battles,
  COUNT(DISTINCT battle_id) AS unique_battles
FROM battle_basic
WHERE trainer_id = 7
GROUP BY trainer_id;
~~~
* 승·패·무 결과 만들기 (CASE WHEN)
~~~sql
WITH battle_basic AS (
  SELECT 
    id AS battle_id,
    player1_id AS trainer_id,
    winner_id
  FROM `basic.battle`
  UNION ALL
  SELECT 
    id AS battle_id,
    player2_id AS trainer_id,
    winner_id
  FROM `basic.battle`
)

SELECT 
  *,
  CASE
    WHEN trainer_id = winner_id THEN "WIN"
    WHEN winner_id IS NULL THEN "DRAW"
    ELSE "LOSE"
  END AS battle_result
FROM battle_basic
WHERE trainer_id = 7;
~~~
⑤ COUNTIF로 실제 승률 계산 후 예상값과 비교
~~~sql
WITH battle_basic AS (
  SELECT 
    id AS battle_id,
    player1_id AS trainer_id,
    winner_id
  FROM `basic.battle`
  UNION ALL
  SELECT 
    id AS battle_id,
    player2_id AS trainer_id,
    winner_id
  FROM `basic.battle`
),

battle_with_result AS (
  SELECT 
    *,
    CASE
      WHEN trainer_id = winner_id THEN "WIN"
      WHEN winner_id IS NULL THEN "DRAW"
      ELSE "LOSE"
    END AS battle_result
  FROM battle_basic
  WHERE trainer_id = 7 
)

SELECT 
  trainer_id,
  COUNTIF(battle_result = "WIN") AS win_count,
  COUNT(battle_id) AS total_battle_count,
  COUNTIF(battle_result = "WIN") / COUNT(DISTINCT battle_id) AS win_ratio
FROM battle_with_result
GROUP BY trainer_id;
~~~
⑥ 검증 완료 후 전체 유저 대상 계산
* 예상값과 실제값이 일치한다면,
`WHERE trainer_id = 7` 조건을 제거하고
9회 이상 배틀한 유저만 대상으로 필터링한다.
~~~sql
...
-- WHERE trainer_id = 7  ← 주석 처리
...

HAVING 
  total_battle_count >= 9;
~~~



<br>

<br>

---

# 2️⃣ 확인문제 & 문제 인증

## 프로그래머스 문제 

https://school.programmers.co.kr/learn/courses/30/lessons/157343

> 특정 옵션이 포함된 자동차 리스트 구하기

☑️풀이 과정 : 
* OPTIONS 컬럼에서 특정 옵션 포함 여부 LIKE로 확인함.
* '%네비게이션%' 패턴으로 부분 문자열 검색함.
* 정렬은 CAR_ID 기준으로 DESC 적용함.

☑️결과 : 
~~~sql
SELECT 
  *
FROM 
  CAR_RENTAL_COMPANY_CAR
WHERE OPTIONS LIKE '%네비게이션%'
ORDER BY CAR_ID DESC;
~~~
💡배운 점 : 문자열 리스트는 LIKE 검색이 필요하며, '%패턴'은 인덱스 사용 어려워 성능 저하 가능함. 정렬 방향은 DESC처럼 명시해야 함.


https://school.programmers.co.kr/learn/courses/30/lessons/59044

> 오랜 기간 보호한 동물(1) 

☑️풀이 과정 : 
* 입양 여부는 LEFT JOIN 후 O.ANIMAL_ID IS NULL로 판별함.
* 오래 보호된 순은 DATETIME ASC 정렬함.
* 조회 개수는 LIMIT 3 적용함.

☑️결과 : 
~~~sql
SELECT 
  I.NAME, 
I.DATETIME
FROM ANIMAL_INS I
LEFT JOIN ANIMAL_OUTS O 
  ON I.ANIMAL_ID = O.ANIMAL_ID
WHERE O.ANIMAL_ID IS NULL
ORDER BY I.DATETIME
LIMIT 3;
~~~
💡배운 점 : LEFT JOIN + IS NULL 로 누락 데이터 찾는 패턴 자주 쓰이며, 오래된 날짜는 값이 작아 ASC 정렬을 사용함. LIMIT로 결과 수를 쉽게 제한할 수 있음.


https://school.programmers.co.kr/learn/courses/30/lessons/59043

> 있었는데요 없었습니다.

☑️풀이 과정 : 
* 입양된 동물만 비교하려고 INNER JOIN 사용함.
* 오류 데이터 조건은 OUT.DATETIME < INS.DATETIME 로 판단함.
* 보호 시작일 빠른 순으로 I.DATETIME ASC 정렬함.

☑️결과 : 
~~~sql
SELECT 
  I.ANIMAL_ID, 
  I.NAME
FROM ANIMAL_INS I
JOIN ANIMAL_OUTS O 
  ON I.ANIMAL_ID = O.ANIMAL_ID
WHERE O.DATETIME < I.DATETIME
ORDER BY I.DATETIME;
~~~
💡배운 점 : DATETIME은 숫자처럼 직접 비교 가능하며, 오류 검증은 핵심 조건식(입양일 < 보호 시작일)만 정확히 잡으면 쉽게 해결됨.



## LeetCode 문제

https://leetcode.com/problems/combine-two-tables/description/

> 175. Combine Two Tables

☑️풀이 과정 : 
* Person 에 있는 사람은 모두 나와야 하니까 Person을 왼쪽 테이블로 두고 LEFT JOIN함 .
* Address에 해당 personId 가 없으면 city, state 가 자동으로 NULL로 뜸.

☑️결과 : 
~~~sql
SELECT 
  p.firstName,
  p.lastName,
  a.city,
  a.state
FROM Person AS p
LEFT JOIN Address AS a 
     ON p.personId = a.PersonId;
~~~


https://leetcode.com/problems/list-the-products-ordered-in-a-period/

> 1327. List the Products Ordered in a Period

☑️풀이 과정 : 
* WHERE에서 2020-02-01 ~ 2020-02-29 만 필터링함.
* GROUP BY로 제품별 합계를 구함.
* HAVING으로 합계가 100 이상인 제품만 남김.

☑️결과 : 
~~~sql
SELECT 
  p.product_name,
  SUM(o.unit) AS unit
FROM Orders AS o 
JOIN products AS p 
    ON o.product_id = p.product_id 
WHERE o.order_date BETWEEN '2020-02-01' AND '2020-02-29'
GROUP BY 
  p.product_id,
  p.product_name
HAVING 
  SUM(o.unit) >=100;
~~~



### <문제 인증 캡쳐>
(1) **특정 옵션이 포함된 자동차 리스트 구하기**
![alt text](<images/(WEEK7)SQL프로그래머스 문제/(1) 자동차.png>)
(2) **오랜 기간 보호한 동물(1)**
![alt text](<images/(WEEK7)SQL프로그래머스 문제/(2) 동물.png>)
(3) **있었는데요 없었습니다.**
![alt text](<images/(WEEK7)SQL프로그래머스 문제/(3) 있었는데.png>)
(4) **Combine Two Tables**
![alt text](<images/(WEEK7)SQL프로그래머스 문제/(4) .png>)
(5) **List the Products Ordered in a Period**
![alt text](<images/(WEEK7)SQL프로그래머스 문제/(5).png>)


## 문제 1

> **🧚예운이는 다음 SQL 쿼리를 다트비 정규과제에 제출했다. 제출한 쿼리는 다음과 같고, 이 쿼리는 에러 메시지 없이 잘 수행하는 쿼리이다.**

~~~sql
# 주영이가 작성한 가독성 나쁜 SQL 

select u.name , o.OrderID
, p.ProductName ,od.Quantity ,od.UnitPrice 	from Users u	join Orders o on u.id = o.userId
join OrderDetails od on o.OrderID = od.orderID	join Products p on od.ProductID = p.ProductID
where u.region= 'Busan'			order by o.OrderID
~~~

> **이에 과제를 검사하던 정우는 작성한 SQL을 보고 코드 리뷰를 진행하려고 했지만, 다음 쿼리를 보고 예운이에게 질문을 하였다. "예운아, 이 쿼리 가독성이 좀 안 좋은데 내가 고쳐도 괜찮을까? 가독성 좋게 SQL 가이드에 따라 정리해보려고 해"**
>
> 다음 SQL 쿼리를 **가독성 좋은 스타일로 다시 작성해보세요.** 



~~~sql
SELECT
  u.name,
  o.OrderID,
  p.ProductName,
  od.Quantity,
  od.UnitPrice
FROM Users u
JOIN Orders o
    ON u.id = o.userId
JOIN OrderDetails od
    ON o.OrderID = od.orderID
JOIN Products p
    ON od.ProductID = p.ProductID
WHERE u.region = 'Busan'
ORDER BY o.OrderID;

~~~



<br>

<br>

<!-- 이렇게 SQL BASIC 과제가 마무리되었습니다. SQL은 범위가 넓고 처음 접할 때 어렵게 느껴지는 학문이지만, 이번 기수에서는 지난 기수에도 활용했던 인프런 무료 강의를 통해 기초를 탄탄히 다질 수 있도록 구성했습니다. 환경 세팅 과정이 다소 복잡했을 수도 있지만, 이번 과제를 통해 기본적인 쿼리 작성과 SELECT 명령어의 개념을 충분히 익혔을 거라 생각합니다. BASIC을 통해 데이터를 추출하는 기초를 다졌으면, 이제 ADVANCED 트랙에서 실무에 맞게 더 복잡한 문접과 분석 쿼리, 그리고 MASTER 트랙에서 실제 데이터베이스를 다루는 실무 명령어까지 배워갈 수 있습니다. 앞으로의 SQL 학습에도 화이팅이고, 부족한 템플릿이었지만 끝까지 함께해줘서 진심으로 감사드립니다.  -->

### 🎉 수고하셨습니다.