### 240822
# Elasticsearch
### 써야 할 건 아니고 공부 목적으로 관련 블로그들을 읽어보는 중이다. AWS에서도 종종 나왔기 때문에 어떤 기능이 있는지 궁금했다.
### elasticsearch의 가장 중요한 특징은 '검색 엔진'이라는 것이다. 그리고 물론 database의 성격을 가지고 있다.
### 여기서는 elasticsearch를 ES라고 줄여서 부르겠다.
- [Elasticsearch란 - Minseop Jeong](https://velog.io/@msjeong97/Elasticsearch%EB%9E%80)
- [\[Elasticsearch\] 기본 개념잡기](https://victorydntmd.tistory.com/308)
- [\[Elasticsearch\] 입문하기(1) - Cluster( 클러스터 )](https://victorydntmd.tistory.com/311)
- [\[Elasticsearch\] 입문하기(2) - 기본 API( index, document CRUD )](https://victorydntmd.tistory.com/312)
- [\[Elasticsearch\] 입문하기(3) - 다양한 검색 방법 ( Search API )](https://victorydntmd.tistory.com/313)
- [\[Elasticsearch\] 입문하기(4) - 다양한 검색 방법 ( Query DSL )](https://victorydntmd.tistory.com/314)
- [\[Elasticsearch\] 입문하기(5) - 검색 결과 가공하기](https://victorydntmd.tistory.com/315)
- [\[Elasticsearch\] 대량 추가/조회 ( Bulk API, MultiSearch API )](https://victorydntmd.tistory.com/316)
- [Elasticsearch - status 바로 알기](https://brunch.co.kr/@alden/43)
- [[Elastic Search] 기본 개념과 특징(장단점)](https://jaemunbro.medium.com/elastic-search-%EA%B8%B0%EC%B4%88-%EC%8A%A4%ED%84%B0%EB%94%94-ff01870094f0)
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
- [Query and filter context](https://www.elastic.co/guide/en/elasticsearch/reference/6.7/query-filter-context.html)
### <br/>

### 기타
### 검색 엔진에 대한 문제점 해결을 위해 ES를 사용한다고 한다.
- [ElasticSearch 1화: 왜 해야하고 무엇을 해야 하는가?](https://medium.com/elecle-bike/elasticsearch-1%ED%99%94-%EC%99%9C-%ED%95%B4%EC%95%BC%ED%95%98%EA%B3%A0-%EB%AC%B4%EC%97%87%EC%9D%84-%ED%95%B4%EC%95%BC-%ED%95%98%EB%8A%94%EA%B0%80-47a21f25508c)
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
### <br/><br/><br/>

## query DSL, query and filter context
### query를 할 때의 성격은 2개로 나뉜다.
#### [Query and filter context](https://www.elastic.co/guide/en/elasticsearch/reference/6.7/query-filter-context.html)
- query context : 얼마나 잘 매치가 되었는지 판단하는 score 값이 계산되는 항목이다.
- filter context : term, range clause와 같은 것이 filter context에 속한다. score 값 계산에 포함하지 않는다. 사용 방법은 mongoDB와 같이 gte, gt, lte, lt와 같이 쓴다.
#### ![image](https://github.com/user-attachments/assets/3cc12390-2848-498e-89bc-838d811190ba)
#### ![image](https://github.com/user-attachments/assets/29a93872-b17b-4f45-b983-ddf3730effa2)
#### ![image](https://github.com/user-attachments/assets/0e2f6903-5d48-48ef-b1ec-dc71606cd375)
### <br/>

### bool
- must : bool must 절에 지정된 모든 쿼리가 일치하는 document를 조회
- should : bool should 절에 지정된 모든 쿼리 중 하나라도 일치하는 document를 조회
- must_not : bool must_not 절에 지정된 모든 쿼리가 모두 일치하지 않는 document를 조회
- filter : must와 같이 filter 절에 지정된 모든 쿼리가 일치하는 document를 조회하지만, Filter context에서 실행되기 때문에 score를 무시합니다.
### <br/>

### filter
### 위에서 설명
### <br/>

### range
- gte : 크거나 같다.
- gt : 크다.
- lte : 작거나 같다.
- lt : 작다.
- boost : 쿼리의 boost 값을 셋팅합니다( 기본 값 1.0 ). 같은 쿼리가 있을 때에 중요도를 더 가산하여 검색하는 항목이다. score 값에는 normalization이 들어가기 때문에 크게 반영되지 않는다. [ex](https://stackoverflow.com/questions/21570963/boosting-in-elasticsearch)
### <br/>

### term
### 키워드를 조회하는 방법이다.
### 예를 들어 "Quick Foxes" 라는 문자열이 있을 때 text 타입은 \[quick, foxes\]으로 각각의 단어를 조회할 수 있다.
### 주의할 점은 "Quick Foxes"라고 검색할 수 없다. 각각의 단어로 검색해야 한다.
```
{
  "query": {
    "terms": {
      "address": ["street", "place", "avenue"]
    }
  }
}
```
### <br/>

### regexp 
### 정규 표현식 사용
```
{
    "query": {
        "regexp":{
            "address": ".*street"
        }
    }
}
```
### <br/><br/><br/>
