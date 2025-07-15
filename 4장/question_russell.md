# russell 4장 질문지

## redis외에 사용하는 rate limiter를 위한 도구는 어떤것이 있는가?
ex) 파티션 조절, arcus(redis와 유사하게 사용), Count-min sketch

## rate limiter와 Circuit Breaker 차이를 설명하시오.

<details>
<summary><strong>Rate Limiter (레이트 리미터)</strong></summary>

- **목적**: 요청 속도 제한을 통한 과부하 방지
- **기능**: 시간 단위 내 허용 가능한 요청 수를 제한
- **성격**: 예방적 조치
- **핵심**: "얼마나 빨리 요청하는가?"

**주요 특징:**
- 미리 정의된 규칙에 따라 요청 차단
- 시간 기반 윈도우 사용
- 공정한 리소스 분배
- 시스템 과부하 예방

</details>

<details>
<summary><strong>Circuit Breaker (서킷 브레이커)</strong></summary>

- **목적**: 장애 전파 방지 및 시스템 복구 시간 확보
- **기능**: 실패율이 높은 서비스에 대한 호출 차단
- **성격**: 장애 발생 후 대응
- **핵심**: "서비스가 정상인가?"

**주요 특징:**
- 실패율 기반 동적 차단
- 3단계 상태 전환 (Closed/Open/Half-Open)
- 빠른 실패 처리
- 시스템 복구 시간 확보

</details>

## rate limiter 모니터링 툴로 무엇을 사용하는가?

ex) [prometheus](https://grafana.com/grafana/dashboards/14091-redis-dashboard-for-prometheus-redis-exporter-1-x/)
