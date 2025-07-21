### 1. redis는 cap 이론에서 어떤 쪽을 선택했을까?
by GPT

> 🔍 Redis는 기본적으로 AP 지향
> ✔️ A (Availability): 고가용성
> Redis는 단일 인스턴스일 경우 매우 빠르고 항상 응답 가능하게 설계됨.
> Redis Sentinel, Redis Cluster 등은 장애 발생 시 자동 failover를 통해 서비스 중단 없이 처리하려 함.
>
> ✔️ P (Partition tolerance): 네트워크 분할 대응
> 분산 환경에서는 언제든지 네트워크 분할이 발생할 수 있음.
> Redis는 클러스터 환경에서도 분할 상황을 감지하고 일부 노드를 격리하거나 마스터를 교체해서 동작을 유지함.
>
> ✖️ C (Consistency): 강한 일관성은 보장하지 않음
> Redis replication (마스터-슬레이브) 구조에서는 슬레이브가 지연될 수 있으므로, **강한 일관성(Strong Consistency)**을 보장하지 않음.
>
> 클러스터 환경에서는 어떤 노드에 쓴 데이터가 다른 노드에서 곧바로 읽히지 않을 수 있음.
> 네트워크 파티션이 생겼을 때, 예전 마스터가 여전히 요청을 처리하면서 split-brain 문제가 발생할 수 있음 (이걸 막기 위해 Sentinel은 다수 투표 기반으로 failover를 수행).

