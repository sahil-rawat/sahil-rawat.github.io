---
title: HTTP 
date: 2021-07-14 16:04:00 +0530
categories: [BugBounty,Web]
tags: [web]
---
# Intro

This series will contain posts related to web application security \,ranging from how website works to various common vulnerabilities found in websites. This series will be helpful for begginers who are starting out in web application security or bugbounty.

Starrting out, This post in the series introduces basic concepts of HTTP Protocol.

# HTTP

Basically the protocol is a system of rules that defines how data is exchanged within or between computers.

![](./assets/img/http.png)

So The HTTP protocol allows us to fetch or send resources from or to the server, In Smple terms It is a pre defined set of rules that need to be followed while communicating with the server, for exapmle if we want to fetch data we need to initiate a GET request, and the format of this request is predefined which we need to follow while sending this request.

## What Happens When a request is made to a website?

As you enter a URL in the browser to open a website, An HTTP Request is made by the browser to fetch the Data from Server.

The HTTP request which the browser sent will look something like:

```http
GET /  HTTP/1.1 /
Host: https://sahilsinghrawat.in
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:50.0) Gecko/20100101 Firefox/50.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*,q=0.8
Authorization: Bearer Something_Here
Refferer: https://google.com/
```

Now Breaking apart the request line by line:

1. First Line determines What page (or endpoint) to fetch
2. Second line tells What website (or host) to fetch from
3. Third line is used by the server to determine information about the browser who is sending the request, It includes Browser Name, Version etc
4. Fourth line specifies What type of data to send/receive, for example text,json etc
5. Fifth line is used to specify authorisation for example if browser uses some kind of access control on the data then the user need to send a authorization token which specifies that the user is allowed to view the resource.
6. Sixth line tells the browser from where the user is redirected/reffered to

Now looking at the corresponding response from the server

```http
200 OK
Connection: Keep-Alive
Content-Encoding: gzip
Content-Type: text/html; charset=utf-8
Date: Mon, 13 Jul 2021 16:06:00 GMT
Keep-Alive: timeout=5, max=997
Server: Apache
Set-Cookie: mykey=myvalue; expires=Mon, 17-Jul-2017 16:06:00 GMT; Max-Age=31449600; 

```

Similarly Breaking down the response line by line:

1. First Line determines the response code, for ex success, redirect etc. More about this in next section
2. Second line tells browser to keep the connection alive for furthur more request.
3. Third line determines the encoding applied to the response data , this is usefull for browser so that browser could decode this data prior to rendering
4. Fourth line specifies the type of data which is recived, for example html.
5. Fifth line is date which is pretty self explanotry.
6. Sixth line hints the browser about how the connection may be used to set a timeout and a maximum amount of requests.
7. Seventh line is the server which is sending the response.
8. Eigth line sends the cookie from the server to the browser, to set a multiple cookie this header needs to be defined multiple times.

These are just some of the common headers associated with HTTP Requests and Responses, There are many more headers apart from it which are used depending on the underlying server.

Follow this guide to learn more about the [List of Headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)

## HTTP methods

The Request shown above was only one of the ways to interact with server from browser, below are the different types of http methods which could be used by the browser to interact with the server.

- **GET** - This is the request we discussed above, it is basically used to fetch resources/data from the server. This request should only be used to retrieve the data
- **HEAD** - This methods asks for response identical to the GET request, but without the response data, This is used to look at the response headers only.
- **POST** - This method is used to create or change data on the server for example creating a user on the server will result in sending a POST request.
- **PUT** - This is used to modify or replace the data on to the server, It replaces all current representation of the target with the request's payload
- **DELETE** - This method as the name suggests is used to delete a specified resource
- **TRACE** - This method does a message-loop back test, this is usually done for debuggin purposes, the response recived is the exact same request that the server recieved, this is done to check if the response headers are modified before reaching to the server (in case of an proxy).
- **OPTIONS** - This method is used simply to specify the communication methods available.

## HTTP response codes

Thses response codes are used by the server to hint the browser about the response, as we seen above in the HTTP response the first line consists of a code,

Some common HTTP response codes are ⬇️

- **200 range** -- Successful Range, This determines that the request was succesfully handeled by the server

* **300 range** -- Redirect, This hints browser to redirect to some other link
* **400 range** --
  * **401** - Unauthorised or unauthenticated
  * **403** - Forbidden or no access to resource
  * **404** - Not Found or File dosent Exist
  * **405**- HTTP Method not allowed
* **500 range** - Internal Server Error, Where the server dosent know how to handle the request
