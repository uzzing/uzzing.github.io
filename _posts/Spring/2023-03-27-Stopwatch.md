---
title:  "[Development] StopWatch"
date: 2023-03-27 5:00PM
excerpt: "Dev"

author: Yuha
categories: [Development]
tags: [eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-03-27 5:00PM
---

# StopWatch
- allowing for timing of a number of tasks, exposing total running time and running time for each named task.

## Methods


```java

@Slf4j
public class ... {
StopWatch stopwatch = new StopWatch();

stopWatch.start();
// logic 1
stopWatch.stop();

log.info("stopwatch 1 : " + stopWatch.getTotalTimeSeconds());

stopWatch.start();
// logic 2
stopWatch.stop();
log.info("stopwatch 2 : " + stopWatch.getTotalTimeSeconds());

// Generate a string with a table describing all tasks performed.
log.info(stopWatch.prettyPrint());

}


```

<https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/util/StopWatch.html>

