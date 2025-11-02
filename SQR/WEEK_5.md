# SQL_BASIC 5주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_5th_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**5주차 과제는 문제 풀이를 중심으로**, 강의에서 제시된 예제 문제 중 **3 문제 이상을 선택하여 직접 풀어본 뒤**, 강의 영상의 풀이와 비교해 **틀린 부분, 맞은 부분, 새롭게 배운 개념**을 구체적으로 정리해주세요. (적어도 4문제는 정리해야 합니다.) 완성된 과제는 Gihub에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**(수행 인증샷은 필수입니다.)** 



## SQL_BASIC_5th

### 섹션 5. 데이터 탐색 - 변환

### 4-4. 날짜 및 시간 데이터 이해하기(2) (EXTRACT, DATETIME_TRUNC, PARSE_DATETIME, FROMAT_DATETIME)

### 4-5. 시간 데이터 연습문제 1~2번

### 4-5. 시간 데이터 연습문제 3~5번

### 4-6. 조건문 (CASE WHEN, IF)

### 4-7. 조건문 연습 문제

### 4-8. 정리

### 4-9. BigQuery 공식 문서 확인하는 법

(강의에서 연습문제가 많아서 따로 프로그래머스 문제 과제는 없습니다.)



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | ✅         |
| 4주차 | 섹션 **3-4** ~ **4-4** | ✅         |
| 5주차 | 섹션 **4-4** ~ **4-9** | ✅         |
| 6주차 | 섹션 **5-1** ~ **5-7** | 🍽️         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<br>



<!-- 여기까진 그대로 둬 주세요-->

---

# 4-4. 날짜 및 시간 데이터 이해하기(2) (EXTRACT, DATETIME_TRUNC, PARSE_DATETIME, FROMAT_DATETIME)

~~~
✅ 학습 목표 :
* 날짜 및 시간 데이터에 대해서 더 자세히 설명할 수 있다. 
* CURRENT_TIME, EXTRACT, DATETIME_TRUNC, PARSE_DATETIME, FROMAT_DATETIME 을 설명할 수 있다. 
~~~

👉 **CURRENT_DATETIME** 
- CURRENT_DATETIME([time_zone]) : 현재 DATETIME 출력
~~~
SELECT
  CURRENT_DATE()AScurrent_date,
  CURRENT_DATE("Asia/Seoul")ASasia_date,
  CURRENT_DATETIME()AScurrent_datetime,
  CURRENT_DATETIME("Asia/Seoul")AScurrent_datetime_asia;
~~~
---
👉 **EXTRACT**
- DATETIME에서 특정 부분만 추출하고 싶은 경우
- EXTRACT(특정 부분 FROM DATETIME) 
~~~
EXTRACT(DATE FROM DATETIME "2024-01-02 14:00:00") AS date, 
→ 2024-01-02

EXTRACT(YEAR FROM DATETIME "2024-01-02 14:00:00") AS year, 
→ 2024

EXTRACT(MONTH FROM DATETIME "2024-01-02 14:00:00" AS DATETIME) AS month, 
→ 1

EXTRACT(DAY FROM DATETIME "2024-01-02 14:00:00" AS DATETIME) AS day, 
→ 2

EXTRACT(HOUR FROM DATETIME "2024-01-02 14:00:00" AS DATETIME) AS hour, 
→ 14

EXTRACT(MINUTE FROM DATETIME "2024-01-02 14:00:00" AS DATETIME) AS minute, 
→ 0
~~~
- ※EXTRACT(DAYOFWEEK FROM datetime_col)※ : 요일을 추출하고 싶은 경우 → 요일을 숫자 형태로 반환, '일요일 =1'을 기준으로 [1~7] 범위의 값을 반환함 
---
👉 **DATETIME_TRUNC**
- DATETIME_TRUNC(datetime_col, 특정 부분) : 특정 부분을 기준으로 자름 
- 시간(HOUR) 자를 때 많이 사용 
~~~
SELECT
  DATETIME "2024-03-02 14:42:13" AS original_data,

  DATETIME_TRUNC(DATETIME "2024-03-02 14:42:13", DAY) AS day_trunc,
  → 2024-03-02T00:00:00

  DATETIME_TRUNC(DATETIME "2024-03-02 14:42:13", YEAR) AS year_trunc,
  → 2024-01-01T00:00:00

  DATETIME_TRUNC(DATETIME "2024-03-02 14:42:13", MONTH) AS month_trunc,
  → 2024-03-01T00:00:00

  DATETIME_TRUNC(DATETIME "2024-03-02 14:42:13", HOUR) AS hour_trunc;
  → 2024-03-02T14:00:00
