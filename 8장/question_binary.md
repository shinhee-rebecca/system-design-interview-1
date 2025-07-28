# kibana는 어떻게 short url을 만들까?

## 참조

- https://github.com/elastic/kibana/issues/12840
- https://github.com/elastic/kibana/issues/98110

### short url 생성 API 호출 예시

```bash
{
  "locatorId": "LEGACY_SHORT_URL_LOCATOR",
  "params": {
    "url": "/app/discover#/?_a=(columns:!(),filters:!(),index:dd357290-d6ef-11ef-81fe-ab71fe9932d2,interval:auto,query:(language:kuery,query:%27%27),sort:!(!(%27@timestamp%27,desc)))&_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-7d%2Fd,to:now))"
  }
}
```

```bash
{
    "id": "101b8120-6bc6-11f0-aabc-d7b0d09db3e3",
    "locator": {
        "id": "LEGACY_SHORT_URL_LOCATOR",
        "version": "7.17.26",
        "state": {
            "url": "/app/discover#/?_a=(columns:!(),filters:!(),index:dd357290-d6ef-11ef-81fe-ab71fe9932d2,interval:auto,query:(language:kuery,query:%27%27),sort:!(!(%27@timestamp%27,desc)))&_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-7d%2Fd,to:now))"
        }
    },
    "accessCount": 0,
    "accessDate": 1753715886642,
    "createDate": 1753715886642,
    "slug": "gjMqd",
    "url": ""
}
```

## 🔄 slug 기반 short URL 생성 원리

### 1. 사용자가 요청 → `locatorId` + `params` + `humanReadableSlug`

- `locatorId`: 어떤 Kibana 앱인지 지정 (`DISCOVER_APP_LOCATOR`, `DASHBOARD_APP_LOCATOR` 등)
- `params`: 이 앱의 특정 상태 (쿼리, 타임레인지 등)
- `humanReadableSlug`: 사람이 읽기 좋은 slug를 만들라는 지시

---

### 2. Kibana 내부 처리 흐름

### 🧠 내부적으로 처리되는 흐름:

1. Kibana는 `locatorId` + `params`를 직렬화(serialize)합니다.
2. 그 상태 값을 `.kibana` 인덱스에 **Saved Object**로 저장합니다. `type: url` 또는 `type: short_url`
3. `slug`를 자동 생성하거나, 직접 명시하지 않으면 `humanReadableSlug`를 기반으로 문자열 생성기(예: kebab-case transformer + 랜덤 문자열 조합)를 사용합니다.
4. 저장된 객체의 `_id`와 `slug`를 바탕으로 Kibana는 아래와 같은 단축 URL을 구성합니다:
    
    ```
    perl
    복사편집
    https://kibana.example.com/goto/{slug}
    
    ```
    

---

### 3. 접근 시 흐름 (slug 리졸브)

- 사용자가 `/goto/discover-status-200-logs`에 접근하면:
    1. Kibana는 `.kibana` 인덱스에서 `slug` 필드가 `discover-status-200-logs`인 saved object를 검색합니다.
    2. 내부에 저장된 `locator` 정보를 바탕으로 원래의 Kibana 앱 URL (e.g., `/app/discover#...`)을 복원합니다.
    3. 해당 Kibana 앱 URL로 **302 리다이렉트** 합니다.
 
# 카카오에서 short url을 생성하는 서비스는 어떻게 만들고 있을까?
