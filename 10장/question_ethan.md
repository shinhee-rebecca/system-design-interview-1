## 알림 중복 / 누락은 어떻게 줄일 수 있을까?
### Kafka의 Semantic guarantees
    - At most once : 메시지는 한 번만 전달되며, 시스템 장애가 발생하는 경우 메시지가 손실되어 다시 전달되지 않을 수 있음
    - At least once: 시스템 장애가 발생하더라도 메시지는 손실되지 않지만, 두 번 이상 전송될 수 있습니다.
    - Exactly once: 시스템 일부에 장애가 발생하더라도 메시지가 손실되거나 두 번 읽히는 일이 없음.

참고 1: [올리브영 Kafka 메시지 중복 및 유실 케이스별 해결 방법](https://oliveyoung.tech/2024-10-16/oliveyoung-scm-oms-kafka/)
참고 2: [Kafka Message Delivery Guarantees](https://docs.confluent.io/kafka/design/delivery-semantics.html)

## 알림 발송 실패에 대한 Retry 정책은 어떻게 설계해야 안전할까?
	- 즉시 재시도 vs Exponential Backoff vs Dead Letter Queue
