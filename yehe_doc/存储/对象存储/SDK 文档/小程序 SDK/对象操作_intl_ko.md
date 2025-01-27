## 소개

본 문서는 간단한 객체 작업, 기타 작업과 관련된 API 개요 및 SDK 예시 코드에 대해 설명하며, 예시를 통해 사용 방법을 제시합니다.

**간단한 작업**

| API                                                          | 작업명         | 작업 설명                             |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [GET Bucket(List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | 객체 쿼리   | 버킷의 일부 또는 모든 객체를 쿼리합니다.           |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | 객체 업로드   | 버킷에 객체를 업로드합니다.                     |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | 폼을 사용한 객체 업로드   | 폼을 사용한 객체 업로드 요청                     |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | 객체 메타데이터 쿼리 | 객체의 메타데이터를 쿼리합니다.                     |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | 객체 다운로드       | 객체 다운로드                             |
| [OPTIONS Object](https://intl.cloud.tencent.com/document/product/436/8288) | CORS(Cross-Origin Resource Sharing) 구성 확인 | 실제 CORS 요청을 보낼 수 있는지 여부를 확인하기 위해 실행 전 요청을 보냅니다. |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | 객체 복사       | 대상 경로(객체 키)에 객체를 복사합니다.             |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 객체 삭제   | 버킷에서 객체를 삭제합니다.                   |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | 다수의 객체 삭제   | 버킷에서 다수의 객체를 삭제합니다.                   |

**멀티파트 작업**

| API                                                          | 작업명         | 작업 설명                             |
| :----------------------------------------------------------- | :------------- | :----------------------------------- |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | 멀티파트 업로드 쿼리   | 진행 중인 멀티파트 업로드를 쿼리합니다.         |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | 멀티파트 업로드 초기화 | 멀티파트 업로드를 초기화합니다.                   |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | 파트로 객체 업로드       | 객체를 파트로 업로드합니다.                         |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | 객체 파트 복사       | 객체의 파트를 복사합니다.             |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | 업로드된 파트 쿼리   | 지정된 멀티파트 업로드의 업로드된 파트를 쿼리합니다.     |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | 멀티파트 업로드 완료   | 객체의 멀티파트 업로드를 완료합니다.               |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | 멀티파트 업로드 중단 | 멀티파트 업로드를 중단하고 업로드된 부분을 삭제합니다. |


**기타 작업**

| API                                                          | 작업명       | 작업 설명                           |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | 아카이브된 객체 복원 | 액세스를 위해 보관된 객체를 복원합니다.           |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | 객체 ACL 설정 | 버킷의 객체에 대한 ACL 설정 |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | 객체 ACL 쿼리 | 객체의 ACL을 쿼리합니다.             |

## 간단한 작업

### 객체 리스트 쿼리

#### 기능 설명

버킷의 일부 또는 모든 객체를 쿼리합니다.

#### 사용 예시

예시1: 디렉터리 a의 모든 파일 나열.

[//]: # (.cssg-snippet-get-bucket)
```js
cos.getBucket({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'ap-beijing',     /* 필수 */
    Prefix: ’a/’,           /* 옵션 */
}, function(err, data) {
    console.log(err || data.Contents);
});
```

반환 값 형식:

```json
{
    "Name": "examplebucket-1250000000",
    "Prefix": "",
    "Marker": "a/",
    "MaxKeys": "1000",
    "Delimiter": "",
    "IsTruncated": "false",
    "Contents": [{
        "Key": "a/3mb.zip",
        "LastModified": "2018-10-18T07:08:03.000Z",
        "ETag": "\"05a9a30179f3db7b63136f30aa6aacae-3\"",
        "Size": "3145728",
        "Owner": {
            "ID": "1250000000",
            "DisplayName": "1250000000"
        },
        "StorageClass": "STANDARD"
    }],
    "statusCode": 200,
    "headers": {}
}
```

예시2: 깊은 순회 없이 디렉터리의 파일 나열.

[//]: # (.cssg-snippet-get-bucket-with-delimiter)
```js
cos.getBucket({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Prefix: ’a/’,              /* 옵션 */
    Delimiter: ’/’,            /* 옵션 */
}, function(err, data) {
    console.log(err || data.CommonPrefixes);
});
```

반환 값 형식:

```json
{
    "Name": "examplebucket-1250000000",
    "Prefix": "a/",
    "Marker": "",
    "MaxKeys": "1000",
    "Delimiter": "/",
    "IsTruncated": "false",
    "CommonPrefixes": [{
        "Prefix": "a/1/"
    }],
    "Contents": [{
        "Key": "a/3mb.zip",
        "LastModified": "2018-10-18T07:08:03.000Z",
        "ETag": "\"05a9a30179f3db7b63136f30aa6aacae-3\"",
        "Size": "3145728",
        "Owner": {
            "ID": "1250000000",
            "DisplayName": "1250000000"
        },
        "StorageClass": "STANDARD"
    }],
    "statusCode": 200,
    "headers": {}
}
```

예시3: 디렉터리의 모든 파일 나열.

```js
var bucket = ’examplebucket-1250000000’;
var region = ’ap-beijing’;
var prefix = ’examplefolder/’;  /* 삭제할 디렉터리 또는 접두사 */
var listFolder = function(marker) {
    cos.getBucket({
        Bucket: bucket,
        Region: region,
        Prefix: prefix,
        Marker: marker,
        MaxKeys: 1000,
    }, function(err, data) {
        if (err) {
            return console.log(’list error:’, err);
        } else {
            console.log(’list result:’, data.Contents);
            if (data.IsTruncated === ’true’) listFolder(data.NextMarker);
            else return console.log(’list complete’);
        }
    });
};
listFolder();
```

#### 매개변수 설명

| 매개변수 이름       | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket       | BucketName-APPID 형식의 버킷 이름 | String | Yes    |
| Region       | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String      | Yes   |
| Prefix       | 객체 키의 접두사 매칭. 지정된 접두사를 포함한 객체 키만 한정하여 반환합니다.             | String | No   |
| Delimiter    | 구분 문자. 세퍼레이터로 객체 키를 그룹화하는 데 사용하며, 보통 `/`로 표시합니다. 모든 객체 키는 Prefix 또는 처음(Prefix 미지정 시)부터 첫 번째 delimiter 사이의 동일한 경로를 하나로 분류하고 Common Prefix로 정의하여, 모든 Common Prefix를 열거합니다. | String | No   |
| Marker       | 시작하는 객체 키를 표시. 해당 표기 다음부터(해당 표기 불포함) UTF-8 사전 순서에 따라 객체 키 항목을 반환합니다. | String | No   |
| MaxKeys      | 단일 응답에서 반환되는 최대 항목 수입니다. 기본값은 1000입니다.                 | String | No   |
| EncodingType | 반환된 값의 인코딩 방법을 나타냅니다. 유효한 값: url, 반환된 객체 키가 URL 인코딩(백분율 인코딩) 값임을 의미합니다. 예를 들어 "Tencent Cloud"는 `%E8%85%BE%E8%AE%AF%E4%BA%91`로 인코딩됩니다. | String | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름            | 매개변수 설명                                                     | 유형        |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err               | 오류(네트워크 오류 또는 서비스 오류)가 발생하면 반환되는 객체입니다. 요청이 성공하면 이 매개변수가 비어 있게 됩니다. 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | Object      |
| - statusCode      | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers         | 헤더                                           | Object      |
| data              | 요청이 성공하면 반환되는 객체입니다. 요청이 실패하면 이 매개변수는 비어 있습니다.               | Object      |
| - headers         | 헤더                                           | Object      |
| - statusCode      | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - Name            | BucketName-APPID 형식의 버킷 이름(예: examplebucket-1250000000) | String      |
| - Prefix          | 객체가 쿼리되는 키 접두사 반환된 객체는 접두사 뒤에 있는 키의 UTF-8 사전순으로 나열됩니다. | String      |
| - Marker          | 시작하는 객체 키를 표시. 해당 표기 다음부터(해당 표기 불포함) UTF-8 사전 순서에 따라 객체 키 항목을 반환합니다. | String      |
| - MaxKeys         | 단일 응답에서 반환되는 최대 항목 수                       | String      |
| - Delimiter       | 구분 기호.                                                     | String      |
| - IsTruncated     | 반환된 목록이 잘렸는지 여부 유효한 값: ’true’ 또는 ’false’             | String      |
| - NextMarker      | 목록이 잘린 경우 다음 반환 목록이 시작되는 객체의 키   | String      |
| - CommonPrefixes  | 지정된 Prefix와 delimiter 사이에 경로가 동일한 객체로, 함께 그룹화되고 Common Prefix로 정의됩니다. | ObjectArray |
| - - Prefix        | Common Prefix                                   | String      |
| - EncodingType    | Delimiter, Marker, Prefix, NextMarker, Key에 유효한 반환값의 인코딩 방식을 나타냅니다. | String      |
| - Contents        | 객체 메타데이터 목록                                           | ObjectArray |
| - - Key           | 객체 키. 즉 객체 이름                                         | String      |
| - - ETag          | 객체 콘텐츠에 따라 계산된 MD5 알고리즘 검증값(예: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`). **주의: 앞뒤에 큰따옴표가 사용됩니다.** | String      |
| - - Size          | 객체의 크기. 단위: Byte                                          | String      |
| - - LastModified  | 객체의 마지막 수정 시간 ISO8601 형식, 예: 2019-05-24T10:56:40Z    | String      |
| - - Owner         | 객체 소유자 정보                                               | Object      |
| - - - ID          | 객체 소유자의 전체 ID. 형식은 `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`입니다. 예: `qcs::cam::uin/100000000001:uin/100000000001`, 여기에서 100000000001이 uin입니다. | String      |
| - - - DisplayName | 객체 소유자 이름                                             | String      |
| - - StorageClass  | 객체 스토리지 클래스를 설정합니다. 열거 값은 STANDARD, STANDARD_IA, ARCHIVE 등이 있으며, 자세한 내용은 [스토리지 유형](https://intl.cloud.tencent.com/document/product/436/30925)을 참고하십시오. | String      |

### 객체 간편 업로드

#### 기능 설명

이 API(PUT Object)는 버킷에 객체를 업로드하는 데 사용되며, 이 API를 호출하려면 버킷에 대한 쓰기 권한이 있어야 합니다.

> !
> 1. 키(파일 이름)는 `/`로 끝날 수 없으며, 그렇지 않으면 폴더로 식별됩니다.
> 2. 각 루트 계정(AAPID)은 최대 1,000개의 버킷 ACL과 무제한의 객체 ACL을 가질 수 있습니다. 객체에 대한 ACL이 필요하지 않은 경우 업로드하는 동안 객체에 대한 ACL을 구성하지 않도록 선택할 수 있습니다. 이러한 방식으로, 객체는 기본적으로 버킷의 권한을 상속합니다.
> 3. 객체가 업로드된 후 동일한 키를 사용하여 미리 서명된 URL을 생성할 수 있으며 다운로드를 위해 다른 클라이언트와 공유할 수 있습니다(다운로드하려면 GET method를 사용하십시오. 자세한 API 설명은 아래에 나와 있음). 파일이 private-read로 설정되어 있는 경우 미리 서명된 URL은 특정 기간 동안만 유효합니다.

#### 사용 예시

문자열을 파일 콘텐츠로 업로드합니다.

[//]: # (.cssg-snippet-put-object-string)
```js
cos.putObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Key: 'picture.jpg',              /* 필수 */
    Body: ’hello!’,
}, function(err, data) {
    console.log(err || data);
});
```

디렉터리를 생성합니다.

[//]: # (.cssg-snippet-put-object-folder)
```js
cos.putObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Key: 'a/',              /* 필수 */
    Body: ’’,
}, function(err, data) {
    console.log(err || data);
});
```

객체 업로드(단일 링크 속도 제한):

>?객체 업로드 속도 제한에 대한 설명은 [단일 링크 속도 제한](https://intl.cloud.tencent.com/document/product/436/34072)을 참고하십시오.

[//]: # (.cssg-snippet-put-object-traffic-limit)
```js
cos.putObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: ’COS_REGION’,     /* 버킷이 위치한 리전. 필수 필드 */
    Key: ’exampleobject’,              /* 필수 */
    StorageClass: ’STANDARD’,
    Body: fileObject, // 파일 객체 업로드
    Headers: {
      'x-cos-traffic-limit': 819200, // 속도 제한 설정 범위는 819200 - 838860800, 즉 100KB/s - 100MB/s이며, 이 범위를 초과하면 400 오류가 반환됩니다.
    },
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                 | 매개변수 설명                                                     | 유형     | 필수 입력 여부 |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket                 | BucketName-APPID 형식의 버킷 이름 | String   | Yes   |
| Region                 | 버킷 리전 열거된 값은 리전 및 액세스 엔드포인트를 참고하십시오. | String   | Yes   |
| Key                        | 객체 키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String   | Yes   |
| Body                   | 생성된 파일의 텍스트 내용(문자열일 수 있음)                           | String   | Yes   |
| CacheControl           | RFC 2616에 정의된 캐시 정책입니다. 객체 메타데이터로 저장됩니다.            | String   | No   |
| ContentDisposition     | RFC 2616에 정의된 파일 이름입니다. 객체 메타데이터로 저장됩니다.            | String   | No   |
| ContentEncoding        | RFC 2616에 정의된 인코딩 형식입니다. 객체 메타데이터로 저장됩니다.            | String   | No   |
| ContentLength          | RFC 2616에 정의된 HTTP 요청 길이(바이트)                   | String   | No   |
| ContentType            | RFC 2616에 정의된 콘텐츠 유형(MIME)입니다. 객체 메타데이터로 저장됩니다.    | String   | No   |
| Expires                | RFC 2616에 정의된 만료 시간입니다. 객체 메타데이터로 저장됩니다.            | String   | No   |
| Expect                 | 예상: 100-continue를 사용하는 경우 서버에서 확인을 받은 후에만 요청 내용을 보냅니다. | String   | No   |
| ACL                    | 객체의 ACL(액세스 제어 목록) 속성을 정의합니다. default, private, public-read와 같은 열거 값은 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583)의 Preset ACL 섹션을 참고하십시오. <br>**주의: 객체에 대한 액세스 제어가 필요하지 않은 경우 이 매개변수의 default를 설정하거나 단순히 비워두면 객체가 버킷의 권한을 상속합니다.** | String   | No   |
| GrantRead              | 사용자에게 다음 형식의 읽기 권한을 부여합니다. 형식은 id="[OwnerUin]"이며, 쉼표(,)를 사용하여 여러 사용자를 구분할 수 있습니다. <br><li>서브 계정을 승인하려면 다음을 사용하십시오. `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정을 인증하려면 다음을 사용하십시오. `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String   | No   |
| GrantReadAcp           | 사용자에게 id="[OwnerUin]" 형식의 객체 ACL에 대한 읽기 권한을 부여합니다. 쉼표(,)를 사용하여 여러 사용자를 구분할 수 있습니다. <br/><li>서브 계정을 승인하려면 다음을 사용하십시오. `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정을 인증하려면 다음을 사용하십시오. `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String   | No   |
| GrantWriteAcp          | 사용자에게 id="[OwnerUin]" 형식의 객체 ACL에 대한 쓰기 권한을 부여합니다. 쉼표(,)를 사용하여 여러 사용자를 구분할 수 있습니다. <br><li>서브 계정을 승인하려면 다음을 사용하십시오. `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정을 인증하려면 다음을 사용하십시오. `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String   | No   |
| GrantFullControl       | 사용자에게 id="[OwnerUin]" 형식의 전체 권한을 부여합니다. 쉼표(,)를 사용하여 여러 사용자를 구분할 수 있습니다. <br><li>서브 계정을 승인하려면 다음을 사용하십시오. `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정을 인증하려면 다음을 사용하십시오. `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String   | No   |
| StorageClass           | 객체의 스토리지 클래스입니다. STANDARD(기본값), STANDARD_IA 및 ARCHIVE와 같은 열거된 값은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참고하십시오. | String   | No   |
| x-cos-meta-*           | 객체 메타데이터로 반환될 사용자 정의 헤더 최대 크기는 2KB입니다. | String   | No   |
| onTaskReady            | 업로드 작업이 생성될 때 콜백 함수. 콜백은 작업을 고유하게 식별하고 작업을 취소(cancelTask), 일시 중지(pauseTask) 또는 재개(restartTask)하는 데 사용할 수 있는 taskId를 반환합니다. | Function        | No   |
| - taskId               | 업로드 작업의 ID                                               | String   | No   |
| onProgress             | 진행 상황의 콜백. 응답 객체인 progressData의 속성은 다음과 같습니다.   | Function | No   |
| - progressData.loaded  | 업로드한 파일의 일부 크기. 단위: 바이트(Bytes)                | Number   | No   |
| - progressData.total   | 파일의 전체 크기. 단위: 바이트(Bytes)                        | Number   | No   |
| - progressData.speed   | 파일의 업로드 속도. 단위: 바이트/초(Bytes/s)                   | Number   | No   |
| - progressData.percent | 파일 업로드 진행률(백분율 형식)(예: 0.5는 50% 다운로드를 의미)       | Number   | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 오류(네트워크 오류 또는 서비스 오류)가 발생하면 반환되는 객체입니다. 요청이 성공하면 이 매개변수가 비어 있게 됩니다. 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data         | 요청이 성공하면 반환되는 객체입니다. 요청이 실패하면 이 매개변수는 비어 있습니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| - ETag       | 객체의 MD5 체크섬 이 매개변수의 값은 업로드 중에 객체가 손상되었는지 여부를 확인하는 데 사용할 수 있습니다. <br>예: `"09cba091df696af91549de27b8e7d0f6"`. **주의: ETag값의 시작과 끝에 큰따옴표가 필요합니다.** | String |
| - Location   | 객체의 공용 네트워크 액세스 끝점                                       | String |
| - VersionId  | 버킷에 대해 버전 관리가 활성화된 경우 업로드된 객체의 버전 ID 버전 관리가 활성화되지 않은 경우 이 매개변수가 반환되지 않습니다. | String |

### HTML 양식을 사용한 객체 업로드

이 API(POST Object)는 wx.chooseImage를 통해 사용자가 선택한 객체를 지정된 버킷에 업로드하는 데 사용되며, 이 API를 호출하려면 버킷에 대한 쓰기 권한이 있어야 합니다.

>! onProgress는 미니 프로그램 [UploadTask.onProgressUpdate](https://developers.weixin.qq.com/miniprogram/dev/api/network/upload/UploadTask.onProgressUpdate.html)에 따라 달라지며 일부 Android 모델에서는 진행 상황이 정확하지 않을 수 있습니다.

#### 사용 예시

단순 업로드를 사용하여 파일 업로드:

[//]: # (.cssg-snippet-post-object)
```js
cos.postObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: filename,
    FilePath: tmpFilePath, // wx.chooseImage 파일을 선택해 획득한 tmpFilePath
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function (err, data) {
    console.log(err || data);
});
```

지정 디렉터리에 파일을 업로드합니다.

```js
var folder = ’examplefolder/’;
cos.postObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    Key: folder + filename,              /* 필수 */
    FilePath: tmpFilePath, // wx.chooseImage 파일을 선택해 획득한 tmpFilePath
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                 | 매개변수 설명                                                     | 유형     | 필수 입력 여부 |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket                 | BucketName-APPID 형식의 버킷 이름 | String   | Yes   |
| Region                 | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String   | Yes   |
| Key                        | 객체 키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String   | Yes   |
| ContentLength          | RFC 2616에 정의된 HTTP 요청 길이(바이트)                   | String   | Yes   |
| CacheControl           | RFC 2616에 정의된 캐시 정책입니다. 객체 메타데이터로 저장됩니다.            | String   | No   |
| ContentDisposition     | RFC 2616에 정의된 파일 이름입니다. 객체 메타데이터로 저장됩니다.            | String   | No   |
| ContentEncoding        | RFC 2616에 정의된 인코딩 형식입니다. 객체 메타데이터로 저장됩니다.            | String   | No   |
| ContentType            | RFC 2616에 정의된 콘텐츠 유형(MIME)입니다. 객체 메타데이터로 저장됩니다.    | String   | No   |
| Expires                | RFC 2616에 정의된 만료 시간입니다. 객체 메타데이터로 저장됩니다.            | String   | No   |
| Expect                 | Expect: 100-continue를 사용하는 경우 서버에서 확인을 받은 후에만 요청 내용을 보냅니다. | String   | No   |
| ACL                    | 객체의 ACL 속성을 정의합니다. default, private 및 public-read와 같은 열거된 값에 대해서는 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583)의 사전 설정 ACL 섹션을 참고하십시오. <br>**주의: 객체에 대한 액세스 제어가 필요하지 않은 경우 이 매개변수에 대한 기본값을 설정하거나 비워 두십시오. 이러한 방식으로 객체는 저장된 버킷의 권한을 상속합니다.** | String   | No   |
| StorageClass           | 객체의 스토리지 클래스입니다. STANDARD(기본값), STANDARD_IA 및 ARCHIVE와 같은 열거된 값은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참고하십시오. | String   | No   |
| x-cos-meta-*           | 객체 메타데이터로 저장될 사용자 정의 헤더 최대 크기는 2KB입니다. | String   | No   |
| FilePath               | 업로드할 파일의 임시 파일 경로, wx.chooseImage를 통해 파일을 선택하여 얻을 수 있습니다.   | String   | Yes   |
| onProgress             | 진행 콜백 함수. 콜백의 첫 번째 매개변수는 progressData 객체입니다.         | Function | No   |
| - progressData.loaded  | 다운로드한 파일의 일부 크기. 단위: 바이트(Bytes)                | Number   | No   |
| - progressData.total   | 파일의 전체 크기. 단위: 바이트(Bytes)                        | Number   | No   |
| - progressData.speed   | 파일의 다운로드 속도. 단위: 바이트/초(Bytes/s)                   | Number   | No   |
| - progressData.percent | 파일 다운로드 진행률(백분율 형식)(예: 0.5는 50% 다운로드를 의미함)       | Number   | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 오류(네트워크 오류 또는 서비스 오류)가 발생하면 반환되는 객체입니다. 요청이 성공하면 이 매개변수가 비어 있게 됩니다. 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data         |요청이 성공하면 반환되는 객체입니다. 요청이 실패하면 이 매개변수는 비어 있습니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| - ETag       | 객체의 MD5 checksum을 반환합니다. ETag 값은 업로드 중에 객체가 손상되었는지 여부를 확인하는 데 사용할 수 있습니다. <br>**주의: ETag 값의 시작과 끝에 큰따옴표가 필요합니다. 예: `"09cba091df696af91549de27b8e7d0f6"`** | String |
| - Location   | 외부 네트워크에 대한 객체의 액세스 도메인 이름을 만듭니다.                                       | String |
| - VersionId  | 버전 관리가 활성화된 버킷에서 반환된 객체의 버전 ID                  | String |

### 객체 메타데이터 쿼리

#### 기능 설명

객체의 메타데이터 정보를 쿼리합니다.

#### 사용 예시

[//]: # (.cssg-snippet-head-object)
```js
cos.headObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Key: 'picture.jpg',               /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름          | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket          | BucketName-APPID 형식의 버킷 이름 | String | Yes   |
| Region          | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String | Yes   |
| Key             | 객체 키(Object의 이름). 버킷에서의 객체 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String | Yes   |
| IfModifiedSince | 지정된 시간 이후에 객체가 수정되면 해당 객체 메타데이터가 반환되고, 그렇지 않으면 304가 반환됩니다. | String | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름                | 매개변수 설명                                                     | 유형    |
| --------------------- | ------------------------------------------------------------ | ------- |
| err                   |오류(네트워크 오류 또는 서비스 오류)가 발생할 때 반환되는 객체입니다. 요청이 성공하면 null입니다. 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | Object  |
| - statusCode          | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number  |
| - headers             | 헤더                                           | Object  |
| data                  | 요청이 성공하면 반환되는 객체입니다. 요청이 실패하면 이 매개변수는 비어 있습니다.               | Object  |
| - statusCode          | 200 및 304와 같은 HTTP 상태 코드. 지정된 시간 이후에 수정이 없으면 304가 반환됩니다. | Number  |
| - headers             | 헤더                                           | Object  |
| - x-cos-object-type   | 객체가 추가 가능 여부 열거 값: normal, appendable. 기본 값 normal은 표시되지 않습니다. | String  |
| - x-cos-storage-class | 객체의 스토리지 클래스입니다. STANDARD(기본값), STANDARD_IA 및 ARCHIVE와 같은 열거된 값은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참고하십시오. 반환되는 경우 STANDARD가 표시되지 않습니다. | String  |
| - x-cos-meta-*        | 사용자 정의 meta                                            | String  |
| - NotModified         | 지정된 시간 이후에 객체가 수정되지 않았는지 여부                                 | Boolean |
| - ETag                | 객체의 MD5 체크섬 ETag 값은 업로드 중에 객체가 손상되었는지 여부를 확인하는 데 사용할 수 있습니다. <br>예: `"09cba091df696af91549de27b8e7d0f6"`. **주의: ETag 값 문자열의 시작과 끝에 큰따옴표가 필요합니다.** | String  |
| - VersionId           | 버킷에 대해 버전 관리가 활성화된 경우 업로드된 객체의 버전 ID 버전 관리가 활성화되지 않은 경우 이 매개변수가 반환되지 않습니다. | String  |

### 객체 다운로드

이 API(GET Object)는 버킷에 지정된 파일의 콘텐츠를 문자열 형식으로 가져오는 데 사용됩니다.

#### 사용 예시

[//]: # (.cssg-snippet-get-object)
```js
cos.getObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Key: 'picture.jpg',              /* 필수 */
}, function(err, data) {
    console.log(err || data.Body);
});
```

Range를 지정하여 파일 콘텐츠를 가져옵니다.

[//]: # (.cssg-snippet-get-object-range)
```js
cos.getObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Key: 'picture.jpg',              /* 필수 */
    Range: ’bytes=1-3’,        /* 옵션 */
}, function(err, data) {
    console.log(err || data.Body);
});
```

객체 다운로드(단일 링크 속도 제한)

>?객체 다운로드 속도 제한에 대한 설명은 [단일 링크 속도 제한](https://intl.cloud.tencent.com/document/product/436/34072)을 참고하십시오.

[//]: # (.cssg-snippet-get-object-traffic-limit)
```js
cos.getObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: ’COS_REGION’,     /* 버킷이 위치한 리전. 필수 필드 */
    Key: ’exampleobject’,              /* 필수 */
    Headers: {
      'x-cos-traffic-limit': 819200, // 속도 제한 설정 범위는 819200-838860800, 즉 100KB/s-100MB/s이며, 이 범위를 초과하면 400 오류가 반환됩니다.
    },
}, function(err, data) {
    console.log(err || data.Body);
});
```

#### 매개변수 설명

| 매개변수 이름                     | 매개변수 설명                                                     | 유형     | 필수 입력 여부 |
| -------------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket                     | BucketName-APPID 형식의 버킷 이름 | String   | Yes   |
| Region                     | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String   | Yes   |
| Key                        | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String   | Yes   |
| ResponseContentType        | 응답 헤더의 Content-Type 매개변수                            | String   | No   |
| ResponseContentLanguage    | 응답 헤더의 Content-Language                       | String   | No   |
| ResponseExpires            | 응답 헤더의 Content-Expires                        | String   | No   |
| ResponseCacheControl       | 응답 헤더의 Cache-Control                           | String   | No   |
| ResponseContentDisposition | 응답 헤더의 Content-Disposition                    | String   | No   |
| ResponseContentEncoding    | 응답 헤더의 Content-Encoding                       | String   | No   |
| Range                      | RFC 2616에 정의된 객체의 바이트 범위입니다. 범위 값은 bytes=first-last 형식이어야 합니다. 여기서 first와 last는 모두 0부터 시작하는 오프셋입니다. 예를 들어, bytes=0-9는 객체의 처음 10바이트를 다운로드한다는 의미이며, 이 매개변수를 지정하지 않으면 전체 객체가 다운로드됩니다. | String   | No   |
| IfModifiedSince            | 지정된 시간 이후에 객체가 수정되면 해당 객체 메타데이터가 반환되고, 그렇지 않으면 304(not modified)가 반환됩니다. | String   | No   |
| IfUnmodifiedSince            | 수정되지 않은 필수 시간으로 지정된 시간 이후 수정되지 않은 경우에만 객체가 다운로드되며, 그렇지 않으면 412(precondition failed)가 반환됩니다.. | String   | No   |
| IfMatch                    | ETag가 지정된 콘텐츠와 일치해야 객체를 반환하며, 그렇지 않을 경우 412(precondition failed)를 반환합니다. | String   | No   |
| IfNoneMatch                | ETag가 지정된 콘텐츠와 불일치해야 객체를 반환하며, 그렇지 않을 경우 304(not modified)를 반환합니다. | String   | No   |
| VersionId                  | 다운로드할 객체의 버전 ID                                     | String   | No   |
| onProgress                 | 진행 콜백. 응답 객체(progressData)의 속성은 다음과 같습니다.     | Function | No   |
| - progressData.loaded      | 다운로드한 객체의 일부 크기. 단위: 바이트(Bytes)                | Number   | No   |
| - progressData.total       | 객체의 전체 크기. 단위: 바이트(Bytes)                        | Number   | No   |
| - progressData.speed       | 객체의 다운로드 속도. 단위: 바이트/초(Bytes/s)                   | Number   | No   |
| - progressData.percent     | 파일 다운로드 진행률(예: 0.5는 50% 다운로드됨을 의미)       | Number   | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름                | 매개변수 설명                                                     | 유형    |
| --------------------- | ------------------------------------------------------------ | ------- |
| err                   |오류(네트워크 오류 또는 서비스 오류)가 발생할 때 반환되는 객체입니다. 요청이 성공하면 null입니다. 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | Object  |
| - statusCode          | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number  |
| - headers             | 헤더                                           | Object  |
| data                  | 요청이 성공하면 반환되는 객체입니다. 요청이 실패하면 이 매개변수는 비어 있습니다.               | Object  |
| - statusCode          | 200, 304, 403 및 404와 같은 HTTP 상태 코드를 반환합니다.             | Number  |
| - headers             | 헤더                                           | Object  |
| - CacheControl        | RFC 2616에 정의된 캐시 지시문. 객체 메타데이터에 포함되어 있거나 요청 매개변수를 통해 지정된 경우에만 반환됩니다. | String  |
| - ContentDisposition  | RFC 2616에 정의된 파일 이름. 객체 메타데이터에 포함되어 있거나 요청 매개변수를 통해 지정된 경우에만 반환됩니다. | String  |
| - ContentEncoding     | RFC 2616에 정의된 인코딩 형식입니다. 객체 메타데이터에 포함되어 있거나 요청 매개변수를 통해 지정된 경우에만 반환됩니다. | String  |
| - Expires             | RFC 2616에 정의된 캐시 만료 시간입니다. 객체 메타데이터에 포함되어 있거나 요청 매개변수를 통해 지정된 경우에만 반환됩니다.  | String  |
| - x-cos-storage-class | 객체의 스토리지 클래스입니다. 열거 값은 STANDARD, STANDARD_IA, ARCHIVE가 있습니다. <br>**주의: 해당 헤더가 반환되지 않으면 CFS 유형이 STANDARD(표준 스토리지)라는 의미입니다.** 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참고하십시오. | String  |
| - x-cos-meta-*        | 사용자 정의된 메타데이터                                           | String  |
| - NotModified         | 요청에 IfModifiedSince가 포함된 경우 이 속성이 반환되고 파일이 수정된 경우 false가 반환되고 그렇지 않은 경우 true가 반환됩니다. | Boolean |
| - ETag                | 객체의 MD5 체크섬 ETag 값은 업로드 중에 객체가 손상되었는지 여부를 확인하는 데 사용할 수 있습니다.<br>예: `"09cba091df696af91549de27b8e7d0f6"`. **주의: ETag 값 문자열의 시작과 끝에 큰따옴표가 필요합니다.** | String  |
| - VersionId           |버킷에 대해 버전 관리가 활성화된 경우 업로드된 객체의 버전 ID 버전 관리가 활성화되지 않은 경우 이 매개변수가 반환되지 않습니다. | String  |
| - Body                | 반환된 파일 내용 기본적으로 문자열 형식을 사용합니다.                           | String  |

### CORS 구성 확인

#### 기능 설명

OPTIONS Object 인터페이스는 객체에 대한 크로스 도메인 액세스 설정을 사전 요청합니다. 즉, 크로스 도메인 요청 발송 전 OPTIONS 요청과 특정 출처, HTTP 방법, 헤더 정보 등을 COS에 보내 실제 크로스 도메인 요청 가능 여부를 결정합니다. CORS 설정이 존재하지 않을 경우 요청에 대해 403 Forbidden이 반환됩니다. **사용자는 PUT Bucket cors 인터페이스를 통해 버킷의 CORS 지원을 활성화할 수 있습니다.**

#### 사용 예시

[//]: # (.cssg-snippet-option-object)
```js
cos.optionsObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Key: 'picture.jpg',              /* 필수 */
    Origin: ’https://www.qq.com’,      /* 필수 */
    AccessControlRequestMethod: ’PUT’, /* 필수 */
    AccessControlRequestHeaders: ’origin,accept,content-type’ /* 옵션 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                      | BucketName-APPID 형식의 버킷 이름 | String | Yes   |
| Region                      | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String | Yes   |
| Key                         | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String | Yes   |
| Origin                      | 시뮬레이션된 CORS 요청의 원본 도메인 이름                                   | String | Yes   |
| AccessControlRequestMethod  | 시뮬레이션된 CORS 요청의 HTTP 메서드                                 | String | Yes   |
| AccessControlRequestHeaders | 시뮬레이션된 CORS 요청의 헤더                                       | String | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름                       | 매개변수 설명                                                     | 유형    |
| ---------------------------- | ------------------------------------------------------------ | ------- |
| err                          | 오류(네트워크 오류 또는 서비스 오류)가 발생하면 반환되는 객체입니다. 요청이 성공하면 이 매개변수가 비어 있게 됩니다. 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object  |
| - statusCode                 | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number  |
| - headers                    | 헤더를 반환                                           | Object  |
| data                         | 요청이 성공하면 반환되는 객체입니다. 요청이 실패하면 이 매개변수는 비어 있습니다.               | Object  |
| - headers                    | 헤더를 반환                                           | Object  |
| - statusCode                 | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number  |
| - AccessControlAllowOrigin   | 크로스 도메인 액세스 시뮬레이션을 요청하는 원본 도메인. 중간에 쉼표로 구분하며, 원본에서 허용하지 않는 경우 해당 Header는 반환되지 않습니다. 예: `*` | String  |
| - AccessControlAllowMethods  | 크로스 도메인 액세스 시뮬레이션을 요청하는 HTTP 방법. 중간에 쉼표로 구분하며, 요청 방법을 허용하지 않는 경우 해당 Header는 반환되지 않습니다. 예: PUT, GET, POST, DELETE, HEAD | String  |
| - AccessControlAllowHeaders  | 크로스 도메인 액세스 시뮬레이션을 요청하는 헤더. 중간에 쉼표로 구분하며, 모든 요청 헤더 시뮬레이션을 허용하지 않는 경우 해당 Header는 요청 헤더를 반환하지 않습니다. 예: accept, content-type, origin, authorization | String  |
| - AccessControlExposeHeaders | 크로스 도메인은 헤더 반환을 지원하며, 중간에 쉼표로 구분합니다. 예: ETag                  | String  |
| - AccessControlMaxAge        | OPTIONS 요청이 결과를 얻는 유효기간을 설정합니다. 예: 3600                  | String  |
| - OptionsForbidden           | OPTIONS 요청 거부 여부. 반환된 HTTP 상태 코드가 403이면 true입니다. | Boolean |

### 객체 복사

#### 기능 설명

PUT Object - Copy는 기존에 있는 COS 객체의 사본 생성을 요청합니다. 즉, 객체 하나를 원본 경로(객체 키)에서 타깃 경로(객체 키)로 복사합니다. 복사 과정에서 객체 메타데이터와 액세스 제어 리스트(ACL)는 수정될 수 있습니다.
사용자는 해당 인터페이스를 통해 복제본 생성, 객체 메타데이터 수정(원본 객체와 타깃 파일의 속성은 동일), 객체의 이동과 이름 변경(먼저 객체를 복사한 다음 삭제 API 호출)이 가능합니다.

> !객체의 크기는 1MB - 5GB를 권장합니다. 5GB가 넘는 객체는 고급 인터페이스 객체 복사 [Slice Copy File](#.E5.A4.8D.E5.88.B6.E5.AF.B9.E8.B1.A12)을 사용하시기 바랍니다.



#### 사용 예시

객체 복사:

[//]: # (.cssg-snippet-copy-object)
```js
cos.putObjectCopy({
    Bucket: ’examplebucket-1250000000’,                               /* 필수 */
    Region: ’COS_REGION’,     /* 버킷이 위치한 리전. 필수 필드 */
    Key: ’exampleobject’,                                            /* 필수 */
    CopySource: ’sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject’, /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

객체 스토리지 유형 수정:

[//]: # (.cssg-snippet-copy-object)
```js
cos.putObjectCopy({
    Bucket: ’examplebucket-1250000000’,                               /* 필수 */
    Region: ’COS_REGION’,     /* 버킷이 위치한 리전. 필수 필드 */
    Key: 'sourceObject',                                            /* Key는 CopySource의 Key와 동일, 필수 */
    CopySource: ’sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject’, /* 필수 */
    StorageClass: 'ARCHIVE',  /* 아카이브로 설정 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                      | BucketName-APPID 형식의 버킷 이름 | String | Yes   |
| Region                      | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String | Yes   |
| Key                         | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String | Yes   |
| CopySource                  | 소스 객체의 URL입니다. URL 매개변수 ?versionId=&lt;versionId>를 사용하여 이전 버전을 지정할 수 있습니다. | String | Yes   |
| ACL                         | 객체의 ACL 속성을 정의합니다. default, private 및 public-read와 같은 열거된 값에 대해서는 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583)의 사전 설정 ACL 섹션을 참고하십시오. <br>**주의: 객체에 대한 액세스 제어가 필요하지 않은 경우 이 매개변수에 대한 기본값을 설정하거나 비워 두십시오. 이러한 방식으로 객체는 저장된 버킷의 권한을 상속합니다.** | String | No   |
| GrantRead                   | 사용자에게 id="[OwnerUin]" 형식의 읽기 권한을 부여합니다. 쉼표(,)를 사용하여 여러 사용자를 구분할 수 있습니다. <br><li>서브 계정을 승인하려면 다음을 사용하십시오. `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정을 인증하려면 다음을 사용하십시오. `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No   |
| GrantWrite                  | 사용자에게 id="[OwnerUin]" 형식의 쓰기 권한을 부여합니다.쉼표(,)를 사용하여 여러 사용자를 구분할 수 있습니다. <br><li>서브 계정을 승인하려면 다음을 사용하십시오. `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정을 인증하려면 다음을 사용하십시오. `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No   |
| GrantFullControl            | 사용자에게 id="[OwnerUin]" 형식의 전체 권한을 부여합니다. 쉼표(,)를 사용하여 여러 사용자를 구분할 수 있습니다. <br><li>서브 계정을 승인하려면 다음을 사용하십시오. `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정을 인증하려면 다음을 사용하십시오. `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No   |
| MetadataDirective           | 메타데이터 복사 여부. 열거 값은 Copy, Replaced이며, 기본값은 Copy입니다. Copy로 표기되어 있다면 Header의 사용자 메타데이터 정보를 무시하고 바로 복사합니다. Replaced로 표기되어 있다면 Header 정보에 따라 메타데이터를 수정합니다. **타깃 경로와 원본 경로가 일치할 때, 즉 사용자가 메타데이터를 수정하려고 할 때는 반드시 Replaced로 표기되어 있어야 합니다.** | String | No   |
| CopySourceIfModifiedSince   | 객체가 지정된 시간 이후에 수정될 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. **CopySourceIfNoneMatch와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다.** | String | No   |
| CopySourceIfUnmodifiedSince | 객체가 지정된 시간 이후에 수정되지 않을 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. **CopySourceIfMatch와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다.** | String | No   |
| CopySourceIfMatch           | 객체의 Etag와 일치할 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. **CopySourceIfUnmodifiedSince와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다.** | String | No   |
| CopySourceIfNoneMatch       | 객체의 Etag와 불일치할 경우 작업을 수행하고, 그렇지 않을 경우 412를 반환합니다. **CopySourceIfModifiedSince와 함께 사용할 수 있으며, 다른 조건과 함께 사용할 경우 충돌합니다.** | String | No   |
| StorageClass                | 객체의 스토리지 유형 설정. 열거 값은 STANDARD, STANDARD_IA 등이 있으며, 기본값은 STANDARD입니다. 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참고하십시오. | String | No   |
| x-cos-meta-*                | 기타 사용자 정의된 파일 헤더                                         | String | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름         | 매개변수 설명                                                     | 유형   |
| -------------- | ------------------------------------------------------------ | ------ |
| err            | 오류(네트워크 오류 또는 서비스 오류)가 발생하면 반환되는 객체입니다. 요청이 성공하면 이 매개변수가 비어 있게 됩니다. 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | Object  |
| - statusCode   | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number |
| - headers      | 헤더                                           | Object |
| data           | 요청이 성공하면 반환되는 객체입니다. 요청이 실패하면 이 매개변수는 비어 있습니다.               | Object |
| - statusCode   | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number |
| - headers      | 헤더                                           | Object |
| - ETag         | 파일의 MD5 알고리즘 검증값(예: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`) **주의: 앞뒤에 큰따옴표가 사용됩니다.** | String |
| - LastModified | 객체의 마지막 수정 시간 반환. 예: 2017-06-23T12:33:27.000Z         | String |
| - VersionId    | 버킷에 대해 버전 관리가 활성화된 경우 업로드된 객체의 버전 ID 버전 관리가 활성화되지 않은 경우 이 매개변수가 반환되지 않습니다. | String |

### 단일 객체 삭제

#### 기능 설명

이 API(DELETE Object)는 COS 버킷에서 객체를 삭제하는 데 사용되며, 이 API를 호출하려면 버킷에 대한 WRITE 권한이 있어야 합니다.

#### 사용 예시

[//]: # (.cssg-snippet-delete-object)
```js
cos.deleteObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Key: 'picture.jpg',                                            /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름    | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| --------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                     | BucketName-APPID 형식의 버킷 이름 | String   | Yes   |
| Region    | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String | Yes   |
| Key       | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String | Yes   |
| VersionId | 삭제할 객체 버전 ID 또는 DeleteMarker 버전 ID                  | String | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 오류(네트워크 오류 또는 서비스 오류)가 발생하면 반환되는 객체입니다. 요청이 성공하면 이 매개변수가 비어 있게 됩니다. 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data         | 요청이 성공하면 반환되는 객체입니다. 요청이 실패하면 이 매개변수는 비어 있습니다.               | Object      |
| - statusCode | HTTP 상태 코드(예: 200, 204, 403, 404 등). **삭제에 성공하거나 파일이 존재하지 않을 경우 204 또는 200을 반환하고, 지정된 Bucket을 찾지 못할 경우 404를 반환합니다.** | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |

### 다수의 객체 삭제

#### 기능 설명

이 API(DELETE Multiple Objects)는 단일 요청의 버킷에서 여러 객체를 삭제하는 데 사용됩니다. 단일 요청으로 최대 1,000개의 객체를 삭제할 수 있습니다. 선택할 수 있는 응답 모드는 Verbose와 Quiet의 두 가지입니다. Verbose 모드는 각 객체의 삭제에 대한 정보를 반환하는 반면 Quiet 모드는 오류 객체에 대한 정보만 반환합니다.

#### 사용 예시

다수의 파일을 삭제합니다.

[//]: # (.cssg-snippet-delete-multi-object)
```js
cos.deleteMultipleObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Objects: [
        key = "picture.jpg";
        {Key: '2.zip'},
    ]
}, function(err, data) {
    console.log(err || data);
});
```

접두사에 따라 여러 객체를 삭제합니다(지정 디렉터리의 파일 삭제).

```js
var bucket: ’examplebucket-1250000000’; /* 필수 */
var region: ’ap-beijing’;     /* 버킷이 위치한 리전. 필수 필드 */
var prefix = ’examplefolder/’;  /* 삭제할 디렉터리 또는 접두사 */
var deleteFolder = function (marker) {
    cos.getBucket({
        Bucket: bucket,
        Region: region,
        Prefix: prefix,
        Marker: marker,
        MaxKeys: 1000,
    }, function (listError, listResult) {
        if (listError) return console.log(’list error:’, listError);
        var nextMarker = listResult.NextMarker;
        var objects = listResult.Contents.map(function (item) {
            return {Key: item.Key}
        });
        cos.deleteMultipleObject({
            Bucket: bucket,
            Region: region,
            Objects: objects,
        }, function (delError, deleteResult) {
            if (delError) {
                console.log(’delete error’, delError);
                console.log(’delete stop’);
            } else {
                console.log(’delete result’, deleteResult);
                if (listResult.IsTruncated === 'true') deleteFolder(nextMarker);
                else console.log(’delete complete’);
            }
        });
    });
}
deleteFolder();
```

#### 매개변수 설명

| 매개변수 이름      | 매개변수 설명                                                     | 유형        | 필수 입력 여부 |
| ----------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket      | BucketName-APPID 형식의 버킷 이름 | String      | Yes   |
| Region      | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String      | Yes   |
| Quiet       | Boolean 값. 이 값은 Quiet 모드의 실행 여부를 결정합니다. true 값이면 Quiet 모드를 실행하고, false 값이면 Verbose 모드를 실행합니다. 기본값: false | Boolean     | No   |
| Objects     | 삭제할 객체 리스트                                             | ObjectArray | Yes   |
| - Key       | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String      | Yes   |
| - VersionId | 삭제할 객체 버전 ID 또는 DeleteMarker 버전 ID                  | String      | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름                    | 매개변수 설명                                                     | 유형        |
| ------------------------- | ------------------------------------------------------------ | ----------- |
| err                       | 오류(네트워크 오류 또는 서비스 오류)가 발생하면 반환되는 객체입니다. 요청이 성공하면 이 매개변수가 비어 있게 됩니다. 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | Object      |
| - statusCode              | 200, 204, 403 및 404와 같은 HTTP 상태 코드를 반환합니다.             | Number      |
| - headers                 | 헤더                                           | Object      |
| data                      | 요청이 성공하면 반환되는 객체입니다. 요청이 실패하면 이 매개변수는 비어 있습니다.               | Object      |
| - statusCode              | 200, 204, 403 및 404와 같은 HTTP 상태 코드를 반환합니다.             | Number      |
| - headers                 | 헤더                                           | Object      |
| - Deleted                 | 성공적으로 삭제된 객체 목록                               | ObjectArray |
| - - Key                   | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String      |
| - - VersionId             | VersionId 매개변수가 전달되면 응답에도 포함되어 객체 또는 DeleteMarker 버전을 나타냅니다. | String      |
| - - DeleteMarker          |버전 관리가 활성화되어 있고 VersionId 매개변수가 지정되지 않은 경우 삭제 작업은 실제로 객체를 삭제하지 않고 대신에 보이는 객체가 삭제되었음을 의미하는 DeleteMarker만 추가합니다. 이는 볼 수 있던 파일이 삭제되었다는 의미이며, 열거 값은 true와 false입니다. | String      |
| - - DeleteMarkerVersionId | 반환의 DeleteMarker가 true인 경우, 새로 추가된 DeleteMarker의 VersionId를 반환합니다. | String      |
| - Error                   | 이번에 삭제하지 못한 객체 정보 리스트 설명                               | ObjectArray |
| - - Key                   | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String      |
| - - Code                  | 삭제 실패 오류 코드                                             | String      |
| - - Message               | 삭제 오류 정보                                                 | String      |



## 멀티파트 작업

### 멀티파트 업로드 조회

#### 기능 설명

List Multiparts Uploads는 현재 진행 중인 멀티파트 업로드 정보를 쿼리하는 데 사용됩니다. 한 번에 최대 1000개의 현재 진행 중인 멀티파트 업로드를 나열합니다.

#### 사용 예시

객체 키 접두사 exampleobject를 사용하여 업로드의 UploadId 목록 가져오기

[//]: # (.cssg-snippet-list-multi-upload)
```js
cos.multipartList({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Prefix: ’exampleobject’,                        /* 옵션 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름         | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket         | BucketName-APPID 형식의 버킷 이름 | String | Yes   |
| Region         | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String | Yes   |
| Prefix         | 객체 키의 접두사 매칭. 지정된 접두사를 포함한 객체 키만 한정하여 반환합니다. prefix를 사용하여 조회할 경우 반환되는 객체 키에 Prefix가 포함되므로 주의해야 합니다. | String | No   |
| Delimiter      | 객체 키를 그룹화하는 데 사용되는 구분 기호입니다. 일반적으로 `/`입니다. Prefix 사이의 동일한 경로 또는 Prefix가 지정되지 않은 경우 시작과 첫 번째 delimiter를 그룹화하여 Common Prefix로 정의합니다. 모든 Common Prefix가 나열됩니다. | String | No   |
| EncodingType   | 규정된 반환 값의 인코딩 형식입니다. 합법적 값은 url입니다.                            | String | No   |
| MaxUploads     | 반환하는 최대 항목 수 설정. 유효한 값 범위: 1 - 1000, 기본값: 1000         | String | No   |
| KeyMarker      | upload-id-marker와 함께 사용합니다.<br> <li> upload-id-marker 미지정 시 <br>&emsp;- ObjectName 알파벳 순서가 key-marker보다 큰 항목 열거됩니다.<br><li>upload-id-marker 지정 시 <br>&emsp;- ObjectName 알파벳 순서가 key-marker보다 큰 항목이 열거되고,<br>&emsp;- ObjectName 알파벳 순서가 key-marker와 동일하고 UploadID가 upload-id-marker보다 큰 항목이 열거됩니다. | String | No   |
| UploadIdMarker | key-marker와 함께 사용합니다.<br><li>key-marker 미지정 시 <br>&emsp;- upload-id-marker는 무시됩니다.<br><li>key-marker 지정 시 <br>&emsp;- ObjectName 알파벳 순서가 key-marker보다 큰 항목이 열거되고, <br>&emsp;- ObjectName 알파벳 순서가 key-marker와 같고 UploadID가 upload-id-marker보다 큰 항목이 열거됩니다. | String | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름               | 매개변수 설명                                                     | 유형        |
| -------------------- | ------------------------------------------------------------ | ----------- |
| err                  | 오류(네트워크 오류 또는 서비스 오류)가 발생하면 반환되는 객체입니다. 요청이 성공하면 이 매개변수가 비어 있게 됩니다. 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | Object      |
| - statusCode         | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers            | 헤더                                           | Object      |
| data                 | 요청이 성공하면 반환되는 객체입니다. 요청이 실패하면 이 매개변수는 비어 있습니다.               | Object      |
| - statusCode         | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers            | 헤더                                           | Object      |
| - Bucket             | 멀티파트 업로드를 위한 타깃 버킷                                         | String      |
| - Encoding-Type      | 반환된 값의 인코딩 유형입니다. 유효한 값: url                            | String      |
| - KeyMarker          | 목록이 시작되는 key를 지정합니다.                                      | String      |
| - UploadIdMarker     | 목록이 시작되는 UploadId를 지정합니다.                                 | String      |
| - NextKeyMarker      | 반환된 목록이 잘리면 반환된 NextKeyMarker가 후속 목록의 시작점이 됩니다. | String      |
| - NextUploadIdMarker | 반환된 목록이 잘리면 반환된 UploadId가 후속 목록의 시작점이 됩니다.     | String      |
| - MaxUploads         | 반환되는 최대 항목 수를 설정합니다. 유효한 값 범위: 1 - 1000               | String      |
| - IsTruncated        | 반환된 객체가 잘리는지 여부를 나타냅니다. 'true' 또는 'false'                      | String      |
| - Prefix             | 객체 키의 접두사 매칭. 지정된 접두사를 포함한 객체 키만 한정하여 반환합니다.           | String      |
| - Delimiter      | 객체 키를 그룹화하는 데 사용되는 구분 기호입니다. 일반적으로 `/`입니다. Prefix 사이의 동일한 경로 또는 Prefix가 지정되지 않은 경우 시작과 첫 번째 delimiter를 그룹화하여 Common Prefix로 정의합니다. 모든 Common Prefix가 나열됩니다. | String      |
| - CommonPrefixs      | prefix부터 delimiter 사이의 동일한 경로를 하나로 분류하고 Common Prefix로 정의합니다. | ObjectArray |
| - - Prefix           | 구체적인 Common Prefixs 표시                                    | String      |
| - Upload             | 멀티파트 업로드의 정보 집합                                           | ObjectArray |
| - - Key              | 객체의 이름, 즉 객체 키                                         | String      |
| - - UploadId         | 이번 멀티파트 업로드의 ID 표시                                        | String      |
| - - StorageClass     | 멀티파트의 스토리지 유형을 표시하는 데 사용. 열거 값은 STANDARD, STANDARD_IA, ARCHIVE 등이 있으며, 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참고하십시오. | String      |
| - - Initiator        | 이번에 업로드한 담당자 정보 표시                                 | Object      |
| - - - DisplayName    | 업로드 담당자 이름                                             | String      |
| - - - ID             | 업로드 담당자 ID. 형식: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>루트 계정인 경우, &lt;OwnerUin>과 &lt;SubUin>의 값이 동일합니다. | String      |
| - - Owner            | 멀티파트 소유자의 정보 표시                                     | Object      |
| - - - DisplayName    | 멀티파트 소유자의 이름                                             | String      |
| - - - ID             | 멀티파트 소유자 ID. 형식: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>루트 계정인 경우, &lt;OwnerUin>과 &lt;SubUin>의 값이 동일합니다. | String      |
| - - Initiated        | 멀티파트 업로드의 시작 시간                                           | String      |

### 멀티파트 업로드 초기화

#### 기능 설명

Initiate Multipart Uploads는 멀티파트 업로드 초기화를 요청합니다. 요청을 성공적으로 처리하면 Upload ID를 반환하고, 이는 다음 Upload Part 요청에 사용됩니다.

#### 사용 예시

[//]: # (.cssg-snippet-init-multi-upload)
```js
cos.multipartInit({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: ’exampleobject’,              /* 필수 */
}, function(err, data) {
    console.log(err || data);
    if (data) {
      uploadId = data.UploadId;
    }
});
```

#### 매개변수 설명

| 매개변수 이름             | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket             | BucketName-APPID 형식의 버킷 이름 | String | Yes   |
| Region             | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String | Yes   |
| Key                | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String | Yes   |
| CacheControl       | RFC 2616에 정의된 캐시 정책. 객체의 메타데이터로 저장됩니다.            | String | No   |
| ContentDisposition | RFC 2616에 정의된 파일 이름. 객체의 메타데이터로 저장됩니다.            | String | No   |
| ContentEncoding    | RFC 2616에 정의된 인코딩 형식. 객체의 메타데이터로 저장됩니다.            | String | No   |
| ContentType        | RFC 2616에 정의된 콘텐츠 유형(MIME). 객체의 메타데이터로 저장됩니다.    | String | No   |
| Expires            | RFC 2616에 정의된 만료 시간. 객체의 메타데이터로 저장됩니다.            | String | No   |
| ACL                | 객체의 ACL 속성을 정의합니다. default, private 및 public-read와 같은 열거된 값에 대해서는 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583)의 사전 설정 ACL 섹션을 참고하십시오. <br>**주의: 객체에 대한 액세스 제어가 필요하지 않은 경우 이 매개변수에 대한 기본값을 설정하거나 비워 두십시오. 이러한 방식으로 객체는 저장된 버킷의 권한을 상속합니다.** | String  | No   |
| GrantRead          | id="[OwnerUin]" 형식으로 사용자에게 읽기 권한을 부여합니다. 쉼표(,)를 사용하여 여러 사용자를 구분할 수 있습니다. <br><li>서브 계정을 승인하려면 다음을 사용하십시오. `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정을 인증하려면 다음을 사용하십시오. `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No   |
| GrantFullControl   | 권한을 부여받은 대상에게 모든 객체 작업 권한을 부여합니다. 형식은 id="[OwnerUin]"이며, 쉼표(,)를 사용하여 여러 사용자를 구분할 수 있습니다. <br><li>서브 계정을 승인하려면 다음을 사용하십시오. `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정을 인증하려면 다음을 사용하십시오. `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No   |
| StorageClass       | 객체의 스토리지 유형 설정. 열거 값은 STANDARD, STANDARD_IA, ARCHIVE 등이 있으며, 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참고하십시오. 기본값은 STANDARD입니다. | String | No   |
| x-cos-meta-*       | 객체 메타데이터로 반환될 사용자 정의 헤더 최대 크기는 2KB입니다. | String | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름   | 매개변수 설명                                                     | 유형   |
| -------- | ------------------------------------------------------------ | ------ |
| err      |오류(네트워크 오류 또는 서비스 오류)가 발생하면 반환되는 객체입니다. 요청이 성공하면 이 매개변수가 비어 있게 됩니다. 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | Object |
| data     | 요청이 성공하면 반환되는 내용입니다. 요청이 실패하면 이 매개변수는 비어 있습니다.               | Object |
| Bucket   | 멀티파트 업로드의 타깃 버킷. 형식은 BucketName-APPID입니다. 예: examplebucket-1250000000 | String |
| Key      | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |
| UploadId | 후속 업로드에 사용되는 ID                                        | String |

### 멀티파트 업로드

#### 기능 설명

이 API(업로드 파트)는 멀티파트 업로드가 초기화된 후 파트를 업로드하는 데 사용되며 한 번에 1MB에서 5GB까지 1-10,000개의 파트를 업로드할 수 있습니다.
<li>멀티파트 업로드 시작 API를 사용하여 Initiate Multipart Upload하면 uploadId를 얻을 수 있습니다. 이 ID는 전체 객체에서 해당 부분과 해당 위치를 고유하게 식별합니다.</li>
<li>Upload Part를 호출할 때마다 partNumber와 uploadId를 전달해야 합니다. partNumber를 순서 없이 업로드할 수 있습니다.</li>
<li>새 부분의 'uploadId'와 partNumber가 이전에 업로드한 부분과 동일한 경우 이전 부분을 덮어씁니다. uploadId가 존재하지 않으면 404 오류 NoSuchUpload가 반환됩니다.</li>

#### 사용 예시

[//]: # (.cssg-snippet-upload-part)
```js
cos.multipartUpload({
   Bucket: ’examplebucket-1250000000’, /* 필수 */
   Region: ’COS_REGION’,     /* 버킷이 위치한 리전. 필수 필드 */
   Key: ’exampleobject’,       /* 필수 */
   UploadId: ’exampleUploadId’,
   PartNumber: ’1’,
   Body: fileObject
}, function(err, data) {
   console.log(err || data);
   if (data) {
     eTag = data.ETag;
   }
});
```

#### 매개변수 설명

| 매개변수 이름        | 매개변수 설명                                                     | 유형             | 필수 입력 여부 |
| ------------- | ------------------------------------------------------------ | ---------------- | ---- |
| Bucket        | BucketName-APPID 형식의 버킷 이름 | String           | Yes   |
| Region        | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String           | Yes   |
| Key           | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String           | Yes   |
| ContentLength | RFC 2616에 정의된 HTTP 요청 콘텐츠 길이(바이트)                   | String           | Yes   |
| PartNumber    | 파트의 번호                                                   | String           | Yes   |
| UploadId      | 이번 멀티파트 업로드 작업의 번호                                       | String           | Yes   |
| Body          | 파일 멀티파트의 콘텐츠를 업로드합니다.  문자열, ArrayBuffer 객체가 될 수 있습니다.    | String/ArrayBuffer | Yes   |
| Expect        | RFC 2616에 정의된 HTTP 요청 콘텐츠의 길이(바이트). `Expect: 100-continue`를 사용할 경우, 서버의 확인을 받아야 요청 콘텐츠를 발송할 수 있습니다. | String           | No   |
| ContentMD5    | RFC 1864에 정의된 Base64로 인코딩한 128-bit 콘텐츠 MD5 검증값. 이 헤더는 파일 콘텐츠의 변경 여부를 검증하는 데 사용됩니다. | String           | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 오류(네트워크 오류 또는 서비스 오류)가 발생할 때 반환되는 오류 코드입니다. 요청이 성공하면 이 매개변수는 비어 있습니다. 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data         | 요청이 성공하면 반환되는 객체입니다. 요청이 실패하면 이 매개변수는 비어 있습니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |

### 멀티파트 복사

#### 기능 설명

Upload Part - Copy는 원본 경로에서 대상 경로로 객체의 일부를 복사하는 데 사용됩니다.

> !객체 부분을 복사하려면 먼저 멀티파트 업로드를 초기화해야 합니다. 그런 다음 고유한 upload ID가 반환됩니다. 이 ID는 복사 요청에 필요합니다.

#### 사용 예시

[//]: # (.cssg-snippet-upload-part-copy)
```js
cos.uploadPartCopy({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: ’exampleobject’,       /* 필수 */
    CopySource: ’sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject’, /* 필수 */
    UploadId: ’exampleUploadId’,    /* 필수 */
    PartNumber: ’1’, /* 필수 */
}, function(err, data) {
    console.log(err || data);
    if (data) {
      eTag = data.ETag;
    }
});
```

#### 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| --------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                      | BucketName-APPID 형식의 버킷 이름 | String | Yes   |
| Region                      | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String | Yes   |
| Key                         | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String | Yes   |
| CopySource                  | 소스 객체의 URL입니다. URL 매개변수 ?versionId=&lt;versionId>를 사용하여 이전 버전을 지정할 수 있습니다. | String | Yes   |
| PartNumber                  | 멀티파트 복사한 파트 번호                                               | String | Yes   |
| UploadId                    | 객체를 부분적으로 업로드하려면 먼저 멀티파트 업로드를 초기화해야 합니다. 멀티파트 업로드 초기화 응답은 멀티파트 업로드 요청에 포함되어야 하는 고유한 설명자(upload ID)를 전달합니다. | String | Yes   |
| CopySourceRange             | 소스 객체의 바이트 범위입니다. 범위 값은 bytes=first-last 형식이어야 합니다. 여기서 first와 last는 모두 0부터 시작하는 오프셋입니다. 예를 들어, bytes=0-9는 원본 객체의 처음 10바이트를 복사한다는 의미입니다. 이 매개변수를 지정하지 않으면 전체 객체가 복사됩니다. | String | No   |
| CopySourceIfMatch           | 일치해야 하는 Etag입니다. 부품은 해당 ETag가 지정된 값과 일치하는 경우에만 복사됩니다. 그렇지 않으면 412가 반환됩니다. 이 매개변수는 x-cos-copy-source-If-Unmodified-Since와 함께 사용할 수 있습니다. 다른 조건과 함께 사용하면 충돌이 발생할 수 있습니다. | String | No   |
| CopySourceIfNoneMatch       | 일치할 수 없는 ETag입니다. 부품은 해당 ETag가 지정된 값과 일치하지 않는 경우에만 복사됩니다. 그렇지 않으면 412가 반환됩니다. 이 매개변수는 x-cos-copy-source-If-Modified-Since와 함께 사용할 수 있습니다. 다른 조건과 함께 사용하면 충돌이 발생할 수 있습니다. | String | No   |
| CopySourceIfUnmodifiedSince | 수정되지 않은 필수 시간. 객체는 지정된 시간 이후 수정되지 않은 경우에만 복사됩니다. 그렇지 않으면 412가 반환됩니다. 이 매개변수는 x-cos-copy-source-If-Match와 함께 사용할 수 있습니다. 다른 조건과 함께 사용하면 충돌이 발생할 수 있습니다. | String | No   |
| CopySourceIfModifiedSince   | 필요한 수정 시간. 지정된 시간 이후에 수정된 경우에만 객체가 복사됩니다. 그렇지 않으면 412가 반환됩니다. 이 매개변수는 x-cos-copy-source-If-None-Match와 함께 사용할 수 있습니다. 다른 조건과 함께 사용하면 충돌이 발생할 수 있습니다. | String | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름         | 매개변수 설명                                                     | 유형   |
| -------------- | ------------------------------------------------------------ | ------ |
| err            | 오류(네트워크 오류 또는 서비스 오류)가 발생하면 반환되는 객체입니다. 요청이 성공하면 이 매개변수는 비어 있습니다. 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | Object |
| - statusCode   | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number |
| - headers      | 헤더                                           | Object |
| data           | 요청이 성공하면 반환되는 객체입니다. 요청이 실패하면 이 매개변수는 비어 있습니다.               | Object |
| - statusCode   | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number |
| - headers      | 헤더                                           | Object |
| - ETag         | 파일의 MD5 알고리즘 검증값(예: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`) **주의: 앞뒤에 큰따옴표가 사용됩니다.** | String |
| - LastModified | 객체의 마지막 수정 시간(GMT 형식)                               | String |

### 업로드된 파트 조회

#### 기능 설명

이 API(List Parts)는 지정된 멀티파트 업로드의 업로드된 부분을 쿼리하는 데 사용됩니다.

#### 사용 예시

[//]: # (.cssg-snippet-list-parts)
```js
cos.multipartListPart({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: ’exampleobject’,              /* 필수 */
    UploadId: 'exampleUploadId', /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름           | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket           | BucketName-APPID 형식의 버킷 이름 | String | Yes   |
| Region           | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String | Yes   |
| Key              | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String | Yes   |
| UploadId         | 멀티파트 업로드 시작 API의 응답에서 얻은 멀티파트 UploadId입니다. | String | Yes   |
| EncodingType     | 반환된 값의 인코딩 유형                                         | String | No   |
| MaxParts         | 한 번에 반환할 최대 부품 수입니다. 기본값은 1000입니다.                           | String | No   |
| PartNumberMarker | 반환된 목록이 시작되는 marker입니다. 기본적으로 항목은 UTF-8 이진 순서로 나열됩니다.  | String | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름                 | 매개변수 설명                                                     | 유형        |
| ---------------------- | ------------------------------------------------------------ | ----------- |
| err                    |오류(네트워크 오류 또는 서비스 오류)가 발생하면 반환되는 객체입니다. 요청이 성공하면 이 매개변수는 비어 있습니다. 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | Object      |
| - statusCode           | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers              | 헤더를 반환                                           | Object      |
| data                   | 요청이 성공하면 반환되는 객체입니다. 요청이 실패하면 이 매개변수는 비어 있습니다.               | Object      |
| - statusCode           | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers              | 헤더를 반환                                           | Object      |
| - Bucket               | 멀티파트 업로드를 위한 대상 버킷                                         | String      |
| - Encoding-type        | 반환값의 인코딩 유형                                         | String      |
| - Key                  | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String      |
| - UploadId             | Initiate Multipart Upload API에서 얻은 멀티파트 UploadId입니다.                                       | String      |
| - Initiator            | 업로드 개시자                                 | Object      |
| - - DisplayName        | 업로드 개시자의 이름                                             | String      |
| - - ID                 | 업로드 개시자 ID. 형식: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>루트 계정의 경우, &lt;OwnerUin>과 &lt;SubUin>은 동일한 값을 갖습니다. | String      |
| - Owner                | 파트 소유자에 대한 정보                                 | Object      |
| - - DisplayName        | 버킷 소유자의 이름                                           | String      |
| - - ID                 | 버킷 소유자의 ID. 일반적으로 사용자의 UIN입니다.                            | String      |
| - StorageClass         | 부품의 스토리지 클래스입니다. STANDARD, STANDARD_IA 및 ARCHIVE와 같은 열거 값은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참고하십시오. | String      |
| - PartNumberMarker     | 기본적으로 UTF-8 이진법 순서로 열거되며, 모든 열거 값은 Marker부터 시작합니다.  | String      |
| - NextPartNumberMarker | 목록이 잘린 경우 반환된 NextMarker가 다음 반환 목록이 시작되는 부분이 됩니다.   | String      |
| - MaxParts             | 한 번에 반환하는 최대 항목 수                                       | String      |
| - IsTruncated          |반환 항목의 잘림 여부. 'true' 또는 'false'                      | String      |
| - Part                 | 멀티파트 정보 리스트                                                 | ObjectArray |
| - - PartNumber         | 파트의 번호                                                     | String      |
| - - LastModified       | 파트의 최종 수정 시간                                               | String      |
| - - ETag               | 파트의 MD5 알고리즘 검증값                                          | String      |
| - - Size               | 파트의 크기. 단위: Byte                                          | String      |

### 멀티파트 업로드 완료

#### 기능 설명

Complete Multipart Upload 인터페이스는 전체 멀티파트 업로드 완료를 요청합니다. Upload Parts를 사용해 모든 파트를 업로드한 후에는 반드시 해당 API를 호출하여 전체 파일의 멀티파트 업로드를 완료해야 합니다. 해당 API를 사용할 때에는 반드시 Body에서 모든 파트의 PartNumber와 ETag를 요청해 파트의 정확성을 검증해야 합니다.
멀티파트 업로드가 완료된 후에는 병합이 필요하며, 병합에는 몇 분 정도의 시간이 소요됩니다. 따라서 멀티파트 병합이 시작되면 COS에서 즉시 상태 코드 200을 반환하고, 병합 과정에서 주기적으로 빈 정보를 반환해 연결을 유지합니다. 병합이 완료될 때까지 COS는 Body에 병합된 파트의 콘텐츠를 반환합니다.

- 업로드된 파트가 1MB 미만인 경우 해당 API 호출 시 400 EntityTooSmall이 반환됩니다.
- 업로드된 파트의 번호가 불연속적인 경우 해당 API 호출 시 400 InvalidPart가 반환됩니다.
- 요청 Body에 있는 파트 정보를 오름차순으로 정렬하지 않은 경우 해당 API 호출 시 400 InvalidPartOrder가 반환됩니다.
- UploadId가 존재하지 않은 경우 해당 API 호출 시 404 NoSuchUpload가 반환됩니다.

> !업로드가 완료되었으나 중단되지 않은 멀티파트는 스토리지 용량을 차지하여 비용이 발생하므로, 즉시 멀티파트 업로드를 완료하거나 취소하는 것을 권장합니다.

#### 사용 예시

[//]: # (.cssg-snippet-complete-multi-upload)
```js
cos.multipartComplete({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: ’exampleobject’,              /* 필수 */
    UploadId: ’exampleUploadId’,    /* 필수 */
    Parts: [
        {PartNumber: ’1’, ETag: ’exampleETag’},
    ]
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름       | 매개변수 설명                                                     | 유형        | 필수 입력 여부 |
| ------------ | ------------------------------------------------------------ | ----------- | ---- |
| Bucket       | BucketName-APPID 형식의 버킷 이름 | String      | Yes   |
| Region       | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String      | Yes   |
| Key          | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String      | Yes   |
| UploadId     | 업로드 작업 번호                                                 | String      | Yes   |
| Parts        | 이번 멀티파트 업로드의 파트 정보 리스트 설명                           | ObjectArray | Yes   |
| - PartNumber | 멀티파트의 번호                                                   | String      | Yes   |
| - ETag       | 모든 파트 파일의 MD5 알고리즘 검증값<br>(예: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`) **주의: 앞뒤에 큰따옴표가 사용됩니다.** | String      | Yes   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 오류(네트워크 오류 또는 서비스 오류)가 발생하면 반환되는 객체입니다. 요청이 성공하면 이 매개변수는 비어 있습니다. 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data         | 요청이 성공하면 반환되는 객체입니다. 요청이 실패하면 이 매개변수는 비어 있습니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| - Location   | 객체의 외부 네트워크 액세스 도메인 생성                                       | String |
| - Bucket     | 멀티파트 업로드의 타깃 버킷                                         | String |
| - Key                  | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |
| - ETag       | 병합 후 파일의 고유 ID. 형식: "uuid-<파트 수>"<br>예: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`, **주의: 시작과 끝에 큰따옴표가 필요합니다.** | String |

### 멀티파트 업로드 중지

#### 기능 설명

Abort Multipart Upload는 멀티파트 업로드 작업 중지 및 이미 업로드된 파트 삭제에 사용됩니다. Abort Multipart Upload 호출 시, 해당 UploadId를 사용해 파트 업로드를 요청한 경우 Upload Parts에서 실패를 반환합니다. 해당 UploadId가 존재하지 않을 경우 404 NoSuchUpload를 반환합니다.

> !업로드가 완료되었으나 중단되지 않은 멀티파트는 스토리지 용량을 차지하여 비용이 발생하므로, 즉시 멀티파트 업로드를 완료하거나 취소하는 것을 권장합니다.

#### 사용 예시

[//]: # (.cssg-snippet-abort-multi-upload)
```js
cos.multipartAbort({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: ’exampleobject’,                           /* 필수 */
    UploadId: 'exampleUploadId'                       /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket   | BucketName-APPID 형식의 버킷 이름 | String | Yes   |
| Region   | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String | Yes   |
| Key      | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String | Yes   |
| UploadId         | 이번 멀티파트 업로드 ID 표시. Initiate Multipart Upload 인터페이스를 사용해 멀티파트 업로드를 초기화했을 때 획득한 UploadId입니다. | String | Yes   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 오류(네트워크 오류 또는 서비스 오류)가 발생하면 반환되는 객체입니다. 요청이 성공하면 이 매개변수는 비어 있습니다. 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data         | 요청이 성공하면 반환되는 객체입니다. 요청이 실패하면 이 매개변수는 비어 있습니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 헤더를 반환  

## 기타 작업

### 보관된 객체 복구

#### 기능 설명

이 API는 COS에 보관된 객체를 복원하는 데 사용되며 복원된 가독성 객체는 임시로 객체를 읽을 수 있도록 구성하고 삭제할 시간을 설정할 수 있습니다. Days 매개변수를 사용하여 임시 객체의 만료 시간을 지정할 수 있습니다. 객체가 만료되고 만료되기 전에 객체를 복사하거나 유효 기간을 연장하는 작업을 시작하지 않은 경우 임시 객체는 자동으로 삭제됩니다. 임시 객체는 원본 아카이브 객체의 복사본일 뿐이며 원본 객체는 이 기간 동안 존재합니다.

#### 사용 예시

[//]: # (.cssg-snippet-restore-object)
```js
cos.restoreObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Key: 'picture.jpg',
    RestoreRequest: {
        Days: 1,
        CASJobParameters: {
            Tier: ’Expedited’
        }
    },
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름           | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket             | BucketName-APPID 형식의 버킷 이름 | String | Yes   |
| Region             | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String | Yes   |
| Key                | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String | Yes   |
| RestoreRequest     | 복구 데이터의 컨테이너에 사용                                           | Object | Yes   |
| - Days             | 임시 사본의 만료 시간 설정                                       | Number | Yes   |
| - CASJobParameters | 아카이브 작업 매개변수의 컨테이너                                       | Object | Yes   |
| - - Tier           | 복원 모드. ARCHIVE의 경우 Tier는 Standard(3 - 5시간 이내에 객체 복원), Expedited(15분 이내에 객체 복원) 및 Bulk(5 - 12시간 이내에 객체 복원)로 설정할 수 있습니다. DEEP ARCHIVE의 경우 Tier를 Standard(12 - 24시간 이내에 객체 복원) 및 Bulk(24 - 48시간 내에 객체 복원)로 설정할 수 있습니다. | String | Yes   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 오류(네트워크 오류 또는 서비스 오류)가 발생하면 반환되는 객체입니다. 요청이 성공하면 이 매개변수는 비어 있습니다. 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data         | 요청이 성공하면 반환되는 객체입니다. 요청이 실패하면 이 매개변수는 비어 있습니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |

### 객체 ACL 설정

#### 기능 설명

PUT Object acl 인터페이스는 특정 버킷에서 한 객체의 액세스 제어 리스트(ACL)를 설정할 때 사용합니다.

> !루트 계정(동일한 APPID)당 버킷의 ACL, Policy 및 CAM 관련 정책은 최대 1000개까지 설정할 수 있으며, 객체 액세스 제어 리스트(ACL) 규칙은 수량 제한이 없습니다. 객체 액세스 제어 리스트(ACL) 제어가 필요하지 않을 경우 설정하지 마십시오. 기본 버킷 권한을 상속합니다.

#### 사용 예시

[//]: # (.cssg-snippet-put-object-acl)
```js
cos.putObjectAcl({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Key: 'picture.jpg',              /* 필수 */
    ACL: 'public-read',        /* 옵션 */
}, function(err, data) {
    console.log(err || data);
});
```

특정 사용자에게 객체의 모든 권한을 부여합니다.

[//]: # (.cssg-snippet-put-object-acl-user)
```js
cos.putObjectAcl({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Key: 'picture.jpg',              /* 필수 */
    GrantFullControl: 'id="100000000001"' // 100000000001: 루트 계정 uin
}, function(err, data) {
    console.log(err || data);
});
```

AccessControlPolicy를 통해 객체의 쓰기 권한을 부여합니다.

[//]: # (.cssg-snippet-put-object-acl-acp)
```js
cos.putObjectAcl({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Key: 'picture.jpg',              /* 필수 */
    AccessControlPolicy: {
        "Owner": { // AccessControlPolicy에는 반드시 owner가 있습니다.
            "ID": 'qcs::cam::uin/100000000001:uin/100000000001' // 100000000001은 Bucket이 속한 사용자의 QQ 번호
        },
        "Grants": [{
            "Grantee": {
                "ID": "qcs::cam::uin/100000000011:uin/100000000011", // 100000000011은 QQ 번호
            },
            "Permission": "WRITE"
        }]
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                      | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket              | BucketName-APPID 형식의 버킷 이름 | String      | Yes    |
| Region              | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String      | Yes   |
| Key                 | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String      | Yes   |
| ACL                 | 객체의 ACL 속성을 정의합니다. default, private 및 public-read와 같은 열거된 값에 대해서는 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583)의 사전 설정 ACL 섹션을 참고하십시오. <br>**주의: 객체에 대한 액세스 제어가 필요하지 않은 경우 이 매개변수에 대한 기본값을 설정하거나 비워 두십시오. 이러한 방식으로 객체는 저장된 버킷의 권한을 상속합니다.** | String      | No   |
| GrantRead                   | 사용자에게 id="[OwnerUin]" 형식의 읽기 권한을 부여합니다. 쉼표(,)를 사용하여 여러 사용자를 구분할 수 있습니다. <br><li>서브 계정을 승인하려면 다음을 사용하십시오. `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정을 인증하려면 다음을 사용하십시오. `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No   |
| GrantFullControl            | 사용자에게 id="[OwnerUin]" 형식의 전체 권한을 부여합니다. 쉼표(,)를 사용하여 여러 사용자를 구분할 수 있습니다. <br><li>서브 계정을 승인하려면 다음을 사용하십시오. `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>루트 계정을 인증하려면 다음을 사용하십시오. `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>예를 들면 다음과 같습니다. `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No   |
| AccessControlPolicy | 객체의 액세스 제어 리스트(ACL) 속성 정보 설정                        | Object      | No   |
| - Owner             | 객체 소유자 정보                                             | Object      | No   |
| - - ID              | 객체 소유자 ID. 형식: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>루트 계정인 경우, &lt;OwnerUin>과 &lt;SubUin>의 값이 동일합니다. | String      | No   |
| - - DisplayName     | 객체 소유자 이름                                             | String      | No   |
| - Grants            | 권한을 부여받은 대상의 정보 및 권한 정보 리스트                                   | ObjectArray | No   |
| - -Permission      | 권한을 부여받은 대상의 권한 정보 표시. 열거 값: READ, WRITE, READ_ACP, WRITE_ACP, FULL_CONTROL | String      | No   |
| - - Grantee         | 권한을 부여받은 대상의 정보                                               | Object      | No   |
| - - - DisplayName   | 권한을 부여받은 대상의 이름                                               | String      | No   |
| - - - ID            | 권한을 부여받은 대상의 ID. 형식: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>루트 계정인 경우, &lt;OwnerUin>과 &lt;SubUin>의 값이 동일합니다. | String      | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 오류(네트워크 오류 또는 서비스 오류)가 발생하면 반환되는 객체입니다. 요청이 성공하면 이 매개변수는 비어 있습니다. 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data         | 요청이 성공하면 반환되는 객체입니다. 요청이 실패하면 이 매개변수는 비어 있습니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 204, 403, 404 등)             | Number |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |

### 객체 ACL 조회

#### 기능 설명

GET Object acl 인터페이스는 버킷의 객체 액세스 권한을 조회할 때 사용합니다. 버킷 소유자에게만 작업 권한이 주어집니다.

#### 사용 예시

[//]: # (.cssg-snippet-get-object-acl)
```js
cos.getObjectAcl({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'ap-beijing',    /* 필수 */
    Key: 'picture.jpg',              /* 필수 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket        | BucketName-APPID 형식의 버킷 이름 | String           | Yes   |
| Region                 | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String           | Yes   |
| Key    | 객체 키(Object의 이름). 버킷에서의 객체 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String           | Yes   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름            | 매개변수 설명                                                     | 유형        |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err               | 오류(네트워크 오류 또는 서비스 오류)가 발생하면 반환되는 객체입니다. 요청이 성공하면 이 매개변수는 비어 있습니다. 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | Object      |
| - statusCode      | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers         | 요청 시 반환되는 헤더 정보                                           | Object      |
| data              | 요청이 성공하면 반환되는 객체입니다. 요청이 실패하면 이 매개변수는 비어 있습니다.               | Object      |
| - statusCode      | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers         | 요청 시 반환되는 헤더 정보                                           | Object      |
| - ACL             | 객체의 액세스 제어 리스트(ACL) 속성. 열거 값은 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583) 문서에서 default, private, public-read와 같은 객체의 사전 설정 ACL 부분을 참고하십시오. | String      |
| - Owner           | 리소스 소유자 식별                                             | Object      |
| - - ID              | 객체 소유자 ID. 형식: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>루트 계정 ID인 경우, &lt;OwnerUin>과 &lt;SubUin>의 값이 동일합니다. | String      |
| - - DisplayName   | 객체 소유자 이름                                             | String      |
| - Grants            | 권한을 부여받은 대상의 정보 및 권한 정보 리스트                                   | ObjectArray |
| - -Permission      | 권한을 부여받은 대상의 권한 정보 표시. 열거 값: READ, READ_ACP, WRITE_ACP, FULL_CONTROL | String      |
| - - Grantee       | 권한을 부여받은 대상 정보.                                             | Object      |
| - - - DisplayName | 사용자 이름                                                   | String      |
| - - - ID          | 사용자 ID. 형식: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>루트 계정 ID인 경우, &lt;OwnerUin>과 &lt;SubUin>의 값이 동일합니다. | String      |

## 고급 인터페이스(권장)

이러한 메소드는 상위 네이티브 메소드를 캡슐화한 것으로, 멀티파트 복사의 전 과정을 구현합니다. 동시 멀티파트 복사, 중단 지점부터 이어서 전송, 업로드 작업의 취소, 일시 중지 및 재시작 등을 지원합니다.

### 고급 업로드

#### 기능 설명
    
Upload File은 고급 업로드되며, SliceSize 매개변수를 통해서 파일 크기가 일정 수치(기본 1MB)를 초과할 경우 자동으로 멀티파트 업로드되고 그렇지 않으면 간편 업로드 되도록 제어할 수 있습니다.
    
#### 사용 예시

[//]: # (.cssg-snippet-transfer-upload-file)
```js
var uploadFile = function(file) {
    cos.uploadFile({
        Bucket: ’examplebucket-1250000000’, /* 필수 */
        Region: ’COS_REGION’,     /* 버킷이 위치한 리전. 필수 필드 */
        Key: file.name,              /* 필수 */
        FilePath: file.path,                /* 필수 */
        FileSize: file.size,                        /* 필수 */
        SliceSize: 1024 * 1024 * 5,     /* 멀티파트 업로드의 임계값을 트리거하여, 5MB를 초과하면 멀티파트 업로드를 사용하도록 합니다. 옵션 */
        onTaskReady: function(taskId) {                   /* 옵션 */
            console.log(taskId);
        },
        onProgress: function (progressData) {           /* 옵션 */
            console.log(JSON.stringify(progressData));
        },
        onFileFinish: function (err, data, options) {
          console.log(options.Key + ’업로드’ + (err ? ’실패’ : ’완료’));
        },
    }, function(err, data) {
        console.log(err || data);
    });
}

wx.chooseMessageFile({
   count: 10,
   type: 'all',
   success: function(res) {
       uploadFiles(res.tempFiles[0]);
   }
});
```

#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형      | 필수 입력 여부 |
| ------------------------------------------------------------ | ------------------------------------------------------------ | --------- | ---- |
| Bucket                                                       | BucketName-APPID 형식의 버킷 이름 | String    | Yes   |
| Region                                                       | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String    | Yes   |
| Key                                                          | 객체 키(Object의 이름). 버킷에서의 객체 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String    | Yes   |
| FilePath                                                         | 파일 업로드 경로                                                 | String | Yes   |
| FileSize                                                         | 업로드 파일 크기           | Number | Yes   |
| SliceSize                                                    | 파일 크기가 일정 값 이상일 때 멀티파트 업로드 사용, 단위 Byte, 기본값 1048576(1MB), 해당 값보다 작거나 같은 경우 putObject를 통해 업로드, 해당 값보다 클 경우 sliceUploadFile를 통해 업로드                                                     | Number    | No   |
| AsyncLimit                                                   | 멀티파트 업로드의 동시 업로드 수량, 멀티파트 업로드 트리거 시에만 유효                                           | Number    | No   |
| StorageClass                                                 | 객체의 스토리지 유형. STANDARD, STANDARD_IA, ARCHIVE, DEEP_ARCHIVE 등과 같은 열거 값이 있으며, 더 많은 스토리지 유형은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 문서를 참고하십시오.       | String    | No   |
| UploadAddMetaMd5                                             | 업로드 시 객체의 메타데이터 정보에 x-cos-meta-md5에 대입한 객체 콘텐츠의 MD5를 추가합니다. 형식은 32비트 소문자 알파벳 문자열입니다. 예: 4d00d79b6733c9cc066584a02ed03410 | String    | No   |
| onTaskReady                                                  | 업로드 작업 생성 시의 콜백 함수. 1개의 taskId를 반환하며, 업로드 작업의 고유 식별자입니다. 업로드 작업 취소(cancelTask), 중지(pauseTask), 재시작(restartTask)에 사용할 수 있습니다. | Function  | No   |
| - taskId                                                     | 업로드 작업의 번호                                               | String    | No   |
| onProgress                                                   | 파일 업로드 진행률 콜백 함수. 콜백 매개변수는 진행률 객체 progressData입니다.      | Function  | No   |
| - progressData.loaded                                        | 업로드한 파일의 일부 크기. 단위: 바이트(Bytes)                | Number    | No   |
| - progressData.total                                         | 파일의 전체 크기. 단위: 바이트(Bytes)                        | Number    | No   |
| - progressData.speed                                         | 파일의 업로드 속도. 단위: 바이트/초(Bytes/s)                   | Number    | No   |
| - progressData.percent                                       | 파일의 업로드 백분율. 소수점으로 표시합니다(예: 업로드 50%를 0.5로 표시).       | Number    | No   |
| onFileFinish           | 모든 파일의 완료 또는 오류 콜백                                       | String    | Yes   |
| - err                  | 업로드 오류 정보                                               | Object    | No   |
| - data                 | 파일의 완료 정보                                               | Object    | No   |
| - options              | 현재 완료된 파일의 매개변수 정보                                       | Object    | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 요청 과정에서 오류 발생 시 반환되는 객체에는 네트워크 오류와 작업 오류가 포함됩니다. 요청 성공 시 빈칸으로 표시되며, 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730) 문서를 참고하십시오. | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data         | 요청이 성공하면 반환되는 객체입니다. 요청이 실패하면 이 매개변수는 비어 있습니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| - Location   | 업로드된 파일 액세스 주소                                       | String |
| - Bucket     | 멀티파트 업로드의 타깃 버킷, 멀티파트 업로드 트리거 시에만 반환                                        | String |
| - Key        | 객체 키(Object의 이름). 버킷에서의 객체 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. 멀티파트 업로드 트리거 시에만 반환 | String |
| - ETag       | 병합 후 파일의 고유 ID. 형식: "uuid-<파트 수>"<br>예: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`, **주의: 앞뒤에 큰따옴표가 사용됩니다.** | String |
| - VersionId  | 버전 제어를 활성화한 버킷에 객체 업로드 시 반환되는 객체의 버전 ID. 버전 제어를 한 번도 활성화하지 않은 버킷은 해당 매개변수가 반환되지 않습니다. | String |

### 객체 멀티파트 업로드
#### 기능 설명
Slice Upload File은 파일의 멀티파트 업로드에 사용되며, 대용량 파일 업로드에 적합합니다.
#### 사용 예시
[//]: # (.cssg-snippet-transfer-copy-object)
```js
var sliceUploadFile = function (file) {
    var key = file.name;
    cos.sliceUploadFile({
        Bucket: 'examplebucket-1250000000',         /* 필수 */
        Region: 'COS_REGION',                       /* 필수 */
        Key: 'exampleobject',                       /* 필수 */
        FilePath: file.path,                        /* 필수 */
        FileSize: file.size,                        /* 옵션 */
        CacheControl: 'max-age=7200',               /* 옵션 */
        Headers: {                                  /* 옵션 */
            aa: 123,
        },
        Query: {                                     /* 옵션 */
            bb: 123,
        },
        onTaskReady: function(taskId) {              /* 옵션 */
            console.log(taskId);
        },
        onHashProgress: function(info) {             /* 옵션 */
            console.log('check hash', JSON.stringify(info));
        },
        onProgress: function(info) {                 /* 옵션 */
            console.log(JSON.stringify(info));
        }
    }, requestCallback);
};
wx.chooseMessageFile({
    count: 10,
    type: 'all',
    success: function(res) {
        sliceUploadFile(res.tempFiles[0]);
    }
});
```
#### 매개변수 설명

| 매개변수 이름                 | 매개변수 설명                                                     | 유형     | 필수 입력 여부 |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket                 | BucketName-APPID 형식의 버킷 이름 | String   | Yes   |
| Region                 | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String   | Yes   |
| Key                        | 객체 키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String   | Yes   |
| FilePath               | 파일 업로드 경로                                                 | String   | Yes   |
| SliceSize              | 멀티파트 크기                                                     | Number   | No   |
| AsyncLimit             | 멀티파트의 동시 전송량. 멀티파트 업로드 트리거 시에만 유효합니다.                                                  | Number   | No   |
| StorageClass           | 객체의 스토리지 유형. 열거 값은 STANDARD, STANDARD_IA, ARCHIVE 등이 있으며, 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 문서를 참고하십시오.       | String   | No   |
| onTaskReady            | 업로드 작업 생성 시의 콜백 함수. 1개의 taskId를 반환하며, 업로드 작업의 고유 식별자입니다. 업로드 작업 취소(cancelTask), 중지(pauseTask), 재시작(restartTask)에 사용할 수 있습니다. | Function        | No   |
| - taskId               | 업로드 작업의 번호                                               | String   | No   |
| onHashProgress         | 파일의 MD5 값을 계산하는 진행률 콜백 함수. 콜백 매개변수는 진행률 객체 progressData입니다. | Function | No   |
| - progressData.loaded  | 검증된 파일의 일부 크기. 단위: 바이트(Bytes)                | Number   | No   |
| - progressData.total   | 파일의 전체 크기. 단위: 바이트(Bytes)                        | Number   | No   |
| - progressData.speed   | 파일 검증 속도. 단위: 바이트/초(Bytes/s)                   | Number   | No   |
| - progressData.percent | 파일의 검증 백분율. 소수점으로 표시합니다(예: 검증 50%를 0.5로 표시).       | Number    | No   |
| onProgress             | 업로드 파일의 진행률 콜백 함수. 콜백 매개변수는 진행률 객체 progressData입니다.      | Function | No   |
| - progressData.loaded  | 업로드한 파일의 일부 크기. 단위: 바이트(Bytes)                | Number   | No   |
| - progressData.total   | 파일의 전체 크기. 단위: 바이트(Bytes)                        | Number   | No   |
| - progressData.speed   | 파일의 업로드 속도. 단위: 바이트/초(Bytes/s)                   | Number   | No   |
| - progressData.percent | 파일의 업로드 백분율. 소수점으로 표시합니다(예: 업로드 50%를 0.5로 표시).      | Number   | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 오류(네트워크 오류 또는 서비스 오류)가 발생하면 반환되는 객체입니다. 요청이 성공하면 이 매개변수는 비어 있습니다. 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data         | 요청이 성공하면 반환되는 객체입니다. 요청이 실패하면 이 매개변수는 비어 있습니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| - Location   | 객체의 외부 네트워크 액세스 도메인 생성                                       | String |
| - Bucket     | 멀티파트 업로드의 타깃 버킷                                         | String |
| - Key                  | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |
| - ETag       | 병합 후 파일의 고유 ID. 형식: "uuid-<파트 수>"<br>예: `"22ca88419e2ed4721c23807c678adbe4c08a7880-3"`, **주의: 앞뒤에 큰따옴표가 사용됩니다.** | String |
| - VersionId  | 버전 제어를 활성화한 버킷에 객체 업로드 시 반환되는 객체의 버전 ID. 버전 제어를 한 번도 활성화하지 않은 버킷은 해당 매개변수가 반환되지 않습니다. | String |


### 객체 복사

#### 기능 설명

Slice Copy File은 멀티파트 복사를 통해 원본 경로에서 타깃 경로로 파일을 복사하는 데 사용합니다. 복사 과정에서 객체 메타데이터와 ACL이 수정될 수 있습니다. 사용자는 해당 인터페이스를 통해 파일 이동, 파일 이름 변경, 파일 속성 수정 및 사본 생성을 할 수 있습니다.

#### 메소드 프로토타입

Slice Copy File을 호출하여 작업합니다.

[//]: # (.cssg-snippet-transfer-copy-object)
```js
cos.sliceCopyFile({
    Bucket: ’examplebucket-1250000000’,                               /* 필수 */
    Region: 'ap-beijing',                                  /* 필수 */
    Key: '1.zip',                                            /* 필수 */
    CopySource: 'test-1250000000.cos.ap-guangzhou.myqcloud.com/2.zip', /* 필수 */
    onProgress:function (progressData) {                     /* 옵션 */
        console.log(JSON.stringify(progressData));
    }
},function (err,data) {
    console.log(err || data);
});
```

#### 매개변수 설명

| 매개변수 이름                | 매개변수 설명                                                     | 유형     | 필수 입력 여부 |
| ---------------------- | ------------------------------------------------------------ | -------- | ---- |
| Bucket                 | BucketName-APPID 형식의 버킷 이름 | String   | Yes   |
| Region                 | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String   | Yes   |
| Key                        | 객체 키(Object의 이름), 객체는 버킷의 고유 표식입니다. 세부 사항은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String   | Yes   |
| CopySource             | 소스 객체의 URL입니다. URL 매개변수 ?versionId=&lt;versionId>를 사용하여 이전 버전을 지정할 수 있습니다. | String   | Yes   |
| ChunkSize              | 멀티파트 복사 시 파트 당 바이트 수. 기본값: 1048576(1MB)          | Number   | No   |
| SliceSize              | 파일 크기가 일정 값 초과 시 멀티파트 복사를 사용하도록 하는 매개변수. 단위: Byte, 기본값: 5G. 이 값 이하인 경우 putObjectCopy를 사용해 업로드하고, 초과하는 경우 sliceCopyFile을 사용해 업로드합니다. | Number   | No   |
| onProgress             | 업로드 파일의 진행률 콜백 함수. 콜백 매개변수는 진행률 객체 progressData입니다.      | Function | No   |
| - progressData.loaded  | 업로드한 파일의 일부 크기. 단위: 바이트(Bytes)                | Number   | No   |
| - progressData.total   | 파일의 전체 크기. 단위: 바이트(Bytes)                        | Number   | No   |
| - progressData.speed   | 파일의 업로드 속도. 단위: 바이트/초(Bytes/s)                   | Number   | No   |
| - progressData.percent | 파일의 복사 백분율. 소수점으로 표시합니다. 예: 복사 50%를 0.5로 표시       | Number   | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 오류(네트워크 오류 또는 서비스 오류)가 발생하면 반환되는 객체입니다. 요청이 성공하면 이 매개변수는 비어 있습니다. 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | Object |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data         | 요청이 성공하면 반환되는 객체입니다. 요청이 실패하면 이 매개변수는 비어 있습니다.               | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| - Location   | 객체의 외부 네트워크 액세스 도메인 생성                                       | String |
| - Bucket     | 멀티파트 업로드의 타깃 버킷                                         | String |
| - Key                  | 객체 키(Object의 이름). 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |
| - ETag       | 병합 후 파일의 MD5 알고리즘 검증값<br>예: `"22ca88419e2ed4721c23807c678adbe4c08a7880"`, **주의: 앞뒤에 큰따옴표가 사용됩니다.** | String |
| - VersionId  | 버전 제어를 활성화한 버킷에 객체 업로드 시 반환되는 객체의 버전 ID. 버전 제어를 한 번도 활성화하지 않은 버킷은 해당 매개변수가 반환되지 않습니다. | String |

### 일괄 업로드

#### 기능 설명

방법1:
일괄 업로드는 putObject와 sliceUploadFile을 직접 여러 번 호출하여 일괄 업로드 효과를 구현할 수 있습니다. 인스턴스화 매개변수 FileParallelLimit을 통해 파일의 동시 전송 수를 제한합니다. 기본값은 3개입니다.

방법2:
cos.uploadFiles를 호출하여 일괄 업로드할 수 있습니다. 매개변수 SliceSize를 전송하여 파일 크기가 일정 값을 초과할 때 멀티파트 업로드를 사용하도록 제어할 수 있습니다. 다음은 uploadFiles 방법 설명입니다.

#### 메소드 프로토타입

uploadFiles를 호출하여 작업합니다.

[//]: # (.cssg-snippet-transfer-batch-upload-objects)
```js
var uploadFiles = function(files) {
    var fileList = files.map(function(file) {
        return Object.assign(file, {
            FilePath: file.path,
            FileSize: file.size,
            Bucket: 'examplebucket-1250000000',
            Region: 'COS_REGION',
            Key: file.name,
            onTaskReady: function(taskId) {
              /* taskId로 큐 작업을 통해 cos.cancelTask(taskId) 업로드 취소, cos.pauseTask(taskId) 업로드 중지, cos.restartTask(taskId), 업로드 재시작을 진행 할 수 있습니다. */
              console.log(taskId);
            }
        });
    });
    cos.uploadFiles({
        files: fileList,
        SliceSize: 1024 * 1024 * 10,    /* 10MB 초과 시 멀티파트 업로드 설정 */
        onProgress: function (info) {
            var percent = parseInt(info.percent * 10000) / 100;
            var speed = parseInt(info.speed / 1024 / 1024 * 100) / 100;
            console.log(’진행률: ’ + percent + ’%; 속도: ’ + speed + ’Mb/s;’);
        },
        onFileFinish: function (err, data, options) {
            console.log(options.Key + ’업로드’ + (err ? ’실패’ : ’완료’));
        },
    }, function (err, data) {
        console.log(err || data);
    });
}
wx.chooseMessageFile({
    count: 10,
    type: 'all',
    success: function(res) {
        uploadFiles(res.tempFiles);
    }
});
```

#### 매개변수 설명

| 매개변수 이름                 | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ---------------------- | ------------------------------------------------------------ | ------ | ---- |
| files                  | 파일 리스트. 모든 항목은 putObject와 sliceUploadFile에 전송되는 매개변수 객체입니다. | Object    | Yes   |
| - Bucket               | BucketName-APPID 형식의 버킷 이름 | String    | Yes   |
| - Region               | 버킷이 위치한 리전. 열거 값은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오. | String    | Yes   |
| - Key                  | 객체 키(Object의 이름). 버킷에서의 객체 고유 식별자입니다. 자세한 내용은 [객체 개요](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String    | Yes   |
| - FilePath             | 파일 업로드 경로                                                 | String | Yes   |
| - FileSize             | 파일 업로드 크기                                                 | Number | Yes   |
| - onTaskReady                                                  | 업로드 작업 생성 시의 콜백 함수. 1개의 taskId를 반환하며, 업로드 작업의 고유 식별자입니다. 업로드 작업 취소(cancelTask), 중지(pauseTask), 재시작(restartTask)에 사용할 수 있습니다. | Function  | No   |
| -- taskId                                                     | 업로드 작업의 번호                                               | String    | No   |
| SliceSize              | 파일 크기가 일정 값 초과 시 멀티파트 업로드를 사용하도록 하는 매개변수(단위: Byte), 기본값1048576(1MB). 이 값 이하인 경우 putObject를 사용해 업로드하고, 초과하는 경우 sliceUploadFile을 사용해 업로드합니다. | Number | Yes   |
| onProgress             | 모든 작업의 진행률이 종합 계산된 업로드 진행률                            | String    | Yes   |
| - progressData.loaded  | 업로드한 파일의 일부 크기. 단위: 바이트(Bytes)                | Number           | No   |
| - progressData.total   | 파일의 전체 크기. 단위: 바이트(Bytes)                        | Number           | No   |
| - progressData.speed   | 파일의 업로드 속도. 단위: 바이트/초(Bytes/s)                   | Number           | No   |
| - progressData.percent | 파일의 업로드 백분율. 소수점으로 표시합니다(예: 업로드 50%를 0.5로 표시).      | Number | No   |
| onFileFinish           | 모든 파일의 완료 또는 오류 콜백                                       | String    | Yes   |
| - err                  | 업로드 오류 정보                                               | Object    | No   |
| - data                 | 파일의 완료 정보                                               | Object    | No   |
| - options              | 현재 완료된 파일의 매개변수 정보                                       | Object    | No   |

#### 콜백 함수 설명

```
function(err, data) { ... }
```

| 매개변수 이름       | 매개변수 설명                                                     | 유형        |
| ------------ | ------------------------------------------------------------ | ----------- |
| err          | 오류(네트워크 오류 또는 서비스 오류)가 발생하면 반환되는 객체입니다. 요청이 성공하면 이 매개변수는 비어 있습니다. 자세한 내용은 [오류 코드](https://intl.cloud.tencent.com/document/product/436/7730)를 참고하십시오. | Object      |
| - statusCode | 요청 시 반환되는 HTTP 상태 코드(예: 200, 403, 404 등)                  | Number      |
| - headers    | 요청 시 반환되는 헤더 정보                                           | Object      |
| data         | 요청이 성공하면 반환되는 객체입니다. 요청이 실패하면 이 매개변수는 비어 있습니다.               | Object      |
| - files      | 모든 파일의 error 또는 data                                     | ObjectArray |
| - - error    | 업로드 오류 정보                                               | Object      |
| - - data     | 파일 완료 정보                                               | Object      |
| - - options  | 현재 완료된 파일의 매개변수 정보   

### 큐 업로드

미니프로그램 SDK는 putObject에서 보낸 업로드 작업을 모두 큐에 기록하며 큐에 관한 방법은 다음과 같습니다.

1. cos.getTaskList로 작업 리스트를 가져올 수 있습니다.
2. cos.pauseTask, cos.restartTask, cos.cancelTask로 작업을 진행합니다.
3. cos.on(’list-update’, callback);으로 리스트와 진행률 변화를 수신할 수 있습니다.

전체적인 큐 사용 예시는 [demo-queue](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo/queue)를 참고하십시오.

#### 업로드 작업 취소

taskId에 따라 업로드 작업을 취소합니다.

**사용 예시**

[//]: # (.cssg-snippet-transfer-upload-cancel)
```js
var taskId = ’xxxxx’;                   /* 필수 */
cos.cancelTask(taskId);
```

**매개변수 설명**

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | 파일 업로드 작업 번호. putObject 방법을 호출할 때 TaskReady 콜백이 해당 업로드 작업의 taskId를 반환합니다. | String | Yes   |

#### 업로드 작업 일시 중지

taskId에 따라 업로드 작업을 일시 중지합니다.

**사용 예시**

[//]: # (.cssg-snippet-transfer-upload-pause)
```js
var taskId = ’xxxxx’;                   /* 필수 */
cos.pauseTask(taskId);
```

**매개변수 설명**

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | 파일 업로드 작업 번호. putObject 방법을 호출할 때 TaskReady 콜백이 해당 업로드 작업의 taskId를 반환합니다. | String | Yes   |

#### 업로드 작업 재시작

taskId에 따라 업로드 작업을 재시작합니다. 사용자가 수동으로 중단(pauseTask를 호출하여 중단)하거나 오류로 중단된 업로드 작업을 재시작하는 데 사용할 수 있습니다.

**사용 예시**

[//]: # (.cssg-snippet-transfer-upload-resume)
```js
var taskId = ’xxxxx’;                   /* 필수 */
cos.restartTask(taskId);
```

**매개변수 설명**

| 매개변수 이름 | 매개변수 설명                                                     | 유형   | 필수 입력 여부 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| taskId | 파일 업로드 작업 번호. putObject를 호출할 때 TaskReady 콜백이 해당 업로드 작업의 taskId를 반환합니다. | String | Yes |


