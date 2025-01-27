## 확인 사항

### MySQL/TDSQL-C MySQL/TDSQL MySQL/PostgreSQL 확인 요건

- 대상 데이터베이스는 원본 데이터베이스의 객체와 이름이 같은 객체를 가질 수 없습니다. 충돌로 인해 오류가 발생하는 경우 다음 방법 중 하나로 수정할 수 있습니다.
   - [방법1: 데이터베이스/테이블 매핑 사용(MySQL 전용)](#1). 
   - [방법2: 대상 데이터베이스에서 이름이 같은 객체의 이름 수정 또는 삭제](#2).
   - [방법3: 마이그레이션 객체에서 이름이 같은 객체 제거](#3).
- 대상 데이터베이스는 비어 있어야 합니다. 충돌로 인해 오류가 발생하면 데이터베이스 콘텐츠를 삭제해야 합니다.

### MongoDB 확인 요건

대상 데이터베이스에는 원본 데이터베이스와 동일한 이름을 가진 테이블이 있을 수 있지만 빈 테이블이어야 합니다. 충돌로 인해 오류가 발생하는 경우 다음 방법 중 하나로 수정할 수 있습니다.

- 방법1: 대상 데이터베이스에서 이름이 같은 테이블을 삭제하거나 데이터를 지웁니다.
- [방법2: 마이그레이션 객체에서 이름이 같은 객체 제거](#3).

### SQL Server 확인 요건

대상 데이터베이스는 원본 데이터베이스와 동일한 이름을 가진 데이터베이스를 가질 수 없습니다. 그렇지 않으면 오류가 보고됩니다.

오류가 보고되면 대상 데이터베이스에서 동일한 이름을 가진 데이터베이스를 삭제하거나 이름을 바꿔야 합니다.

## 수정 방법

### [테이블 매핑 사용(MySQL 전용)](id:1)
DTS 테이블 매핑 기능을 사용하여 동일한 이름으로 마이그레이션할 객체의 이름을 대상 데이터베이스의 다른 이름에 매핑할 수 있습니다. 
1. [DTS 콘솔](https://console.cloud.tencent.com/dts/migration)에 로그인하고 해당 마이그레이션 작업을 선택한 다음 **작업** 열에서 **더보기** > **수정**을 클릭합니다. 
2. 오른쪽의 ‘선택된 객체’에서 수정할 객체 위로 마우스를 가져간 후 표시된 편집 아이콘을 클릭하고 객체의 이름을 바꿉니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c89be2f80c4c4c7bc53858cb8bc24ccc.png)
3. 확인 작업을 다시 실행합니다.

### [대상 데이터베이스에서 동일한 이름의 객체 수정](id:2)
대상 데이터베이스에 로그인하고 마이그레이션 객체와 이름이 같은 객체의 이름을 바꾸거나 삭제합니다.

### [마이그레이션 객체에서 동일한 이름을 가진 객체 제거](id:3)
마이그레이션 작업 구성을 수정하여 마이그레이션 객체에서 동일한 이름을 가진 객체를 제거합니다. 제거된 객체는 마이그레이션할 수 없습니다.
1. [DTS 콘솔](https://console.cloud.tencent.com/dts/migration)에 로그인하고 해당 마이그레이션 작업을 선택한 다음 **작업** 열에서 **더보기** > **수정**을 클릭합니다. 
2. 마이그레이션 객체에서 이름이 같은 객체를 제거합니다.
3. 확인 작업을 다시 실행합니다. 

### 대상 데이터베이스 콘텐츠 삭제
대상 데이터베이스에 로그인하여 원본 데이터베이스와 동일한 이름의 객체를 삭제하고 확인 작업을 다시 실행합니다.