~~~
---
👉 PARSE_DATETIME
- 문자열로 저장된 DATETIME을 DATETIME 타입으로 바꾸고 싶은 경우
- PARSE_DATETIME('문자열의형태', 'DATETIME 문자열') AS datetime
- "파싱하다" : 문자열을 보고 알맞은 것으로 배치한다 
~~~
SELECT
  PARSE_DATETIME('%Y-%m-%d%H:%M:%S', '2024-01-11 12:35:35') AS parse_datetime;
  → 2024-01-11T12:35:35
~~~
---
👉 FORMAT_DATETIME
-  DATETIME 타입 데이터를 특정 형태의 문자열 데이터로 변환하고 싶은 경우
- ※ 문자열 → DATETIME : PARSE_DATETIME
- ※ DATETIME → 문자열 : FORMAT_DATETIME
~~~
SELECT
  FORMAT_DATETIME("%c", DATETIME "2024-01-1112:35:35") AS formatted;
~~~
---
👉 LAST_DAY
- 마지막 날을 알고 싶은 경우(자동으로 월의 마지막 값을 계산해서 특정 연산을 할 경우)
- LAST_DAY(DATETIME) : 월의 마지막 값을 반환
~~~
LAST_DAY(DATETIME '2024-01-03 15:30:00') AS last_day,
→ 2024-01-31 (월의 마지막 일자)

LAST_DAY(DATETIME '2024-01-03 15:30:00', MONTH) AS last_day_month,
→ 2024-01-31

LAST_DAY(DATETIME '2024-01-03 15:30:00', WEEK) AS last_day_week,
→ 2024-01-06 (대부분 일요일 기준) 

LAST_DAY(DATETIME '2024-01-03 15:30:00', WEEK(SUNDAY)) AS last_day_week_sun,
→ 2024-01-06(일요일 기준으로 마지막 날 : 토요일 날짜)

LAST_DAY(DATETIME '2024-01-03 15:30:00', WEEK(MONDAY)) AS last_day_week_mon
→ 2024-01-06(월요일 기준으로 마지막 날 : 일요일 날짜) 
~~~
 ---
👉 DATETIME_DIFF
- 두 DATETIME의 차이를 알고 싶은 경우
- DATETIME_DIFF(첫 DATETIME, 두번째 DATETIME, 궁금한 차이)
~~~
SELECT
  DATETIME_DIFF(first_datetime, second_datetime, DAY) AS day_diff1,
  → 1187 (날짜 차이)
  DATETIME_DIFF(second_datetime, first_datetime, DAY) AS day_diff2,
  → -1187
  DATETIME_DIFF(first_datetime, second_datetime, MONTH) AS month_diff,
  → 39 (개월 차이) 
  DATETIME_DIFF(first_datetime, second_datetime, WEEK) AS week_diff,
  → 170 (주 차이)
FROM(
  SELECT
    DATETIME "2024-04-02 10:20:00" AS first_datetime,
    DATETIME "2021-01-01 15:30:00" AS second_datetime,
  )
~~~




# 4-6. 조건문(CASE WHEN, IF)

~~~
✅ 학습 목표 :
* 조건문 함수의 기능을 이해하고, 설명할 수 있다. 
~~~

👉 조건문 함수? 
- 조건문 : 특정 조건이 충족되면 → 어떤 행동을 하자 (특정 조건이 참일 때 A, 아닐 때 B)
- ① 조건에 따른 분기 처리가 필요한 경우 ② 조건에 따라 다른 값을 표시하고 싶은 경우 (컬럼 변환 등) 
- CASE WHEN 함수, IF 함수 
- 특정 카테고리를 하나로 합치는 전처리가 필요할 때 조건문 함수를 사용할 수 있음(예시 : 1, 2, 3학년 → 저학년 / 4, 5, 6학년 → 고학년)(월, 화, 수, 목, 금 → 주중 / 토, 일 → 주말) 

👉 CASE WHEN
- 여러 조건이 있을 경우 유용 
- 문법
~~~
SELECT
  CASE
    WHEN 조건 1 THEN 조건1이 참일 경우 결과
    WHEN 조건 2 THEN 조건2가 참일 경우 결과
    ELSE 그 외 조건일 경우 결과
