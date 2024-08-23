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
### <br/>

### API 관련
#### elasticsearch가 RESTful API는 아니다.
- 잘 정리 되어 있는 블로그
  - [\[Rest API\] RESTful하게 URL 설계하기](https://velog.io/@yoojkim/Rest-API-RESTful%ED%95%98%EA%B2%8C-URL-%EC%84%A4%EA%B3%84%ED%95%98%EA%B8%B0)
- 참고
  - [REST API - GET, POST,PUT,DELETE](https://velog.io/@dbsgywls9855/REST-API-GET-POST-PUT-DELETE)
  - [\[웹\] HTTP, URL 개념 정리 (REST API / GET, POST, PUT, DELETE )](https://hyunki99.tistory.com/38)
### <br/>

### 공식 문서
- [Common options](https://www.elastic.co/guide/en/elasticsearch/reference/current/common-options.html)
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
### <br/><br/>

### ES는 기본적으로 API를 사용하기 때문에, API 관련한 블로그를 참고해고 좋다(위 API 관련 블로그 링크 참고).
### 여기서 method에 따라 header, body가 있는 경우가 있고 없는 경우가 있는데, 각 method의 사용 가능한 형태를 참고하면 좋다.
- GET : path, parameter 사용 가능
- PUT : header, body 사용 가능(안 해도 됨). path, parameter 사용 가능. 리소스 갱신, 생성(갱신이 기본형태이고, 해당 리소스가 없으면 생성 => POST와의 차이점)
- POST : header, body 사용 가능(안 해도 됨). path, parameter 사용 가능
- DELETE : path, parameter 사용 가능
### <br/><br/><br/>


## 클러스터 구성
### ES에서 가장 큰 단위가 cluster이고, 그 하위로 node가 있다.
### node에는 여러 index로 구성된다.
### index는 primary shard, replica shard로 구성된다. 여기서 primary shard는 필수이고, replica는 없어도 조회는 가능하지만 성능 상 좋지 않다.
### shard는 index의 데이터가 분산되어 저장된 것이다.
### replica shard는 primary의 복제본이다. 
### 같은 node 안에 같은 것에서 기인한 primary, replica shard가 있는 건 불가능하다.
#### [\[Elasticsearch\] 입문하기(1) - Cluster( 클러스터 )](https://victorydntmd.tistory.com/311)
#### ![image](https://github.com/user-attachments/assets/24d25a6e-03de-4898-9d62-1244d286e784)
### <br/><br/><br/>


## status
### status가 red면 읽기 / 쓰기가 안 되지만, 한 index에서 조회하는 모든 것이 다 불가능한 건 아니다.
### index에 있는 primary shard가 5개인데, 그 중 2개가 unnasigned이면 그럼 40% 정도만 조회가 불가능할 것이다.
#### [Elasticsearch - status 바로 알기](https://brunch.co.kr/@alden/43)
#### ![image](https://github.com/user-attachments/assets/fe3a859c-2f9b-4009-af99-eb9b0449df3b)
### <br/><br/><br/>


## Index, type, document
####  [\[Elasticsearch\] 입문하기(2) - 기본 API( index, document CRUD )](https://victorydntmd.tistory.com/312)
### ES는 다양한 index 간에 같이 조회할 수 있다는 것이 특징이다. MySQL에서는 불가능. 하려면 SQL을 다양한 방식을 통해 작성해야 함(with을 쓴다던지...).
### 그리고 document를 조회를 하려면 반드시 색인화(id를 지정)해줘야 한다. 그래서 id를 지정해주지 않으면 default 값으로 특정 값이 들어간다.
### 아마 mongoDB, MySQL 등 다양한 형태의 db를 알고 있다면 익숙한 개념이다.
- Index : RDBMS의 database와 같은 범주
- type : RDBMS의 table과 같은 범주
- document : RDBMS의 row와 같은 범주
### <br/>

### API 호출에서 document에 대한 주소는 다음과 같이 path 하위 구분으로 나뉜다.
#### ![image](https://github.com/user-attachments/assets/c3958480-1663-4fe3-afd4-37310c162413)
### <br/>

### filter_path 여러개 쓰려면 다음과 같이 ','로 구분한다.
#### [Common options](https://www.elastic.co/guide/en/elasticsearch/reference/current/common-options.html)
#### ![image](https://github.com/user-attachments/assets/1aa1eab6-e8d5-4e7e-87cb-9f97f1026dd9)

