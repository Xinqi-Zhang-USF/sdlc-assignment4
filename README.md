# sdlc-assignment4

## Running Application

  1. Ensure MySql and MongoDB instance is installed, configured and run.
  2. Create a new database in the MySQL instance with name “helloworlddb”:
  ```
  CREATE DATABASE helloworlddb
  ```
  3. Start Discovery Server Consul
  ```
  consul agent -data-dir=your-consul-data-file -dev -ui
  ```
  4. Run UsersService, RequestsService, and OffersService by run this command for each service:
  ```
  gradlew run
  ```
  5. Run Gateway :
  ```
  gradlew bootRun
 
  ```
  
  ![Running](https://github.com/Xinqi-Zhang-USF/sdlc-assignment4/blob/main/screenshot/Screen%20Shot%202021-02-23%20at%203.28.58%20AM.png)
  
  ## Try Services

### 1) Register John as user.
POST http://localhost:8080/uaa/signup/user
Content-Type: application/json

{"username":  "John", "password": "hello123"}


![Test](https://github.com/Xinqi-Zhang-USF/sdlc-assignment4/blob/main/screenshot/Screen%20Shot%202021-02-23%20at%203.38.08%20AM.png)

### 2) Register Mike as Service_provider.
POST http://localhost:8080/uaa/signup/service_provider
Content-Type: application/json

{"username":  "Mike", "password": "hello123"}

![Test](https://github.com/Xinqi-Zhang-USF/sdlc-assignment4/blob/main/screenshot/Screen%20Shot%202021-02-23%20at%203.38.54%20AM.png)

### 3) Login with John's credentials 
POST http://localhost:8080/login
Content-Type: application/json

{
  "username": "John",
  "password": "hello123"
}

![Test](https://github.com/Xinqi-Zhang-USF/sdlc-assignment4/blob/main/screenshot/Screen%20Shot%202021-02-23%20at%203.39.54%20AM.png)

### 4) Login with Mike Credentials. 
POST http://localhost:8080/login
Content-Type: application/json

{
  "username": "Mike",
  "password": "hello123"
}

![Test](https://github.com/Xinqi-Zhang-USF/sdlc-assignment4/blob/main/screenshot/Screen%20Shot%202021-02-23%20at%203.41.05%20AM.png)


### 5) Submit a Service Request. 
POST http://localhost:8080/requests/api/submit
Content-Type: application/json
Authorization: Bearer <token> # replace <token> with the token that you received in Step 3

{
     "type":"Maintenance",
     "title":"Maintenance",
     "detail":"A Full Maintenance for my apartement",
      "city":"MyCity"
}

![Test](https://github.com/Xinqi-Zhang-USF/sdlc-assignment4/blob/main/screenshot/Screen%20Shot%202021-02-23%20at%203.45.21%20AM.png)

### 6) Submit Offer
POST http://localhost:8080/offers/api/submit
Content-Type: application/json
Authorization: Bearer <token> # replace <token> with the token that you received in Step 4

{
   "requestNumber": "John_0", 
    "message": "I offer the full service for $1000",
    "price": 500
}

![Test](https://github.com/Xinqi-Zhang-USF/sdlc-assignment4/blob/main/screenshot/Screen%20Shot%202021-02-23%20at%203.47.37%20AM.png)

### 7) get the offers of a service request 
GET http://localhost:8080/offers/api/offers/John_0
Authorization: Bearer <token> # replace <token> with the token that you received in Step 3

![Test](https://github.com/Xinqi-Zhang-USF/sdlc-assignment4/blob/main/screenshot/Screen%20Shot%202021-02-23%20at%203.49.12%20AM.png)

### 8) Accept Offer
GET http://localhost:8080/requests/api/requests/accept/John_0/Mike_1
Authorization: Bearer <token> # replace <token> with the token that you received in Step 3

![Test](https://github.com/Xinqi-Zhang-USF/sdlc-assignment4/blob/main/screenshot/Screen%20Shot%202021-02-23%20at%203.49.35%20AM.png)

### 9) Reject Offer
GET http://localhost:8080/requests/api/requests/reject/John_0/Mike_3
Authorization: Bearer <token> # replace <token> with the token that you received in Step 3

![Test](https://github.com/Xinqi-Zhang-USF/sdlc-assignment4/blob/main/screenshot/Screen%20Shot%202021-02-23%20at%203.50.08%20AM.png)
  
