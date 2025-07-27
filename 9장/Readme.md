# 웹 크롤러
**웹 크롤러(web crawler)**는 조직적, 자동화된 방법으로 월드 와이드 웹을 탐색하는 컴퓨터 프로그램이다. 
대게 시드(seeds)라고 불리는 URL 리스트에서부터 시작하여, 페이지의 모든 하이퍼링크를 인식하여 URL 리스트를 갱신한다.

<img width="505" height="399" alt="스크린샷 2025-07-26 오후 6 55 31" src="https://github.com/user-attachments/assets/7796b479-4001-4ca2-985c-1ed0ff2a3ac5" />

출처: [위키피디아](https://ko.wikipedia.org/wiki/%EC%9B%B9_%ED%81%AC%EB%A1%A4%EB%9F%AC)

## 활용
1. 검색 엔진 인덱싱(search engine indexing) : 검색 엔진을 위한 로컬 인덱스(local index) - ex 구글의 Googlebot
2. 웹 아카이빙(web archiving) : 보존 목적으로 많은 국립 도서관이 웹을 아카이빙
3. 웹 마이닝(web mining): 웹 자원 분석 목적
4. 웹 모니터링: ex. 저작권 / 상표권 침해 사례 모니터링

## 요구사항
### 면접관의 요구사항
1. 용도 : 검색 엔진 인덱싱
2. 매달 10억개의 웹 페이지 수집(QPS= 400페이지/초, 최대 400*2 QPS)
3. 5년간 저장 (페이지의 평균 크기는 500k라고 가정하면, 월에 500TB)
4. 중복된 페이지는 무시
<img width="2329" height="1000" alt="image" src="https://github.com/user-attachments/assets/642ca729-d17c-4b14-a2a7-46fd699c3b50" />

### 좋은 웹 크롤러의 요구사항
1. 규모 확장성(?): 병행성을 활용한 효과적인 웹 크롤링
2. 안정성(robustness): 잘못 작성된 HTML, 반응 없는 서버, 악성코드 링크 등 비정상적인 입력이나 환경에 잘 대응할 수 있어야 한다.
3. 예절(politeness): 짧은 시간 동안 너무 많은 요청을 보내서는 안된다.
4. 확장성(extensibility): 새로운 형태의 콘텐츠(ex. 이미지)를 지원하기 쉬워야 한다.

5. 
