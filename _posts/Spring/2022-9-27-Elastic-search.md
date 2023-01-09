---
title:  "[Development] Elasticsearch"
date: 2022-9-27 2:00PM
excerpt: "Dev"

author: Yuha
categories: [Development, Elasticsearch]
tags: [eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2022-10-4 2:00PM
---

# Architecture
# Elasticsearch Flow

<img width="702" alt="Screen Shot 2022-09-30 at 1 24 53 PM" src="https://user-images.githubusercontent.com/83699657/193190090-2ad586ae-a066-42f3-9e37-b43576a49264.png">

## Small-sized Solution
<img width="673" alt="Screen Shot 2022-09-30 at 6 13 52 PM" src="https://user-images.githubusercontent.com/83699657/193237119-def2c957-2cfd-4983-95e6-bd8483219464.png">
<img width="749" alt="Screen Shot 2022-09-30 at 6 14 01 PM" src="https://user-images.githubusercontent.com/83699657/193237124-f7749487-3d7b-4dd7-b161-77f59fcee4a8.png">

## ELK Stack

![architecture](https://user-images.githubusercontent.com/83699657/193196519-264b2d89-4787-40c6-8f66-3c8b1e2c3f93.jpeg)

<img width="709" alt="Screen Shot 2022-09-30 at 6 14 06 PM" src="https://user-images.githubusercontent.com/83699657/193240807-d3016bcb-53ae-42bc-b513-58d6f5af42a5.png">


## Elasticsearch / Lucene
- Lucene 
: Elasticsearch is an open-source search engine built **on top of Apache Lucene**, as the rest of the ELK Stack, including Logstash and Kibana.

![lucene](https://user-images.githubusercontent.com/83699657/193196279-7712492e-d858-48c3-bedf-0e6ca7e86038.png)

---

# Componenets

![es](https://user-images.githubusercontent.com/83699657/195297472-ca01c529-e7e4-48b5-bf42-bfc1b768ffdb.png)

![es2](https://user-images.githubusercontent.com/83699657/195297718-3f637691-6461-48b5-927f-22ceace4d3d2.png)



- Index
: An index consists of one or more Documents
  - Shard, Replicas 2개 유형으로 구분 가능

- Document
: Document consists of one or more Fields

- Cluster
: ES내 가장 큰 시스템 단위
  - 서로 다른 cluster는 데이터의 접근, 교환을 할 수 없는 독립적인 시스템
  - 여러 대의 server가 하나의 cluster를 구성 가능 / 한 서버에 여러 cluster가 존재할 수 있음
- Node
: ES를 구성하는 하나의 단위 프로세스 (데이터를 저장하고 indexing을 하는 등의 ES Instance)

- Shards 
: split up indices horizontally into pieces called shards
  - index를 여러 shard로 쪼갬 **for scaling out** in ES
  - Sharding : 데이터를 분산해서 저장하는 방법

- Replica
: One or More copy of index
  - 또 다른 형태의 shard
  - node를 손실했을 경우의 데이터의 신뢰성을 위해 shard를 복제
  - 권장사항 : replica는 서로 다른 노드에 존재할 것

---

# Inverted index

- Elasticsearch uses a data structure called an inverted index that supports **very fast full-text searches.** An inverted index lists **every unique word** that appears in any document and identifies **all of the documents each word occurs in.**
<img width="657" alt="Screen Shot 2022-10-04 at 2 10 50 PM" src="https://user-images.githubusercontent.com/83699657/193739395-5414e085-7e73-4013-914f-601cdb31ab6b.png">

---

# Example
<img width="816" alt="Screen Shot 2022-09-27 at 3 12 06 PM" src="https://user-images.githubusercontent.com/83699657/192446949-539f372c-c58a-4fcc-b888-a138fe4f3e65.png">

---

# Source Example

`Blog.java`
@Entity
- ES 7.0.0 부터는 Type 이 deprecated 되어 **indexName**만 설정가능

```java
@Setter
@Document(indexName = "blog")
public class Blog {

    @Id
    @Field(type = FieldType.Long)
    private String id;

    @Field(type = FieldType.Text)
    private String title;

    @Field(type = FieldType.Text)
    private String content;

    @Field(type = FieldType.Date)
    private Date log_date;

    @Field(type = FieldType.Text)
    private String log_text;

    @Field(type = FieldType.Long)
    private Long price;
}
```

`BlogEsRepository.java`
```java
@Repository
public interface BlogEsRepository extends ElasticsearchRepository<Blog, String> {
}
```

`BlogEsService.java`
```java
@Service
public class BlogEsService {

   @Autowired
   private ElasticsearchOperations operations;

   @Autowired
   private RestHighLevelClient client;


  public serviceMethod() {

    // BoolQueryBuilder
    // NativeSearchQueryBuilder
    // SearchHits
    // PageRequest
    // SearchRequest
    // SearchResponse
    // ...
    // Reference : Classes

  }

}
```

`Test`
```java
@Resource
BlogEsRepository blogEsRepository;

@Test
void test(){
    Blog blog = new Blog();
    blog.setId("1");
    blog.setContent("내용입니다.");
    blog.setTitle("제목입니다.");
    blogEsRepository.save(blog);
}
```

`bulid.gradle`
```java
dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-data-elasticsearch'
}
```

`application.yml`

```
elasticsearch:
  host: localhost
  port: 9200
```

---

# Classes
- SearchRequest
- SearchResponse
- SearchSourceBuilder
- SearchHits
- Document
  - @Document(indexName = "noresults_#{indexNames.getYMD()}", createIndex = false)
- RequestOptions
- NativeSearchQueryBuilder
- QueryBuilders
  - termsQuery
  - boolQuery
  - matchAllQuery
  - wildcardQuery
  - prefixQuery
- SortBuilders
  - fieldSort
- IndexQueryBuilder

- ElasticsearchOperations
  - search
  - getIndexCoordinatesFor
  - bulkUpdate
- RestHighLevelClient
- IndexCoordinates

---


[Reference]

<https://esbook.kimjmin.net/>

<https://bgpark.tistory.com/158>

<https://velog.io/@sunghwancode/TIL-%EA%B2%80%EC%83%89-%EC%8B%9C%EC%8A%A4%ED%85%9C-Elastic-Search-Redis>

SpringBoot ElasticSearch using Spring Data | Java Techie <https://www.youtube.com/watch?v=dlChXjE7IHw>

<https://yeminyi.github.io/myblog/elk/2020/10/22/what-is-elk.html>

<https://victorydntmd.tistory.com/308>

<https://idea-sketch.tistory.com/59>

<https://esbook.kimjmin.net/06-text-analysis/6.1-indexing-data>

<https://engineering.mercari.com/en/blog/entry/20220311-operational-tips-on-using-elasticsearch/>

<https://juntcom.tistory.com/137>