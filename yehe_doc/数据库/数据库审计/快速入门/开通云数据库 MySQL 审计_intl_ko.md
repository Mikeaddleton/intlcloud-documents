Tencent Cloud는 TencentDB for MySQL 데이터베이스 감사 기능을 제공하여 데이터베이스 액세스 및 SQL 명령어 실행 상황을 기록하고, 기업의 리스크 관리와 데이터 보안 등급 향상에 이바지합니다.  

>!TencentDB for MySQL 5.6、5.7 이중 노드 및 삼중 노드 데이터베이스 감사 기능 지원. TencentDB for MySQL 5.5 버전 및 TencentDB for MySQL 단일 노드 미지원.

## 감사 작업
### 감사 규칙 생성
1. [MySQL 콘솔](https://console.cloud.tencent.com/dls/mysql) 로그인，왼쪽 메뉴에서 [데이터베이스 감사] 선택，상단의 리전 선택 후, [감사 규칙] 선택.
2. 감사 규칙 페이지에서 [규칙 생성] 클릭.
![](https://main.qcloudimg.com/raw/c4e92d4471a82b2c38d1bc78d8995044.png)
3. 감사 규칙 생성 페이지에서 규칙 명칭, 설명 기입 후, [다음 단계] 클릭.
4. 매개변수 설정 페이지에서 감사 방식 및 매개변수 선택 후, [저장] 클릭.
>?규칙 생성 완료 후, 감사 정책과 연결해야 규칙 적용됨.
>
![](https://main.qcloudimg.com/raw/b6059e729814c6f585f9098370f5eef0.png)

### SQL 감사 서비스 활성화
1. [MySQL 콘솔](https://console.cloud.tencent.com/dls/mysql) 로그인，좌측 메뉴에서 [데이터베이스 감사] 선택，상단의 리전 선택 후, [감사 정책] 선택.
2. 감사 정책 페이지에서 감사 대상 데이터베이스 인스턴스, 해당 프로토콜 선택 후, [다음 단계] 클릭.
![](https://main.qcloudimg.com/raw/f80b3ed667734c9aa1b00838a73fada0.png)
3. SQL 감사 서비스 설정 페이지에서 감사 저장 기간 선택 후, [다음 단계] 클릭.
>!SQL 로그 저장 기간에 대한 보안 컴플라이언스 요구 사항을 충족하기 위해, 180일 이상으로 선택할 것을 권고함.
4. 정책 생성 페이지에서 정책 명칭을 설정하고, 감사 규칙 선택 후, [정책 생성] 클릭.

### 감사 정책 생성
1. [MySQL 콘솔](https://console.cloud.tencent.com/dls/mysql) 로그인，좌측 메뉴에서 [데이터베이스 감사] 선택，상단의 리전 선택 후, [감사 정책] 선택
2. 감사 정책 페이지에서 [정책 생성] 클릭.
![](https://main.qcloudimg.com/raw/9713931fcbd22e2f47d31b764c2d09c4.png)
3. 팝업 대화창에서 정책 명칭을 설정하고, 감사 규칙 선택 후, [확인] 클릭. 

### 감사 로그 조회
1. [MySQL 콘솔](https://console.cloud.tencent.com/dls/mysql) 로그인 후，좌측 메뉴에서 [데이터베이스 감사] 선택，상단의 리전 선택 후, [감사 로그] 선택.
2. ‘감사 인스턴스’에서 이미 감사를 활성화한 데이터베이스 인스턴스를 선택하면 해당 SQL 감사 로그 조회 가능.  
 - ‘시간창’ 클릭 후, 시간대를 선택하면 해당 시간대의 감사 결과 조회 가능.
 - ‘텍스트창’에서 키 태그로 검색하면 감사 결과 조회 가능. SQL 키 명령어 조합하여 검색하면 감사 결과 조회 가능.
>?
>- ‘텍스트창’에서 여러 키 태그 입력 및 검색 시, 엔터 키를 눌러 키 태그 분할 가능.
>- ‘텍스트창’에 SQL 명령어, 클라이언트 IP, 계정, 데이터베이스, 객체명, 정책명, 실행 시간 범위，영향을 받는 행의 수 등 주요 값 조합하여 입력 가능.
>
![](https://main.qcloudimg.com/raw/33443b0991fb282782cf054d0cba0812.png)

## SQL 감사 필드
TencentDB for MySQL의 감사 로그는 다음 필드를 지원합니다. 사용자는 [MySQL 콘솔](http://console. cloud. tencent. com/dls/mysql)의 [감사 로그] 페이지에서 아래와 같은 아이콘을 클릭하면 전체 SQL 감사 로그를 조회할 수 있습니다.
![](https://main.qcloudimg.com/raw/a504bd3353af1c0fce27b223bda0003c.png)



| 시리얼 넘버 | 필드 이름 | 필드 의미                                                         | 비고                                         |
| ---- | ------------- | ------------------------------------------------------------ | -------------------------------------- |
| 1            | host     |클라이언트 IP                                           |   -                                           |
| 2            |dbname   | 데이터베이스 이름                                                 |  -                                            |
| 3            |user       | 사용자 이름                                                    |      -                                        |
| 4            | sql        | SQL 명령                                             |    -                                          |
| 5            | sqlType    | SQL 명령 유형                                          |   -                                           |
| 6    | errCode       | 에러 코드                                                | 0은 성공을 의미함                           |
| 7    | affectRows    | 영향받는 행의 수                                                    |     -                                       
| 8    | checkRows     | 스캔된 행의 수                                                     |     -                                         |
| 9    | sentRows      | 반환된 행의 수                                                     |    -                                          |
| 10   | threadId      | 스레드 ID                                                       |       -                                       |
| 11   | ruleNum       | 감사 규칙 번호                                                 |     -                                         |
| 12   | policyName    | 감사 정책 이름                                                   |    -                                          |
| 13   | instanceName  | 인스턴스 이름                                                       |    -                                          |
| 14   | timestamp     | 시작 시간 (초)                                               |   -                                           |
| 15   | nsTime        | 시작 시간 (나노 초). timestamp와 조합하여 시작 시간을 나노 초 단위까지 표기 가능 | 예시 timestamp.nsTime 1577953020.887984015 |
| 16   | execTime      | 실행 시간 (마이크로 초)                                             |    -                                          |
| 17   | cpuTime       | CPU 시간 (나노 초)                                              |     -                                         |
| 18   | lockWaitTime  | 잠금 대기 시간（마이크로 초）                                           |    -                                          |
| 19   | ioWaitTime    | IO 대기 시간（마이크로 초）                                           |     -                                         |
| 20   | trxLivingTime | 트랜잭션 실행 시간 (마이크로 초）                                   |      -                                        |

## SQL 감사 규칙
### 규칙 내용
지원하는 설정은 다음과 같습니다. 
클라이언트 IP, 데이터베이스 계정, 데이터베이스 이름, [포함, 불포함, 같음, 다름] 방식의 매칭을 지원합니다. 

전수 감사 규칙은 특수 규칙으로, 활성화하면 모든 명령을 감사합니다.

## 규칙 연산
- 모든 규칙 내부의 유형은 조건 추가 제한 관계로 and (&&) 관계입니다.
예를 들어 사용자 이름은 user1, 매칭 유형은 같음으로 지정하고, 데이터베이스 이름은 test, 매칭 유형은 같음으로 지정하면 user1 사용자의 test 라이브러리에 대한 작업만 감사하고 나머지는 무시합니다.
- 규칙과 규칙 간에는 or (||) 관계입니다.
모든 인스턴스는 하나 혹은 다수의 감사 규칙을 지정할 수 있으며 어느 한 규칙에만 부합해도 감사가 진행됩니다. 예를 들어 A 규칙으로 user1의 실행 시간이 1초와 같거나 이상인 작업만 감사하도록 지정하고 B 규칙으로 user1과  실행 시간이 &lt; 1인 명령을 감사하라고 한 경우, 결국 user1의 모든 명령에 감사가 진행됩니다.

### 규칙 상세 설명
클라이언트 IP, 데이터베이스 계정, 데이터베이스 이름이 [포함, 불포함, 같음, 다름]을 지원하는 것과 관련하여 ‘다름’ 처럼 한 번에 하나의 오퍼레이터 설정만 가능합니다.
‘같음’과 ‘다름’의 경우 다수의 값을 쓸 수 있으며 쉼표로 구분할 수 있습니다. 포함, 불포함의 경우 하나의 값만 쓸 수 있습니다. 예를 들어 오퍼레이터가 ‘같음’인 경우 user1, user2, user3의 값을 지정할 수 있습니다.

#### 데이터베이스 이름 관련 설명
다음 테이블 객체 유형의 명령에 해당하는 경우:
```
SQLCOM_SELECT, SQLCOM_CREATE_TABLE, SQLCOM_CREATE_INDEX, SQLCOM_ALTER_TABLE,
SQLCOM_UPDATE, SQLCOM_INSERT, SQLCOM_INSERT_SELECT, SQLCOM_DELETE, SQLCOM_TRUNCATE, SQLCOM_DROP_TABLE
```
이런 유형의 동작에 있어서 데이터베이스 이름은 명령 중 실제 작업하는 데이터베이스 이름을 기준으로 합니다. 예를 들어 현재 use db3인 경우 명령어는 다음과 같습니다.
```
select *from db1.test,db2.test;
```
db1과 db2를 타깃 라이브러리로 하여 규칙 판단을 하고 규칙에 db1 CFA 설정이 있다면 감사를 진행합니다. db3 CFA 설정이 있다 해도 감사를 진행하지 않습니다.
상기 테이블 객체 유형의 명령이 아닌 경우, 현재 use 라이브러리를 타깃 라이브러리로 인식하고 판단합니다. 현재 라이브러리가 use db1이고 실행 명령이 `show databases`인 경우, 현재 라이브러리 db1을 타깃 라이브러리로 하여 규칙 판단을 하며 규칙에 db1 CFA 설정이 있다면 감사를 진행합니다.

### 특이 사항
포함, 불포함은 하나의 값만 쓸 수 있습니다. 여러 값을 쓸 경우 하나의 열로 인식되어 매칭 오류가 발생할 수 있습니다.

