---
title:  "[Development] ElasticSearch - UpdateByQuery"
date: 2023-03-28 5:00PM
excerpt: "Dev"

author: Yuha
categories: [Development]
tags: [eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-03-28 5:00PM
---

# Update VS Reindex
- An update is a reindex of the original document, then marking that original as deleted, then having to merge it out of the segement. A reindex adds the original document to a new segment in a new index (usually), and leaves the original.

<https://discuss.elastic.co/t/update-vs-reindex/269929>

# UpdateByQuery
- Sync
- bulk

# UpdateByQueryAsync
- Asynchronous execution
    - Executing a UpdateByQueryRequest can also be done in an asynchronous fashion so that the client can return directly. Users need to specify how the response or potential failures will be handled by passing the request and a listener to the asynchronous update-by-query method:


# UpdateByQuery

- ctx._source 
    - map
    - ctx is a special variable that allows you to access the source of the object that you want to update. The ctx._source is a writable version of the source.
        - NOTE: You can modify this document in the script and the modified source will be persisted as the new version of the document.
        <https://stackoverflow.com/questions/37696380/elasticsearch-update-with-scripts-what-does-ctx-mean#:~:text=ctx%20is%20a%20special%20variable,new%20version%20of%20the%20document.>

- 작업 중간에 실패하더라도 이미 UPDATE된 내용은 롤백하지 않는다.
    - ES의 경우 오류가 발생하면 업데이트된 내용은 남겨둡니다. 이어서 작업을 즉시 중지하고 이후의 작업도 중지됩니다.
    - conflicts 옵션은 default 값은 ‘abort’ : 충돌이 발생시 그 상태에서 중지
    - conflicts ‘proceed’ : 충돌이 발생 시 멈추지 않고 변경하려는 내용으로 업데이트
    - <https://danawalab.github.io/elastic/2022/01/12/Update-By-Query-copy.html>






# boolQuery().filter() vs termsQuery()
- the only difference is "caching"
- filter is not cached by default
- the succeeding calls will be
faster since the first call will cache the result of the above filter.


- Filter query works much much faster as chunks with just terms query. But making really big filter can slower getting the result a lot. In my case, using filter query with chunks of 10 000 ids is 10 times faster, than using filter query with all 100 000 ids at once (btw, this number is already restricted in Elasticsearch 6).
    - <https://stackoverflow.com/questions/51464083/elasticsearch-filter-vs-term-query-for-many-ids>

- Generally, filters are executed in a "non-scoring" mode which gives them two main performance advantages. Firstly, they can omit the actual scoring of the document. Scoring a doc is relatively quick (the summation of a bunch of multiplications), but even 1ns for a billion documents is 1 second of computation.
- Secondly, non-scoring filters can be cached, meaning subsequent executions of the filter clause can leverage the cache instead of hitting the various data-structures.
- Where possible, we encourage people to convert queries => filters for better performance (assuming you don't need the scoring aspect)
    - <https://discuss.elastic.co/t/filter-performance-difference-bool-vs-terms/59928>


- for clarity and simplicity, we will use the term "filter" to mean a query which is used in a non-scoring, filtering context. You can think of the terms "filter", "filtering query" and "non-scoring query" as being identical.
- Similarly, if the term "query" is used in isolation without a qualifier, we are referring to a "scoring query".
    - <https://nag-9-s.gitbook.io/elastic-search-notes/query-dsl/query-and-filter-context/termquery-vs-termfilter>

# filter vs match
- term is designed for exact comparison while match is analyzed and used as full-text search.
    - <https://stackoverflow.com/questions/53053054/query-vs-filter-in-elastic-search>


# _search API

## if array
```java
GET /product/_search
{
  "query": {
      "nested" : {
        "path": "flags",
        "query": {
          "term": {
            "flags.flagCode": {
              "value": "dd"
            }
          }
        }
      }
    }
}
```

## if array
```java
GET /product/_search
{
  "query": {
      "nested" : {
        "path": "flags",
        "query": {
          "term": {
            "flags.flagCode": {
              "value": "dd"
            }
          }
        }
      }
    }
}
```

