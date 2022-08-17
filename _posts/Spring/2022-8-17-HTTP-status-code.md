---
title:  "[Development] HTTP Status Code"
date: 2022-8-17 3:00PM
excerpt: "Dev"

author: Yuha
categories: [Development]
tags: [eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2022-8-17 4:35PM
---

# Rules

![http-status-codes](https://user-images.githubusercontent.com/83699657/185044154-c0e0d6dc-2e53-4ad5-ad58-daad0be2b86a.png)


---
 
# Common HTTP Status Codes

|Status Code|Meaning|
|:---:|:---:|
| **200 OK** |the HTTP request was successfully carried out|
| **201 Created** |the PUT request was successfully carried out|
| **301 Moved Permanently** | the data requested from the client cannot be found <br> under the given address <br> since it has been moved permanently. |
|**302 Moved Temporarily**| the requested data has temporarily been moved. <br> the remaining information is specified so that an automatic redirection can take place. <br> The old address remains valid. |
|**401 Unauthorized**| when authentication is required <br> but has failed or not been provided. |
| **403 Forbidden** | the client that the requested data is access-protected<br> and that the request cannot be performed <br> due to the client not having authority.|
| **404 Not Found** | the requested website information was not found <br> on the server |
|**500 Internal Server Error**|-|
|**502 Bad Gateway**|something is wrong with your settings |


--- 

more info : <https://restfulapi.net/http-status-codes/>