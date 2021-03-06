# BareboneShop

# Task List Status
- [x] Server side web api that can be used to fetch products either one at a time or all at once
- [x] Every product should have a title, price, and inventory_count
- [x] Querying for all products should support passing an argument to only return products with available inventory
- [x] Products should be able to be "purchased" which should reduce the inventory by 1
- [x] Products with no inventory cannot be purchased.
- [x] Fit these product purchases into the context of a simple shopping cart
- [x] Creating a cart, adding products to the cart
- [x] Completing the cart
- [x] Cart should contain a list of all included products, a total dollar amount
- [x] Product inventory shouldn't reduce until after a cart has been completed
- [x] Secure API
- [x] Write documentation
- [x] Include unit tests
- [x] Building API using GraphQL

# Endpoints

| Endpoint        | Description           | Method Allowed  |
| :------------- |:-------------| :-----|
| /      | Return link to products & cart endpoints | GET |
| /products/      | Returns all products & Create new products | GET, POST |
| /products/{id}/      | Returns single product. id parameter will be 1,2,3..      |   GET |
| /products/avl/ | Returns all products with non zero inventory      |    GET |
| /products/{id}/purchase/ | Endpoint to purchase product. It will decrease the product's inventory by 1. Products with zero inventory will throw 404 error "Not found"     |    POST |
| /product/{id}/addcart/ | Endpoint to add product to Cart      |    POST |
| /cart/ | Returns Cart details. Contains products, quantity and total amount of cart      |    GET |
| /cart/checkout/ | Complete Cart purchase. Inventory of all products in cart will be reduced.      |    POST |

* Note:
  * POST request to endpoint `/product/id/addcart/` should contain the product data as follows:  
`{"product": "Amazon Echo","price": 29,"product_cnt": 1,"checked_out": false,"owner": 1}`  
See sample requests below.  
  * `/products/{id}/purchase/` Products with no inventory cannot be purchased. 404 Not Found response will be generated

# Sample Requests & Response
#### GET /products/
* Request  
<pre>
GET /products/ HTTP/1.1
Host: 127.0.0.1:8000
Connection: keep-alive
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.103 Safari/537.36
DNT: 1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
Cookie: csrftoken=VHcNRPaoYtUPQ8QliFJGJQZgBbV3vSGBPUEUpjitzd32T129nXqpEJgDFPV1LrVm; sessionid=3kieqota42sr0ujfxeegajgfk3asts6l;  tabstyle=html-tab
</pre>

* Response  
<pre>
{
  "count": 3,
  "next": null,
  "previous": null,
  "results": [
    {
      "id": 1,
      "title": "Iphone 6",
      "price": 350,
      "inventory_count": 17
    },
    {
      "id": 2,
      "title": "Amazon Echo",
      "price": 29,
      "inventory_count": 42
    },
    {
      "id": 3,
      "title": "Oneplus 6t",
      "price": 650,
      "inventory_count": 0
    }
  ]
}
</pre>

#### GET /products/avl/
* Request
<pre>
GET /products/avl.json HTTP/1.1
Host: 127.0.0.1:8000
Connection: keep-alive
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.103 Safari/537.36
DNT: 1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
Cookie: csrftoken=VHcNRPaoYtUPQ8QliFJGJQZgBbV3vSGBPUEUpjitzd32T129nXqpEJgDFPV1LrVm; sessionid=3kieqota42sr0ujfxeegajgfk3asts6l; tabstyle=html-tab
</pre>

* Response
<pre>
{
  "count": 2,
  "next": null,
  "previous": null,
  "results": [
    {
      "id": 1,
      "title": "Iphone 6",
      "price": 350,
      "inventory_count": 17
    },
    {
      "id": 2,
      "title": "Amazon Echo",
      "price": 29,
      "inventory_count": 42
    }
  ]
}
</pre>

#### GET /products/1/
* Request
<pre>
GET /products/1.json HTTP/1.1
Host: 127.0.0.1:8000
Connection: keep-alive
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.103 Safari/537.36
DNT: 1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
Cookie: csrftoken=VHcNRPaoYtUPQ8QliFJGJQZgBbV3vSGBPUEUpjitzd32T129nXqpEJgDFPV1LrVm; sessionid=3kieqota42sr0ujfxeegajgfk3asts6l; tabstyle=html-tab
</pre>

* Response
<pre>
{
  "id": 1,
  "title": "Iphone 6",
  "price": 350,
  "inventory_count": 17
}
</pre>

