# store_items-api
items api for store in golang

use sqlmock to mock the sql driver
use https://github.com/olivere/elastic/wiki

run elasticsearch in the cmd.

##### To build docker image
docker build -t items-api .

##### To run docker image (host ports, elastic search ports, and the container name)
docker run -p 8081:8081 -p 9200:9200 items-api:latest

###### create items index 
curl --location --request PUT '127.0.0.1:9200/items' \
--header 'Content-Type: application/json' \
--data-raw '{
	"settings":{
		"number_of_shards":4,
		"number_of_replicas":2
	}
}'

###### Get items index
curl --location --request GET '127.0.0.1:9200/items'

###### Search items directly in elasticsearch
curl --location --request GET '127.0.0.1:9200/items/_search'
You can use POST

###### Save item
curl --location --request POST 'localhost:8080/items' \
--header 'Content-Type: application/json' \
--data-raw '{
    "title": "Mac book pro",
    "description": {
        "plain_text": "Mac book pro"
    },
    "status": "pending",
    "available_quantity": 10
}'

###### Example of the elastic custom query

###### AnyEquals applies an or statement

{
    "equals": [
        {
            "field": "status",
            "value": "pending"
        },
        {
            "field": "seller",
            "value": "1"
        }
    ],
    "any_equals": [
        {
            "field": "status",
            "value": "pending"
        },
        {
            "field": "seller",
            "value": "1"
        }
    ]
}

###### items search
curl --location --request GET 'localhost:8081/items/search' \
--header 'Content-Type: text/plain' \
--data-raw '{
    "equals": [
        {
            "field": "seller",
            "value": 1
        },
           {
            "field": "status",
            "value": "pending"
        }
    ]
}'