END AS 새로운_컬럼_이름
~~~
- 예시 : 포켓몬 타입 중 Rock(바위) 타입과 Ground(땅) 타입을 묶어서 → Rock&Ground 타입 새로 만들기
~~~
SELECT
  new_type1,
  COUNT(DISTINCTid)AScnt
FROM(
  SELECT
  *,
  CASE
    WHEN(type1IN("Rock","Ground"))OR(type2IN("Rock","Ground"))
    THEN"Rock&Ground"
  ELSEtype1
  ENDASnew_type1
FROMbasic.pokemon
)
GROUPBY
new_type1
~~~
- **조건의 순서**가 매우 중요함 : 처음 조건문에서 처리가 되면 이후는 다시 체크하지 않음 (조건 1, 조건 2 둘 다에 해당하면 앞선 순서를 따름)

👉 IF 
- 단일 조건일 경우 유용 
- 문법 
~~~
IF(조건문, True일 때의 값, False일 때의 값) AS 새로운_컬럼_이름
~~~
- 예시
~~~
SELECT
  IF(1=1, '동일한 결과', '동일하지 않은 결과') AS result1, 
  IF(1=2, '동일한 결과', '동일하지 않은 결과') AS result2
~~~




 # 4-5. 시간 데이터 연습문제 & 4-7. 조건문 연습 문제

~~~
✅ 학습 목표 :
* 4-5, 4-7 각각에서 두 문제 이상 (최소 4문제) 푼 내용 정리하기
~~~

👉 **4-5(1)** : 트레이너가 포켓몬을 포획한 날짜(catch_date)를 기준으로, 2023년 1월에 포획한 포켓몬의 수를 계산해주세요. 
- 풀이 
~~~
SELECT 
  COUNT(DISTINCT id) AS cnt
FROM basic.trainer_pokemon 
WHERE 
  EXTRACT(YEAR FROM DATETIME(catch_datetime, "Asia/Seoul")) = 2023
  AND EXTRACT(MONTH FROM DATETIME(catch_datetime, "Asia/Seoul")) = 1
~~~
- 틀린 부분 : DATETIME(catch_datetime, "Asia/Seoul") ← "Asia/Seoul"을 붙이지 않았음 
- 맞은 부분 : EXTRACT(YEAR FROM~) AND EXTRACT(MONTH FROM~)
- 새롭게 배운 점 : 컬럼 설명을 꼭 확인하고 쿼리 작성하기🤔

👉 **4-5(2)** : 배틀이 일어난 시간(battle_datetime)을 기준으로, 오전 6시에서 오후 6시사이에 일어난 배틀의 수를 계산해주세요.
- 풀이 
~~~
SELECT
  COUNT(DISTINCT id) AS battle_cnt
FROM basic.battle
WHERE 
  EXTRACT(HOUR FROM battle_datetime) >=6
  AND EXTRACT(HOUR FROM battle_datetime) <=18
~~~
- 틀린 부분 :  EXTRACT(HOUR FROM battle_datetime) <=18 ← 오후 6시를 18로 표현해야겠다고 생각하지 못함 
- 맞은 부분 : EXTRACT(HOUR FROM battle_datetime) >=6
- 새롭게 배운 점 : EXTRACT 구문을 두 개 작성하지 않고 'BETWEEN 6 and 18'으로 표현해도 된다😮

👉 **4-7(1)** : 포켓몬의 'speed'가 70 이상이면 '빠름', 그렇지 않으면 '느림'으로 표시하는 새로운 컬럼 'Speed_Category'를 만들어 주세요. 
- 풀이 
~~~
SELECT 
  id,
  kor_name,
  speed, 
  IF(speed>=70, "빠름", "느림") AS Speed_Category
FROM basic.pokemon
~~~
- 틀린 부분 : WHEN으로 풀려고 시도함.. (너무 복잡하게 풀려고 했음) 
- 맞은 부분 : ..😢
- 새롭게 배운 점 : 단일 조건인지 아닌지 파악 잘 하기! 

👉 **4-7(2)** : 각 트레이너 배지 개수(badge_count)를 기준으로, 5개 이하면 'Beginner', 6개에서 8개 사이면 'Intermediate', 그 이상이면 'Advanced'로 분류해주세요. 
- 풀이 
~~~
SELECT
  id,
  name,
  badge_count,
  CASE 
    WHEN badge_count >=9 THEN "Advanced"
    WHEN badge_count BETWEEN 6 AND 8 THEN "Intermediate"
  ELSE "Beginner"
  END AS trainer_level
