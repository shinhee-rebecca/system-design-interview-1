1. 루아스크립트를 사용하면, 불필요한 네트워크 비용 및 경쟁 조건은 해소할 수 있지만, Redis는 싱글스레드이므로, lock을 거는 것과 같지 않나? (71p)
    - Redis HA는 싱글스레드임에도 TPS를 어떻게 [40K](https://wiki.daumkakao.com/spaces/INFRASVCEXT/pages/1646958623/%EC%9D%B4%EC%A0%84+%EC%A0%88%EC%B0%A8+Redis+HA+Prod%EB%A1%9C+%EC%9D%B4%EC%A0%84)나 받아주는거지?
3. 깜짝 세일 같은 이벤트로 트래픽이 급증하는 경우, **토큰 버킷**이 왜 적합할까? (73p)
4. 각 부서에서는 경성(hard), soft(연성)의 처리율 제한을 사용하는 케이스가 있나요?
5. rate limit 이외에 [bulkhead](https://learn.microsoft.com/en-us/azure/architecture/patterns/bulkhead)를 활용하는 부서가 있나요?
