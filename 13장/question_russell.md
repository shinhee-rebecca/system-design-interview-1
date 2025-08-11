# 검색어 자동완성 시스템

1. [Trie](https://ko.wikipedia.org/wiki/%ED%8A%B8%EB%9D%BC%EC%9D%B4_(%EC%BB%B4%ED%93%A8%ED%8C%85))를 이용하여 글자수 제한을 두고 마지막자가 될 수 있으면 masking하고 검색된 수를 기록해둔다.
2. 만약 처음부터가 아닌 패턴 매칭이 필요한 경우 [아호코라식](https://ko.wikipedia.org/wiki/%EC%95%84%ED%98%B8_%EC%BD%94%EB%9D%BC%EC%8B%9D_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)을 이용한다.

이후 인기 검색어에 대해 캐시처리를한다.

## 질문

1. 부서에서 특수한 케이스를 위해 따로 사용하는 자료구조가 있는가?

2. 아호코라식을 이용할 경우 어떻게 설계해야할까?
