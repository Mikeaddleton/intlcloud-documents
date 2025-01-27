기본적으로 COS(Cloud Object Storage)의 리소스(버킷 및 객체)는 개인 읽기/쓰기 이며, 객체 URL을 획득하더라도 익명의 사용자는 서명이 없기 때문에 url을 통해 리소스 콘텐츠에 액세스할 수 없습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/fa01129197b8f995eeddf992bd30a13a.png)

## 주요 단계

Tencent Cloud 계정 생성을 시작으로 COS의 권한 및 실명 인증 프로세스는 이 5단계를 거쳐야 합니다. Tencent Cloud 계정 생성, COS 서비스 활성화, 인증 ID 생성, ID에 대한 권한 설정 그리고 액세스 및 실명 인증을 시작합니다. 

![](https://qcloudimg.tencent-cloud.cn/raw/257077f136d7c50be671964140e7996d.png)

#### 1단계: Tencent Cloud 계정 생성

Tencent Cloud 계정 생성 후 귀하의 계정은 루트 계정으로 존재하며 루트 계정이 가장 높은 권한을 가집니다.

#### 2단계: COS 서비스 활성화

COS 서비스 활성화 후 생성하는 모든 버킷은 루트 계정이 소유합니다. 루트 계정은 모든 리소스를 사용할 수 있는 가장 높은 권한을 가지며, 서브 계정을 생성하고 서브 계정을 승인할 수 있는 권한이 있습니다. 

#### 3단계: 인증 ID 생성

>! 버킷이나 객체가 공개 읽기로 개방되어 있지 않는 한 COS에 액세스하려면 실명 인증 절차를 거쳐야 합니다.
>

루트 계정을 통해 여러 ID를 생성하고 리소스마다 다른 사용 권한을 부여할 수 있습니다.

- 회사 동료, 특정 부서의 사용자 등 특정 사용자에게 인증이 필요한 경우 [CAM(Cloud Access Management) 콘솔](https://console.cloud.tencent.com/cam)에서 해당 사용자에 대한 서브 계정을 생성할 수 있습니다. 버킷 정책, 사용자 정책(CAM 정책), 버킷 ACL, 객체 ACL 등 다양한 인증 방법을 통해 서브 계정에 지정된 리소스에 대한 지정된 액세스 권한을 부여합니다.
- 다른 사람이 실명 인증 없이 url을 통해 직접 객체를 다운로드할 수 있도록 하는 등 익명 사용자에게 권한을 부여해야 하는 경우 리소스 권한을 기본 개인 읽기에서 공개 읽기로 수정해야 합니다.
- COS 버킷 사용 시 다른 Tencent Cloud 기타 서비스(예: CDN 등)가 필요한 경우에도 동일한 인증 절차를 따라야 하며, 귀하의 허가가 있는 경우 이러한 서비스는 서비스 역할을 통해 합법적으로 COS에 액세스할 수 있으며 CAM 콘솔에서 생성된 서비스 역할을 조회할 수 있습니다.

교차 Tencent Cloud 계정 인증의 경우 하나의 COS 버킷만 인증하려면, 버킷 정책 또는 버킷 ACL을 통해 다른 루트 계정을 직접 인증할 수 있습니다. 여러 COS 버킷 또는 여러 Tencent Cloud 리소스를 인증해야 하는 경우 [CAM 콘솔](https://console.cloud.tencent.com/cam)을 통해 협업 파트너 ID를 생성하여 더 넓은 범위를 인증할 수 있습니다.

#### 4단계: ID 권한 설정

COS는 [버킷 정책](https://intl.cloud.tencent.com/document/product/436/45235), [사용자 정책(CAM 정책)](https://intl.cloud.tencent.com/document/product/436/45236), [버킷 ACL](https://intl.cloud.tencent.com/document/product/436/30583) 및 [객체 ACL](https://intl.cloud.tencent.com/document/product/436/30583)을 포함한 다양한 권한 설정 방식을 지원하며, 사용 시나리오에 따라 적절한 인증 방식을 선택할 수 있습니다.

#### 5단계: 액세스 및 실명 인증 시작

콘솔, API 요청, SDK 등을 통해 COS에 액세스할 수 있습니다. 보안상의 이유로 버킷은 기본적으로 개인 읽기이며 어떤 방법을 사용하든 실명 인증이 필요합니다. 콘솔의 경우 계정 비밀번호를 사용하여 로그인합니다. API 요청과 SDK 모두에 대해 사용자는 키(SecretId/SecretKey)를 사용하여 실명 인증을 해야 합니다.

## COS 실명 인증 방식

![](https://qcloudimg.tencent-cloud.cn/raw/ec955992e6a0af7e9a01b7fd1e009330.png)

기본적으로 COS 버킷은 비공개이며 키(영구키, 임시키)를 통한 COS에 액세스 또는 사전 서명된 URL을 통한 액세스 모두 실명 인증을 완료해야 합니다. 특별한 경우에는 버킷을 공개 읽기로 개방할 수도 있으나 이는 위험한 작업입니다. 모든 사용자가 실명 인증 없이 객체 URL을 통해 직접 객체를 다운로드할 수 있습니다.

### 1. 영구 키를 사용하여 액세스

키(SecretId/SecretKey)는 사용자가 Tencent Cloud API에 액세스 시 인증할 때 사용하는 보안 자격 증명으로 [API 키 관리](https://console.cloud.tencent.com/cam/capi)에서 획득할 수 있습니다. 각 루트 계정과 서브 계정은 여러 개의 키를 생성할 수 있습니다.

![](https://qcloudimg.tencent-cloud.cn/raw/6b2eac5ee953de3ace61b954e12c0cf2.png)

영구 키는 SecretId와 SecretKey를 포함합니다. 각 루트 계정과 서브 계정은 두 쌍의 영구 키를 생성할 수 있습니다. 영구 키는 계정의 영구 ID를 나타내며 삭제하지 않으면 오랫동안 유효합니다. 자세한 내용은 [영구 키를 사용하여 COS 액세스](https://intl.cloud.tencent.com/document/product/436/45241)를 참고하십시오.

### 2. 임시 키를 사용하여 액세스

임시 키는 SecretId, SecretKey 및 Token을 포함하며, 각 루트 계정과 서브 계정은 여러 개의 임시 키를 생성할 수 있습니다. 임시 키는 영구 키에 비해 유효 기간이 있으며(기본 1800초) 최대 유효 기간은 루트 계정 7200초, 서브 계정 129600초로 설정할 수 있습니다. 자세한 내용은 연합 ID 임시 액세스 자격 증명 획득을 참고하십시오.

임시 키는 프런트 엔드 직접 전송과 같은 임시 인증 시나리오에 적합하며 영구 키에 비해 신뢰할 수 없는 사용자에게 임시 키를 배포하는 것이 더 안전합니다. 자세한 내용은 [임시 키를 사용하여 COS 액세스](https://intl.cloud.tencent.com/document/product/436/45242)를 참고하십시오.

### 3. 임시 URL(사전 서명된 URL)을 사용하여 액세스

자세한 내용 및 사용 설명은 [사전 서명된 URL을 사용하여 COS 액세스](https://intl.cloud.tencent.com/document/product/436/45243)를 참고하십시오.

#### 객체 다운로드

타사가 버킷에서 객체를 다운로드할 수 있지만 상대방의 CAM 계정 또는 임시 키 사용을 제한하고 싶은 경우, URL 사전 서명 방식으로 타사에 서명을 제출함으로써 임시 다운로드 작업을 완료할 수 있습니다. 유효한 URL 사전 서명을 받은 계정은 모두 객체 다운로드를 진행할 수 있습니다.

- 콘솔 또는 COSBrowser에서 임시 다운로드 링크 가져오기(1 - 2시간 동안 유효)
콘솔이나 COSBrowser에서 직접 객체의 임시 다운로드 링크를 빠르게 가져올 수 있으며, 브라우저에 직접 임시 링크를 입력하여 객체를 다운로드할 수 있습니다. 자세한 내용은 [임시 링크 빠르게 획득](https://intl.cloud.tencent.com/document/product/436/45243) 문서를 참고하십시오.
<span id="SDK 사용하여 사전 서명 url 생성"></span> 
- SDK 사용하여 사전 서명 url 생성
SDK를 사용하면 사용자 정의 유효 기간이 있는 사전 서명된 URL을 일괄적으로 가져올 수 있으며, 자세한 내용은 [SDK 사용하여 사전 서명된 URL 일괄 가져오기](https://intl.cloud.tencent.com/document/product/436/45243) 문서를 참고하십시오.
- 서명 툴을 사용하여 사전 서명된 URL 생성
프로그래밍에 익숙하지 않은 사용자에게 적합한 사용자 정의 유효 기간의 사전 서명 URL 가져오기 입니다. 자세한 내용은 서명 툴 사용 문서를 참고하십시오.
- 서명 링크 자체 스티칭 
사전 서명된 URL은 실제로 객체 URL 뒤에 스티칭되는 서명입니다. 따라서 SDK, 서명 생성 툴 등을 통해 직접 서명을 생성하고 URL과 서명을 서명 링크로 스티칭할 수도 있습니다. 그러나 서명 생성 알고리즘의 복잡성으로 인해 이 사용 방식은 일반적으로 권장되지 않습니다.

#### 객체 업로드

서드 파티가 버킷에 객체를 업로드할 수 있지만 CAM 계정 혹은 임시 키 사용을 원치 않는 경우 임시 업로드 작업을 완료하기 위해 URL 사전 서명을 사용해 서드 파티에게 서명을 제출합니다. 유효한 서명 URL을 받은 계정은 모두 객체 업로드를 진행할 수 있습니다.

- 방법1: SDK를 사용하여 사전 서명된 URL 생성
각 언어 SDK는 사전 서명된 URL을 생성하고 업로드하는 방법을 제공하며, 생성 방법은 [사전 서명된 인증 업로드](https://intl.cloud.tencent.com/document/product/436/14114)를 참고하여 익숙한 개발 언어를 선택하십시오.
- 방법2: 서명 링크 자체 접합
사전 서명된 URL은 실제로 객체 URL 뒤에 스티칭되는 서명입니다. 따라서 SDK, 서명 생성 툴 등을 통해 직접 서명을 생성하고 URL과 서명을 서명 링크로 스티칭하여 객체 업로드를 할 수도 있습니다. 그러나 서명 생성 알고리즘의 복잡성으로 인해 이 사용 방식은 일반적으로 권장되지 않습니다.

### 4. 익명 액세스

기본적으로 COS 버킷은 비공개로 되어 있으며, 키(영구 키, 임시 키)를 통한 COS 액세스 또는 사전 서명된 URL을 통한 액세스 모두 실명 인증 절차를 거쳐야 합니다.

특별한 필요에 의해 버킷이나 객체를 공개 읽기로 개방할 수도 있으며 모든 사용자는 실명 인증 없이 객체 URL을 통해 객체를 직접 다운로드할 수 있습니다.

>! 리소스를 공개 읽기로 개방하는 것은 보안상 위험하며, 리소스 링크가 유출되면 누구나 액세스할 수 있어 악의적인 사용자에게 트래픽을 도난당할 수 있습니다.
>

#### 공개 읽기로 버킷 개방

콘솔에서 전체 버킷을 공개 읽기로 설정할 수 있습니다. 이 경우 버킷의 각 객체는 모두 객체 URL을 통해 직접 다운로드될 수 있습니다. 설정 방법은 [버킷 액세스 권한 설정](https://intl.cloud.tencent.com/document/product/436/13315)을 참고하십시오.

#### 공개 읽기로 객체 개방

콘솔에서 개별 객체를 공개 읽기로 설정할 수 있습니다. 이 경우 URL을 통해 그 객체만 직접 다운로드될 수 있으며 다른 객체는 영향을 받지 않습니다. 설정 방법은 [객체 액세스 권한 설정](https://intl.cloud.tencent.com/document/product/436/13327)을 참고하십시오.

#### 폴더를 공개 읽기로 개방

콘솔에서 폴더를 공개 읽기로 설정할 수 있습니다. 이 경우 폴더 아래의 모든 객체는 URL을 통해 직접 다운로드될 수 있으며 폴더 외부의 객체는 영향을 받지 않습니다. 설정 방법은 [폴더 권한 설정](https://intl.cloud.tencent.com/document/product/436/35261)을 참고하십시오.

