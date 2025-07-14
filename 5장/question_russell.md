# 5장 russell 질문지

## ring hash의 장단점과 부서에서 사용하는/사용하지 않는 이유
- 장점
  - 노드 추가/제거 시 최소한의 재분배
  - 균등한 부하 분산
  - 장애 처리 용이성
- 단점
  - 메모리 오버헤드
  - 구현 복잡도
  - 핫스팟 문제 가능성
 
## 각 부서별 데이터를 서버에 나누는 기준

ex) user_id, ...

## 부서별 다시 샤딩하는 방법

ex) binlog로 snapshot 생성 후 이를 이용하여 전체 재적재 및 streaming을 통한 sync


## 부서별 사용하는 hash 기법 및 사용처

ex) binlog 데이터 비교시에 md5해시를 이용.


#### 구글의 jump consistent hash code
```cpp

int32_t JumpConsistentHash(uint64_t key, int32_t num_buckets) {
   int64_t b = 1,   j = 0;
   while (j < num_buckets) {
        b = j;
        key = key * 2862933555777941757ULL + 1;
        j = (b + 1) * (double(1LL << 31) / double((key >> 33) + 1));
    }
    return b;
}
```
#### kafka의 murmur hash
```cpp
static inline uint32_t murmur_32_scramble(uint32_t k) {
    k *= 0xcc9e2d51;
    k = (k << 15) | (k >> 17);
    k *= 0x1b873593;
    return k;
}
uint32_t murmur3_32(const uint8_t* key, size_t len, uint32_t seed)
{
	uint32_t h = seed;
    uint32_t k;
    /* Read in groups of 4. */
    for (size_t i = len >> 2; i; i--) {
        // Here is a source of differing results across endiannesses.
        // A swap here has no effects on hash properties though.
        memcpy(&k, key, sizeof(uint32_t));
        key += sizeof(uint32_t);
        h ^= murmur_32_scramble(k);
        h = (h << 13) | (h >> 19);
        h = h * 5 + 0xe6546b64;
    }
    /* Read the rest. */
    k = 0;
    for (size_t i = len & 3; i; i--) {
        k <<= 8;
        k |= key[i - 1];
    }
    // A swap is *not* necessary here because the preceding loop already
    // places the low bytes in the low places according to whatever endianness
    // we use. Swaps only apply when the memory is copied in a chunk.
    h ^= murmur_32_scramble(k);
    /* Finalize. */
	h ^= len;
	h ^= h >> 16;
	h *= 0x85ebca6b;
	h ^= h >> 13;
	h *= 0xc2b2ae35;
	h ^= h >> 16;
	return h;
}
```


