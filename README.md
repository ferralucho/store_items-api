# store_items-api
itemms api for store in golang

use sqlmock to mock the sql driver
use https://github.com/olivere/elastic/wiki

run elasticsearch in the cmd.


//create items index 
curl --location --request PUT '127.0.0.1:9200/items' \
--header 'Content-Type: application/json' \
--data-raw '{
	"settings":{
		"number_of_shards":4,
		"number_of_replicas":2
	}
}'

//Get items index
curl --location --request GET '127.0.0.1:9200/items'

//Search items
curl --location --request GET '127.0.0.1:9200/items/_search'
You can use POST

//Save item
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