#### POST /products/1/purchase/
* Request
<pre>
POST /products/1/purchase/ HTTP/1.1
Host: 127.0.0.1:8000
Connection: keep-alive
Content-Length: 0
Origin: http://127.0.0.1:8000
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.103 Safari/537.36
Content-Type: application/json
Accept: text/html; q=1.0, */*
X-Requested-With: XMLHttpRequest
X-CSRFTOKEN: VHcNRPaoYtUPQ8QliFJGJQZgBbV3vSGBPUEUpjitzd32T129nXqpEJgDFPV1LrVm
DNT: 1
Referer: http://127.0.0.1:8000/products/1/purchase/
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
Cookie: csrftoken=VHcNRPaoYtUPQ8QliFJGJQZgBbV3vSGBPUEUpjitzd32T129nXqpEJgDFPV1LrVm; sessionid=3kieqota42sr0ujfxeegajgfk3asts6l; tabstyle=html-tab
</pre>
* Response
<pre>
HTTP 201 Created
Allow: POST, OPTIONS
Content-Type: application/json
Vary: Accept

{
    "success": true
}
</pre>

#### Endpoint /products/1/addcart/
* Request
<pre>
POST /products/2/addcart/ HTTP/1.1
Host: 127.0.0.1:8000
Connection: keep-alive
Content-Length: 87
Origin: http://127.0.0.1:8000
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.103 Safari/537.36
Content-Type: application/json
Accept: text/html; q=1.0, */*
X-Requested-With: XMLHttpRequest
X-CSRFTOKEN: VHcNRPaoYtUPQ8QliFJGJQZgBbV3vSGBPUEUpjitzd32T129nXqpEJgDFPV1LrVm
DNT: 1
Referer: http://127.0.0.1:8000/products/2/addcart/
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
Cookie: csrftoken=VHcNRPaoYtUPQ8QliFJGJQZgBbV3vSGBPUEUpjitzd32T129nXqpEJgDFPV1LrVm; sessionid=3kieqota42sr0ujfxeegajgfk3asts6l; tabstyle=html-tab
data: {"product": "Amazon Echo","price": 29,"product_cnt": 1,"checked_out": false,"owner": 1}
</pre>

* Response
<pre>
HTTP 200 OK
Allow: POST, OPTIONS
Content-Type: application/json
Vary: Accept

{
    "success": true
}
</pre>

#### GET /cart/
* Request
<pre>
GET /cart/ HTTP/1.1
Host: 127.0.0.1:8000
Connection: keep-alive
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.103 Safari/537.36
DNT: 1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
Cookie: csrftoken=VHcNRPaoYtUPQ8QliFJGJQZgBbV3vSGBPUEUpjitzd32T129nXqpEJgDFPV1LrVm; sessionid=3kieqota42sr0ujfxeegajgfk3asts6l; tabstyle=html-tab
</pre>

* Response
<pre>
{
  "Products": {
    "Amazon Echo": 1
  },
  "Total Amount": 29
}
</pre>

#### POST /cart/checkout/
* Request
<pre>
POST /cart/checkout/ HTTP/1.1
Host: 127.0.0.1:8000
Connection: keep-alive
Content-Length: 0
Origin: http://127.0.0.1:8000
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/51.0.2704.103 Safari/537.36
Content-Type: application/json
Accept: text/html; q=1.0, */*
X-Requested-With: XMLHttpRequest
X-CSRFTOKEN: VHcNRPaoYtUPQ8QliFJGJQZgBbV3vSGBPUEUpjitzd32T129nXqpEJgDFPV1LrVm
DNT: 1
Referer: http://127.0.0.1:8000/cart/checkout/
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
Cookie: csrftoken=VHcNRPaoYtUPQ8QliFJGJQZgBbV3vSGBPUEUpjitzd32T129nXqpEJgDFPV1LrVm; sessionid=3kieqota42sr0ujfxeegajgfk3asts6l; tabstyle=html-tab
</pre>

* Response
<pre>
HTTP 200 OK
Allow: POST, OPTIONS
Content-Type: application/json
Vary: Accept

{
    "Success": "Cart Checkout Successful"
}
</pre>

# GraphQL Requests
* Create new product
<pre>
mutation{
  createProduct(
    title: "Phillips iron",
    price: 20,
    inventoryCount: 5
  ){
    id
    title
    price
    inventoryCount
  }
}
</pre>

* Query all products
<pre>
query {
  products {
      id
      title
      price
      inventoryCount
  }
}
</pre>

* Get products with inventory count greater than 0
<pre>
query {
  products(avl:1){
      id
      title
      price
      inventoryCount
  }
}
</pre>

* Get individual products
<pre>
query {
  products(id:1){
      id
      title
      price
      inventoryCount
  }
}
</pre>

* Get the cart
<pre>
query {
  cart{
      products {
        product
        productCnt
        totalCost
      }
      cartAmount
  }
}
</pre>

* To purchase single product
<pre>
mutation{
  createPurchaseproduct(
    title: "Iphone 6",
    price: 350,
    inventoryCount: 1
  ){
    title
    price
    inventoryCount
    status
  }
}
</pre>

* Add to cart
<pre>
mutation{
  createAddcart(
    product: "Iphone 6",
    price: 350,
    productCnt: 1
  ){
    product
    price
    productCnt
    checkedOut
    status
  }
}
</pre>

* Checkout cart
<pre>
mutation{
  createCheckout(
    checkout: true
  ){
    status
  }
}
</pre>

# Requirements
* graphene-django = 2.2.0
* Django = 2.1.5
* Python = 3.7.2


# Configuring Barebone Django App
* Run `django-admin startproject Shop` to create new project
* Copy Barebone App to the new project directory
* Replace files in new Shop/ directory with this repos files in Shop/
* Run `python manage.py makemigrations Barebone`. To create migrations files from models
* Run `python manage.py migrate`. To execute migration file
* Run `python manage.py createsuperuser`. To create user
* Run `python manage.py runserver`

# Testing
* Test cases are written in `Barebones/test.py`. Execute `python manage.py test` for running test cases.

# Securing the end points
* Access Control: Only authenticated users are able to send POST requests.
* Restricted HTTP methods: As shown in the table above each function is restricted. All requests not matching the allowed methods rejects with HTTP response code 405 Method not allowed
* Input validations have been implemented
