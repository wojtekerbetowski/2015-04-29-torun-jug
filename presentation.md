# Designing mobile API

## Wojtek Erbetowski
### MobileWarsaw #21, 19.01.2015
### t: @erbetowski

---
# About me?

## You all know me already, right?

---
## Why not simply 'design an API'?

---
## Good mobile API
## ≠
## Good API

---
![fit](http://wojtekerbetowski.github.io/geecon-mobile-api-presentation/img/sir.jpg)

---
# REST & HATEOAS

---
`GET /users/123`

```json
{
  "name": "John Doe",
  "age": 25,
  "links": [
    {
      "rel": "self",
      "href": "/users/123"
    },
    {
      "rel": "account",
      "href": "/accounts/987"
    },
    {
      "rel": "address",
      "href": "/addresses/555"
    }
  ]
}
```

---
`GET /addresses/555`

```json
{
  "street": "Sesame",
  "no": 25,
  "zipCode": "12-321",
  "state": "NY",
  "country": "US"
}
```

---

# HATEOAS is great!

---
## there's a thing called latency

---
Latency 

![fit](http://placehold.it/350x150/fff&text=%20)

![inline](http://wojtekerbetowski.github.io/geecon-mobile-api-presentation/img/GeeCON_latency.png)

---
Latency 

![fit](http://placehold.it/350x150/fff&text=%20)

![inline](https://www.dropbox.com/s/dlju52udord1to2/Screenshot%202015-01-19%2014.04.06.png?dl=1)

---
# It can get crazy

---
# Merging responses

---
`GET /user/123`

```json
{
  "name": "John Doe",
  "age": 25,
  "country": "US"
}
```

---
## And if it ain't yours?

---
# Expansion FTW!

---
`GET /users/123?fields=[name,age,address[country]]`

```json
{
  "name": "John Doe",
  "age": 25,
  "country": "US"
}
```

---
## but most of all

---
`CONNECTION: KEEP-ALIVE`

---
# Docs

---
![fit](http://wojtekerbetowski.github.io/geecon-mobile-api-presentation/img/swagger.png)

---
# THROUGHPUT

---
![fit](http://wojtekerbetowski.github.io/geecon-mobile-api-presentation/img/GeeCON_map.png)

---
## Do you get only what you need?

---
```json
{
  "person": {
    "id": 12345,
    "firstName": "John",
    "lastName": "Doe",
    "age": 25,
    "phones": {
      "home": "800-123-4567",
      "work": "888-555-0000",
      "cell": "877-123-1234"
    },
    "email": [
      "jd@example.com",
      "jd@example.org"
    ],
    "dateOfBirth": "1980-01-02T00:00:00.000Z",
    "registered": true,
    "emergencyContacts": [
      {
        "name": "",
        "phone": "",
        "email": "",
        "relationship": "spouse|parent|child|other"
      }
    ],
    "address": {
        "street": "Sesame",
        "no": 25,
        "zipCode": "12-321",
        "state": "NY",
        "country": "US"
    }
  }
}
```

---
```json
{
    "firstName": "John",
    "lastName": "Doe",
    "age": 25,
    "country": "US"
}
```

---
## And if it ain't yours?

---
# Expansion FTW!

---
`GET /users/123?fields=[name,age,address[country]]`

```json
{
  "name": "John Doe",
  "age": 25,
  "country": "US"
}
```

---
# DATA COMPRESSION

---
```json
{
"people": [
    {
        "firstName": "Jason",
        "lastName": "Page",
        "username": "jasonp",
        "isMale": true,
        "phone": "142-808-3743",
        "nid": "12252671714"
 ...
 ```

 ---
## Full
222910 bytes

## GZipped
32128 bytes (14%)

---
# Domain complexity

---
## Usually automated testing sucks
## (on mobile)

---
## So if UI differs from 
##DATA MODEL

---
## ... let the backend guys worry

---
`POST /relation`

```json
{
  "type": "follower",
  "from": 123,
  "to": 456
}
```

---
`POST /follow/456`

---
# HTTP Cache

---
`Expires: Sat, 21 Feb 2015 05:00 GMT`

## iOS (AFNetworking + NSURLCache)
## Android (Retrofit + OkHttp + HttpResponseCache)

---
`GET /users?page=1`

```json
[
  "Arthur",
  "Bob",
  "Celine",
  "Daniel",
  "Eve",
  "Fred",
  "George"
]
```

---
`GET /users?since=185328145127`

---
```json
{
    "items": [
        ...
    ],
    "next": "/users?since=185328145127"
}
```

---
# Case study

---
# Endpoints overall

## from 36 to 20

---
# Endpoints usage
## (full application flow)

## from 86 to 20

---
## 96% data size reduction 
## (84% without GZIP)

---
# In the end 
# it's all about usability

---
# Starring

---
# Akamai
## State of the Internet
### http://www.akamai.com/stateoftheinternet/

---
# Swagger
### http://swagger.io/

---
# Applause
## (Former uTest)
#### https://itunes.apple.com/us/app/utest/id411486493

---
# Any thoughts?
