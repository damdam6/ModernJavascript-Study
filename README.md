# ModernJavascript-Study
<br>

## ✔ Info

### 📕 Book

<img src="https://github.com/damdam6/ModernJavascript-Study/assets/47710007/9aba00f7-f3cd-46e2-b0b8-88edbe827002" width="300">
<br>
<br>

### 🧑‍🤝‍🧑 Members

|<img src="https://avatars.githubusercontent.com/u/47710007?v=4" width="150"> |<img src="https://avatars.githubusercontent.com/u/80046476?v=4"  width="150">|<img src="https://avatars.githubusercontent.com/u/139521783?v=4"  width="150">| <img src="https://avatars.githubusercontent.com/u/135293451?v=4" width="150">| <img src="https://avatars.githubusercontent.com/u/73322485?v=4" width="150"> |
|:---:|:---:|:---:|:---:|:---:|
|[damdam6](https://github.com/damdam6)|[gabalja](https://github.com/gabalja) | [sgryu23](https://github.com/sgryu23) | [HunTeac](https://github.com/HunTeac) |[zoowb](https://github.com/zoowb) |
|이담비|손의성|류승광|한재훈|최지우|

<br>

---
<br>


## 📢 Convention

### 💡 참여 방식

#### 1. git 운영 방식
- 저장소를 `fork`한 후, 각자의 레포지토리에서 작업을 진행합니다.
- 각자 원하는 주제를 선정하여 주차별 mm공지에 공유합니다. (서로 다른 주제 선정을 원칙으로 합니다.)
- 매주 `week00` 폴더에 본인의 `username`에 해당하는 폴더를 생성합니다. 이 폴더 안에서 자신이 공부한 파일을 업로드합니다.
- 파일 형식은 `.txt` 혹은 `.md`로 하며, 파일 이름은 공부한 주제에 맞추어 작성합니다.

#### 2. 주간 제출 파일 목록 <br>
- `week00/user-name/study-title` : 필수
- `week00/quiz/quiz` : 해당 주차 담당자
- `week00/quiz/answer` : 해당 주차 담당자
<br>


### 💡 제출 규칙

**1. 커밋 규칙**
```
<tag>(<week>):<study-title>
```
예시 :
``` 
feat(week01):변수 호이스팅 장단점
```
|tag | 설명 |
|---|---|
| feat | 새로운 기능을 추가하는 경우 | 
fix | 버그를 고친경우
docs | 문서를 수정한 경우(READ.md 등)
chore | 빌드 업무 수정, 패키지 매니저 수정
rename | 파일명(or 폴더명) 을 수정한 경우
remove | 코드(파일) 의 삭제가 있을 때

<br>

**2. PR 규칙**

```
<week> <user_name> PR
```
예시 :
``` 
week01 damdam6 PR
```
<br>

**3. 제출 기한**
  * 일요일 23:59까지 제출
  * 벌금 : 미제출 시 5000원
  * 벌금은 추후 기프티콘으로 1/n합니다.
    <br>
***

### 🔎 폴더 구조

 ```
 .
 ├── week01
 │   ├── quiz
 │   |   ├── quiz.txt(md)
 │   │   └── answer.txt(md)
 │   ├── user-name-1
 │   |   ├── study-title.md
 │   │   └── study-title.txt
 │   └── user-name-2
 │       └── study-title-2.md
 └── week02
     ├── quiz
     |   ├── quiz.txt(md)
     │   └── answer.txt(md)
     ├── user-name-1
     │   └── study-title.txt
     └── user-name-2
         ├── study-title.txt
         └── study-title-2.md
 ```

***

## 📢 진도

| 주차(일정) | 진도(교재 범위) | quiz 담당자 |
|---|---|---|
|  | 공부 주제 | 담당자 |
||||
|**week01**<br>(24.01.08 ~ 24.01.14)|04장 변수 ~ 06장 데이터 타입 <br> 34p ~ 73p|**damdam6**|
||동적 타입 언어와 타입스크립트|damdam6|
|| 변수 호이스팅 |gabalja|
||표현식|sgryu23|
||표현식과 문 리터럴 |HunTeac|
||변수 - 값의 재할당|zoowb|
||||
|**week02**<br>(24.01.15 ~ 24.01.21)|07장 연산자 ~ 09장 타입변환과 단축 평가 <br> 74p ~ 123p|**gabalja**|
||Object.is와 === 연산자 비교|damdam6|
||단축평가|gabalja|
||반복문|sgryu23|
||가독성 좋은 조건문 작성 방법|HunTeac|
||암묵적 타입 변환|zoowb|
||||
|**week03**<br>(24.01.22 ~ 24.01.28)|10장 연산자 ~ 12장 함수 <br> 124p ~ 188p|**sgryu23**|
||함수 선언문vs함수 표현식(airbnb가이드)|damdam6|
||유사배열객체|gabalja|
||함수 정의|sgryu23|
||다양한 함수의 형태|HunTeac|
||암묵적 타입 변환|zoowb|
||||
|**week04**<br>(24.01.29 ~ 24.02.04)|13장 스코프 ~ 16장 프로퍼티 어트리뷰트 <br> 189p ~ 233p|**HunTeac**|
||-|damdam6|
||유사배열객체|gabalja|
||함수 정의|sgryu23|
||-|HunTeac|
||암묵적 타입 변환|zoowb|
||||
|**week05**<br>(24.02.13 ~ 24.02.18)|17장 생성자 함수에 의한 객체 생성 ~ 19장 프로토타입 <br> 234p ~ 312p|**HunTeac**|
||프로퍼티 명확히 하기 |damdam6|
||-|gabalja|
|| 프로토타입 객체 |sgryu23|
||-|HunTeac|
||- |zoowb|
||||