FROM basic.trainer 
~~~
- 틀린 부분 : badge_count, Advanced, Intermediate 등에 ''를 붙여서 오류가 뜸 
- 맞은 부분 : CASE WHEN 구문을 써서 문제 풀이에 접근함, 'BETWEEN 6 AND 8'를 적절하게 사용함 
- 새롭게 배운 점 : 😀

👉 **4-7(3)** : 트레이너가 포켓몬을 포획한 날짜(catch_date)가 '2023-01-01' 이후이면 'Recent', 그렇지 않으면 'Old'로 분류해주세요.
- 풀이 
~~~
SELECT 
  id,
  trainer_id,
  pokemon_id,
  catch_datetime,
  IF(DATE(catch_datetime, "Asia/Seoul") > "2023-01-01", "Recent", "Old") AS recent_or_old
FROM basic.trainer_pokemon
~~~
- 틀린 부분 : DATE(catch_datetime, "Asia/Seoul") > "2023-01-01" ← 에서 '2023-01-01' 자체를 부등호로 비교할 수 있을 것이라고 생각하지 못함 
- 맞은 부분 : IF 구문을 써서 문제 풀이에 접근함 
- 새롭게 배운 점 : TIMESTAMP, DATETIME 등 시간 데이터 관련해서 조금 더 이해가 필요할 것 같음😱



<br>

<br>

---

# 확인문제

## 문제 1

> **🧚Q. 광윤이는 사용자 로그 데이터에서, 2021년에 접속한 사용자 수를  집계하려고 했습니다. 그는 여러 SQL 쿼리들을 실행해봤지만, 그 중 일부는 문법적으로 잘못되어 실행되지 않았습니다. 다음 보기 중 틀린 쿼리를 모두 골라보세요 (복수 선택 가능)**

~~~sql
1. SELECT COUNT(*)  
   FROM user_log  
   WHERE EXTRACT(YEAR FROM login_date) = 2021;

2. SELECT EXTRACT(YEAR FROM login_date), COUNT(*)  
   FROM user_log  
   GROUP BY EXTRACT(YEAR FROM login_date);

3. SELECT COUNT(*)  
   FROM user_log  
   WHERE login_date = '2021';

4. SELECT COUNT(*)  
   FROM user_log  
   WHERE login_date BETWEEN '2021-01-01' AND '2021-12-31';
~~~

<!-- 틀린쿼리에 대한 오류의 원인도 같이 작성해주세요. 문제에서 제공된 login_data 컬럼은 DATE type의 데이터를 가지고 있다고 가정하시면 됩니다. -->

~~~
* 3번 쿼리 → login_date = '2021'처럼 문자열 '2021'과 날짜 타입을 직접 비교하면, 데이터베이스마다 자동 형 변환이 다르게 이루어져서 원하는 결과가 안 나올 가능성이 높음. 

* 4번 쿼리 → BETWEEN '2021-01-01' AND '2021-12-31'은 login_date가 DATE형이면 괜찮지만, TIMESTAMP형이라면 12월 31일 자정 이후(예: 2021-12-31 23:59:59)는 포함되지 않을 수 있음. 
~~~



## 문제 2

> **🧚Q. 혜성이는 포켓몬 타입에 따라 설명을 부여하는 쿼리를 작성했습니다. type 1 컬럼의 값에 따라 조건을 분기했으며, 다음 SQL 쿼리를 실행했습니다.**

~~~sql
SELECT name,
       CASE 
         WHEN type1 = 'Fire' THEN 'Hot'
         WHEN type1 = 'Water' THEN 'Cool'
         ELSE 'Normal'
       END AS type_description
FROM pokemon;
~~~

> **다음 중 type_description의 결과가 'Normal'로 출력될 포켓몬은?**

| **name**   | **type1** |
| ---------- | --------- |
| Pikachu    | Electric  |
| Charmander | Fire      |
| Squirtle   | Water     |
| Bulbasaur  | Grass     |

<!-- 근거와 함께 답을 작성해주세요 -->

~~~
Pikachu와 Bulbasaur → 'Fire'나 'Water'가 아닌 'Electric'과 'Grass'가 ELSE 조건에 걸리기 때문. 
~~~



<br>

### 🎉 수고하셨습니다.