TencentDB for MySQL 데이터베이스 프록시는 연결 풀 기능을 지원합니다. 현재 지원되는 데이터베이스 프록시 연결 풀 기능은 세션 수준 연결 풀로, 짧은 연결 서비스를 위한 새로운 빈번한 비지속 연결로 인한 과도한 인스턴스 로드 문제를 효과적으로 해결할 수 있습니다. 본 문서에서는 세션 수준 연결 풀 기능을 소개합니다.

## 전제 조건
[데이터베이스 프록시 활성화](https://intl.cloud.tencent.com/document/product/236/42052)가 완료 되어 있어야 합니다.

## 배경 정보
#### 세션 수준 연결 풀
![](https://qcloudimg.tencent-cloud.cn/raw/f708a404a68e16abb747e1088ce14ba6.png)
세션 수준 연결 풀은 비지속 연결 시나리오에 적합합니다.

세션 수준 연결 풀은 주로 짧은 연결 서비스에 대한 새 연결의 빈번한 설정으로 인해 발생하는 인스턴스 부하를 줄이는 데 사용됩니다. 클라이언트 연결이 끊어지면 시스템은 현재 연결이 유휴 연결인지 확인하고, 유휴 연결이면 시스템은 해당 연결을 프록시의 연결 풀에 넣고 잠시 동안 보관합니다(시스템 기본값은 5초이며 [연결 유지 임계값 설정](https://intl.cloud.tencent.com/document/product/236/45623)을 지원합니다).
클라이언트가 새 연결을 다시 제안할 때 연결 풀에 사용 가능한 연결이 있으면 직접 사용할 수 있으므로 데이터베이스와의 연결 설정 비용이 감소합니다. 연결 풀에서 사용할 수 있는 유휴 연결이 없는 경우 일반적인 연결 프로세스를 수행하고 데이터베이스와의 새로운 연결을 다시 생성합니다.

>?
>- 세션 수준 연결 풀은 데이터베이스에 대한 동시 접속 수를 감소시키지 않지만 애플리케이션이 데이터베이스에 연결하는 속도를 감소시켜 MySQL 메인 스레드의 비용을 줄이고 서비스 요청을 더 잘 처리합니다. 그러나 연결 풀의 유휴 연결은 연결 수를 일시적으로 차지합니다.
>- 세션 수준 연결 풀은 많은 수의 느린 SQL로 인해 발생하는 연결 힙 문제를 해결할 수 없으므로 먼저 느린 SQL 문제를 해결해야 합니다.

## 주의 사항
- 현재 연결 풀 기능은 동일한 계정의 IP에 대한 다른 권한을 지원하지 않습니다. 연결 다중화 시 권한 오류가 발생할 수 있습니다. 예를 들어 mt@test123은 database_a의 권한을 설정하지만 mt@test456은 database_a의 권한을 가지고 있지 않기 때문에 연결 풀을 활성화하면 권한 오류가 발생할 수 있습니다.
- 연결 풀 기능이란 데이터베이스 프록시의 연결 풀 기능으로서 클라이언트의 연결 풀 기능에 영향을 미치지 않습니다. 클라이언트가 이미 연결 풀을 지원한다면 데이터베이스 프록시의 연결 풀 기능을 사용하지 않아도 됩니다.

