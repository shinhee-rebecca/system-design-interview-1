## joel 13장 질문

### Q. 한글 처리: 한글의 경우 초성/중성/종성으로 나눠서 트라이를 구성할지, 완성형 글자 단위로 할지?
- 구글 "ㄱ" 검색
```
[Request]
https://www.google.com/complete/search?q=%E3%84%B1&cp=1&client=gws-wiz&xssi=t&gs_pcrt=undefined&hl=ko&authuser=0&psi=Y_-ZaJ-gD-Db1e8P0K-F8Qg.1754922851618&dpr=1.600000023841858

[Response]
)
]
}'
[[["\u003cb\u003e국토교통부\u003c\/b\u003e",0,[3]],["\u003cb\u003e감염\u003c\/b\u003e",0,[3]],["\u003cb\u003e김숙\u003c\/b\u003e",0,[3]],["\u003cb\u003e공매도\u003c\/b\u003e",0,[3]],["\u003cb\u003e구글번역\u003c\/b\u003e",0,[512,433,131]],["구글",46,[512,433,465,131,199],{"lm":[],"zh":"구글","zi":"","zp":{"gs_ssp":"eJzj4tTP1TcwMU02T1JgNGB0YPBie7V1zasdDQBH6QfD"},"zs":"https://encrypted-tbn0.gstatic.com/images?q\u003dtbn:ANd9GcTB0ZPX6y3sf_lL4QGQqjOYfVitXSTIH4v9vF8UnBOqx0ChrH__gxsSWGnVmA\u0026s\u003d10"}],["김문수",46,[512,433,131],{"lm":[],"zh":"김문수","zi":"전 대한민국 고용노동부 장관","zp":{"gs_ssp":"eJzj4tTP1TdISjM2qjRg9OJ8tbPh9ZodbzpmAABYJAm3"},"zs":"https://encrypted-tbn0.gstatic.com/images?q\u003dtbn:ANd9GcRW1_xc2WtmOdEBJ7irDNBqAqZ19MJ4DAFhw98Z0faduW_gWCpWq3RaZrfgSA\u0026s\u003d10"}],["\u003cb\u003e건강\u003c\/b\u003e",0,[3]],["\u003cb\u003e극한 호우\u003c\/b\u003e",0,[3]],["\u003cb\u003e고용24\u003c\/b\u003e",0,[512,433,131]]],{"ag":{"a":{"40024":["","",1,20]}},"q":"IIEgdVE-j65Vjjcw1JOG4pswTzk"}]
```
- 미리 초성에 대해서는 캐싱을 해두지 않았을까... 이후 한글자 다 쓰면 트라이 탐색

### Q. 오타(typo)나 한영 변환 같은 유사 검색어는 어떻게 처리할 수 있을까요?
1. 편집 거리(Edit Distance) 알고리즘 활용:
- Levenshtein Distance 같은 알고리즘으로 두 문자열 간의 유사도를 측정합니다. 사용자가 입력한 검색어와 일정 거리(e.g., 1~2글자 차이) 내에 있는 인기 검색어를 추천해 줄 수 있습니다. (예: '샘성' -> '삼성')

2. N-gram 기반 인덱싱:
- 문자열을 N개의 글자 단위로 잘라 인덱싱합니다. 일부 오타가 있더라도 공통된 N-gram을 많이 포함하는 단어를 찾아낼 수 있어 유사어 검색에 효과적입니다.

3. 과거 데이터 기반 매핑 테이블 구축:
- 사용자들이 오타를 입력했다가 바로 올바른 단어로 다시 검색하는 로그 데이터를 분석합니다. (예: 'kㅏ카오' -> '카카오' 검색 로그) 이를 통해 자주 발생하는 오타-정타 쌍을 미리 테이블로 만들어두고, 오타가 들어오면 바로 정타로 변환하여 결과를 보여줍니다. 한영 변환 실수(e.g., 'dkssud' -> '안녕')도 이 방식으로 처리할 수 있습니다.

4. 음소(Phonetic) 알고리즘:
- 'Soundex' 와 같이 발음이 비슷한 단어를 같은 코드로 변환하는 알고리즘을 활용하여, 발음은 비슷하지만 철자가 다른 단어들을 찾아낼 수 있습니다.

### Q. 샤드 리밸런싱: 새로운 검색어 트렌드가 생겼을 때 샤드 간 부하를 어떻게 재분산시킬까? (Consistent Hashing?)

