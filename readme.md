### 240822
# Elasticsearch
### 써야 할 건 아니고 공부 목적으로 관련 블로그들을 읽어보는 중이다. AWS에서도 종종 나왔기 때문에 어떤 기능이 있는지 궁금했다.
### 여기서는 elasticsearch를 ES라고 줄여서 부르겠다.
- [Elasticsearch란 - Minseop Jeong](https://velog.io/@msjeong97/Elasticsearch%EB%9E%80)
- [\[Elasticsearch\] 기본 개념잡기](https://victorydntmd.tistory.com/308)
- [\[Elasticsearch\] 입문하기(1) - Cluster( 클러스터 )](https://victorydntmd.tistory.com/311)
- [\[Elasticsearch\] 입문하기(2) - 기본 API( index, document CRUD )](https://victorydntmd.tistory.com/312)
- [\[Elasticsearch\] 입문하기(3) - 다양한 검색 방법 ( Search API )](https://victorydntmd.tistory.com/313)
- [\[Elasticsearch\] 대량 추가/조회 ( Bulk API, MultiSearch API )](https://victorydntmd.tistory.com/316)
- [Elasticsearch - status 바로 알기](https://brunch.co.kr/@alden/43)
### <br/><br/><br/>

## API
### ES는 API로 호출하여 사용한다는 것이 특징이다.
### 그래서 curl로 통신할 수 있다. 아래 명령어는 cluster에 대한 정보를 출력한다.
#### [\[Elasticsearch\] 입문하기(1) - Cluster( 클러스터 )](https://victorydntmd.tistory.com/311)
```
curl -XGET http://localhost:9200/_cluster/health?pretty=true
```
#### ![image](https://github.com/user-attachments/assets/6d9cf836-43e5-4b33-b021-6bfc1647f6a8)
### <br/>

### 이외에 status 체크 등등 모든 것들이 API를 통해 출력할 수 있다.
### update, delete, insert도 동일하고 각각 이용하기 위한 주소의 규칙이 있다(나머지는 블로그 글 참고).
#### [\[Elasticsearch\] 입문하기(2) - 기본 API( index, document CRUD )](https://victorydntmd.tistory.com/312)
### <br/><br/><br/>

## 클러스터 구성
#### [\[Elasticsearch\] 입문하기(1) - Cluster( 클러스터 )](https://victorydntmd.tistory.com/311)
#### ![image](https://github.com/user-attachments/assets/24d25a6e-03de-4898-9d62-1244d286e784)
### <br/><br/><br/>

## status
#### [Elasticsearch - status 바로 알기](https://brunch.co.kr/@alden/43)
#### ![image](https://github.com/user-attachments/assets/fe3a859c-2f9b-4009-af99-eb9b0449df3b)
