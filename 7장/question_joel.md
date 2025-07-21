## joel 7장 질문

### Q. 부서에서 특정 중복되지 않는 key를 만드는 방법을 소개해주세요.
- 여러 데이터를 엮어서 유일키를 만드는 방식 많이 쓰는 듯 (트위터 스노플레이크처럼)
- 알림톡 serialNumber는 `날짜-숫자|문자열`
- milliseconds도 겹칠 수 있어 nanotime을 사용하여 redis lock 잡을 key를 생성했던 경험
