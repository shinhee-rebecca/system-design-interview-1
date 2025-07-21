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

### 2. redis는 장애 감지와 처리를 어떻게 할까?

redis에는 sentinel이라는 고가용성 컴포넌트가 있다. 

https://redis.io/docs/latest/operate/oss_and_stack/management/sentinel/

> ## 📡 Redis Sentinel의 장애 감지와 처리 방식
>
> Redis Sentinel은 Redis의 고가용성(HA)을 위한 구성 요소로, 장애 감지와 자동 장애 조치(Failover)를 담당한다.
>
> ---
>
> ### 1. 장애 감지 (Failure Detection)
>
> Sentinel은 Redis 노드(마스터/슬레이브 포함)에 주기적으로 `PING` 명령을 보내서 생존 여부를 확인한다.
>
> - **Subjectively Down (`sdown`)**  
>   하나의 Sentinel이 마스터로부터 일정 시간 이상 `PONG` 응답을 받지 못하면 `sdown` 상태로 간주한다.  
>   기준은 `down-after-milliseconds` 설정 값 (기본: 5000ms).
>
> - **Objectively Down (`odown`)**  
>   여러 Sentinel이 해당 마스터가 `sdown` 상태라고 판단하면, 투표(quorum)를 통해 `odown`으로 확정한다.  
>   이 판단을 통해 장애 조치 절차가 시작된다.
>
> ---
>
> ### 2. 장애 처리 (Failover Handling)
>
> 장애가 확정되면 Sentinel은 다음과 같은 단계로 자동 장애 조치를 수행한다.
>
> 1. **마스터 후보 슬레이브 선정**  
>    - replication offset이 최신인 슬레이브  
>    - `slave-priority` 값이 높은 노드  
>    - 연결 상태가 안정적인 노드
>
> 2. **새 마스터 승격**  
>    - 선택된 슬레이브에게 `SLAVEOF NO ONE` 명령을 내려 마스터로 전환
>
> 3. **나머지 슬레이브 재구성**  
>    - 기존의 다른 슬레이브 노드들에게 새 마스터를 따라가도록 `SLAVEOF <new-master>` 명령 전송
>
> 4. **Sentinel 상태 동기화**  
>    - 모든 Sentinel이 새로운 마스터 정보를 공유하고, 감시 대상을 새롭게 설정함
>
> ---
>
> ### 3. 장애 조치 순서 요약
>
> 1. Sentinel이 `PING`으로 노드를 감시함  
> 2. 하나가 `sdown` 판단 → 여러 Sentinel이 동의하면 `odown` 확정  
> 3. 리더 Sentinel 선출  
> 4. 리더가 새 마스터 후보 선택 후 승격  
> 5. 나머지 슬레이브를 새 마스터로 전환  
> 6. Sentinel들이 상태를 모두 동기화
>
> ---
>
> ### 📌 요약: 장애 감지 & 처리 핵심
>
> | 단계 | 설명 |
> |------|------|
> | **PING 감시** | Sentinel이 Redis 노드에 주기적으로 PING |
> | **sdown** | 하나의 Sentinel이 감지한 잠정적 장애 상태 |
> | **odown** | 복수 Sentinel이 합의한 확정 장애 상태 |
> | **리더 선출** | 장애 조치를 수행할 Sentinel 결정 |
> | **PROMOTE** | 슬레이브 → 마스터 승격, 나머지 슬레이브 재구성 |

### 3. 어떤 시스템 특성이 CP에 적합하고, AP에 적합할까?
