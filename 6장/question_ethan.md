1. 읽기 연산에 대한 정족수(Quorum)은 왜 필요한가?
    - 읽기 정족수란 클라이언트가 읽기 요청을 보낼 때 응답을 받아야 하는 노드의 최소 개수를 의미하며, 동일한 응답을 보낸 노드의 수를 의미하지 않음
    - 이는 읽기를 통해 최신 상태를 근사하기 위함임
    - majority quorum이란, [n/2] + 1개의 노드가 응답하거나 동의해야 정족수가 성립하는 방식으로 read, write가 최소 하나 이상 겹치게 되어 일관성이 높아지게 되며, n = 3일 때 최소 한 개의 장애를 견딜 수 있음
    - 출처: [[강의 정리] Distributed System 5.2: Quorums (정족수)](https://hayz.tistory.com/entry/%EA%B0%95%EC%9D%98-%EC%A0%95%EB%A6%AC-Distributed-System-52-Quorums-%EC%A0%95%EC%A1%B1%EC%88%98)
 
2. 중재자(coordinator)는 누구인가
    - Dynamo DB는 leaderless replication 접근 방식을 사용했을 때는 해시링에서 처음 만나는 노드를 Coordinator로 지정한 것으로 보임 (저장소에 따라 다를 수 있음)
    - 이후에는 Multi-Paxos를 활용한 leader based replication을 적용한 것으로 보임
    - 참고로 **majority quorom에서도 linearizability(선형성)을 보장받지 못할 수 있음**
    - 출처: [DynamoDB, Ten Years Later](https://www.mydistributed.systems/2022/10/dynamodb-ten-years-later.html?utm_source=chatgpt.com)
3. 영구 장애 동안 발생한 차이를 동기화하는 동안 발생하는 쓰기 데이터는? (즉, 머클 트리를 구성하고, 동기화 하는 동안에 정상 노드에 쓰기된 데이터는?)
