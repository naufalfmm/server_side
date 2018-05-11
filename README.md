Congestion Detection System (API Side)
===========================
**This is the repository of API Side.**

Congestion Detection System is *Internet of Things* based system for detect and rank the congestion severity of the road. Ranking the congestion severity is based on *Indonesian Highway Capacity Manual* published by Ministry of Public Works Republic of Indonesia in 2014. The rank of severity range between A to F as the result of saturation degree calculation of the road. The project is a undergraduate last project owned by [Naufal Farras][1] in [Departement Computer Science][2], [Faculty Mathematics and Natural Sciences][3], [Bogor Agricultural University][3]. The project is also presented in Seminar Ilmiah Ilmu Komputer 2018.

# Requirements
The API Side of system requires NodeJS >= 8.5.0 and MySQL as DBMS. If you want to test or run the API Side without the node, you have to install API tester, such as Postman, etc.

# Installation
#### 1. Install NodeJS
> **Note:**
> Before you install, please check first by run a command
> ```
> node --version
> ```
> If the version of node >=8.5.0, you can **skip** this step.

1. If you are Windows user, please download [here][3]. Choose the right Windows version (32/64 bit) based on your computer. Please check [here][4] to get the version of Windows.
2. If you're Ubuntu user, run command

    ```
    curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
    sudo apt-get install -y nodejs
    ```
3. For another OS, you can check [here][5].

#### 2. Clone The Project
> **Note:**
> You must install [**git command**][6] first before do the step.

You can store the project file wherever you want. Clone the project by run a command
```
git clone https://gitlab.com/naufalfmm/server_side.git
```
Before you clone the project, you have to be in the directory you want to store the project file.

#### 3. Install The Dependencies
> **Note:**
> You have to be in the directory of the project file stored.

Install the dependecies by run a command
```
npm install
```
If you use yarn, please run command below.
```
yarn
```

#### 4. Run The App!
The application is ready to serve on 7777. Please type and run command below to start the application
```
node app.js
```
or
```
npm start
```

# API Documentation
## **Admin**
---
### **Admin Login**
  Login for admin role. Returns token for "auth" header using JWT.
  ```
  POST /api/admin/login
  ```
#### Request Body:
  ```json
  {
      "username":"",
      "password":""
  }
  ```
#### **Success Response:**
* **Code:** 200 <br />
  **Content:** 
  ```json
  {"status": true, "token": "", "message": "Happy Login"}
  ```
#### **Error Responses:**
* **Code:** 500 Internal Server Error <br />
  **Content:** 
   ```json
   {"status": false, "message": "Internal Server Error"}
   ```
* **Code:** 401 Unauthorized <br />
  **Content:** 
  ```json
  {"status": false, "message": "Unauthorized"}
  ```
---
## **Node**
---
### **Node Login**
  Login for node role. Returns token for "auth" header using JWT.
  ```
  `POST` /api/device/login
  ```
#### **Request Body:**
  ```json
  {
      "username":"",
  }
  ```
#### **Success Response:**
* **Code:** 200 <br />
  **Content:** 
  ```json
  {"status": true, "token": "", "message": "Happy Login"}
  ```
#### **Error Responses:**
* **Code:** 500 Internal Server Error <br />
  **Content:** 
  ```json
  {"status": false, "message": "Internal Server Error"}
  ```
* **Code:** 401 Unauthorized <br />
  **Content:** 
  ```json
  {"status": false, "message": "Unauthorized"}
  ```
### **Add/Register Node**
  Register new node for a lane. Each lane is just for one node. Node **only** can be registered by Admin.
  ```
  POST /api/device/add/{laneId}
  ```
#### Path Parameters
| Parameter name | Value   | Description | Additional |
| -------------- | ------- | ----------- | ---------- |
| laneId         | integer | Lane id     | Required   |

#### **Success Response:**
* **Code:** 201 <br />
  **Content:** 
  ```json
  {"status": true,  "message": "Device Successfully Created"}
  ```
#### **Error Responses:**
* **Code:** 400 Bad Request <br />
  **Content:** 
  ```json
  {"status": false, "message": "Data Incomplete"}
  ```
* **Code:** 401 Unauthorized <br />
  **Content:** 
  ```json
  {"status": false, "message": "Unauthorized"}
  ```
* **Code:** 409 Conflict <br />
  **Content:** 
  ```json
  {"status": false, "message": "Unique Constraint Error"}
  ```
  or
  ```json
  {"status": false, "message": "Lane Id Error"}
  ```
* **Code:** 500 Internal Server Error <br />
  **Content:** 
  ```json
  {"status": false, "message": "Internal Server Error"}
  ```
### **Delete Node**
  Delete node registered by admin.
  ```
  DELETE /api/device/delete/{deviceId}
  ```
#### Path Parameters
| Parameter name | Value   | Description | Additional |
| -------------- | ------- | ----------- | ---------- |
| deviceId       | integer | Device id   | Required   |

#### **Success Response:**
* **Code:** 200 <br />
  **Content:** 
  ```json
  {"status": true,  "message": "Device is Successfully Deleted"}
  ```
#### **Error Responses:**
* **Code:** 400 Bad Request <br />
  **Content:** 
  ```json
  {"status": false, "message": "Data Incomplete"}
  ```
* **Code:** 401 Unauthorized <br />
  **Content:** 
  ```json
  {"status": false, "message": "Unauthorized"}
  ```
* **Code:** 403 Forbidden <br />
  **Content:** 
  ```json
  {"status": false, "message": "Device Doesn't Exist"}
  ```
* **Code:** 500 Internal Server Error <br />
  **Content:** 
  ```json
  {"status": false, "message": "Internal Server Error"}
  ```
### **Create Node Config**
  Create config file of node.
  ```
  POST /api/device/create/{deviceId}
  ```
#### Path Parameters
| Parameter name | Value   | Description | Additional |
| -------------- | ------- | ----------- | ---------- |
| deviceId       | integer | Device id   | Required   |

#### **Success Response:**
* **Code:** 201 <br />
  **Content:** 
  ```json
  {"status": true,  "message": "Config File Created Successfully"}
  ```
#### **Error Responses:**
* **Code:** 400 Bad Request <br />
  **Content:** 
  ```json
  {"status": false, "message": "Data Incomplete"}
  ```
* **Code:** 401 Unauthorized <br />
  **Content:** 
  ```json
  {"status": false, "message": "Unauthorized"}
  ```
* **Code:** 403 Forbidden <br />
  **Content:** 
  ```json
  {"status": false, "message": "Device Doesn't Exist"}
  ```
* **Code:** 404 Not Found <br />
  **Content:** 
  ```json
  {"status": false, "message": "Device Not Found"}
  ```
* **Code:** 500 Internal Server Error <br />
  **Content:** 
  ```json
  {"status": false, "message": "Internal Server Error"}
  ```
### **Download Node Config File**
  Download node config file created by server.
  ```
  GET /api/device/download/{deviceId}
  ```
#### Path Parameters
| Parameter name | Value   | Description | Additional |
| -------------- | ------- | ----------- | ---------- |
| deviceId       | integer | Device id   | Required   |

#### **Success Response:**
* **Code:** 200 <br />
#### **Error Responses:**
* **Code:** 400 Bad Request <br />
  **Content:** 
  ```json
  {"status": false, "message": "Data Incomplete"}
  ```
* **Code:** 401 Unauthorized <br />
  **Content:** 
  ```json
  {"status": false, "message": "Unauthorized"}
  ```
* **Code:** 403 Forbidden <br />
  **Content:** 
  ```json
  {"status": false, "message": "Device Doesn't Exist"}
  ```
* **Code:** 404 Not Found <br />
  **Content:** 
  ```json
  {"status": false, "message": "File Not Found"}
  ```
* **Code:** 500 Internal Server Error <br />
  **Content:** 
  ```json
  {"status": false, "message": "Internal Server Error"}
  ```
---
## **Road**
---
### **Add Road**
  Add new road to *database*.
  ```
  `POST` /api/road/add
  ```
#### **Request Body:**
  ```json
  {
      "name":"",
      "lanes":,
      "paths":
  }
  ```
#### **Success Response:**
* **Code:** 201 <br />
  **Content:** 
  ```json
  {"status": true, "message": "Road Successfully Added"}
  ```
#### **Error Responses:**
* **Code:** 400 Bad Request <br />
  **Content:** 
  ```json
  {"status": false, "message": "Data Incomplete"}
  ```
* **Code:** 401 Unauthorized <br />
  **Content:** 
  ```json
  {"status": false, "message": "Unauthorized"}
  ```
* **Code:** 500 Internal Server Error <br />
  **Content:** 
  ```json
  {"status": false, "message": "Internal Server Error"}
  ```
---
## **Lane**
---
### **Add Lane**
  Add new lane of road to *database*.
  ```
  `POST` /api/lane/add
  ```
#### **Request Body:**
  ```json
  {
    "th":,
    "width":,
    "cap":,
    "path":,
    "road_id":
}
  ```
#### **Success Response:**
* **Code:** 201 <br />
  **Content:** 
  ```json
  {"status": true, "message": "Lane Successfully Added"}
  ```
#### **Error Responses:**
* **Code:** 400 Bad Request <br />
  **Content:** 
  ```json
  {"status": false, "message": "Data Incomplete"}
  ```
  or
  ```json
  {"status": false, "message": "Bad Request"}
  ```
* **Code:** 401 Unauthorized <br />
  **Content:** 
  ```json
  {"status": false, "message": "Unauthorized"}
  ```
* **Code:** 500 Internal Server Error <br />
  **Content:** 
  ```json
  {"status": false, "message": "Internal Server Error"}
  ```
---
## **Traffic Data**
---
### **Post traffic data**
  Post traffic data to the *database*.
  ```
  `POST` /api/data/post
  ```
#### **Request Body:**
  ```json
  {
    "data": "encrypted_data"
  }
  ```
#### **Success Response:**
* **Code:** 201 <br />
  **Content:** 
  ```json
  {"status": true, "message": "Data is Successfully Added"}
  ```
#### **Error Responses:**
* **Code:** 400 Bad Request <br />
  **Content:** 
  ```json
  {"status": false, "message": "Data Incomplete"}
  ```
  or
  ```json
  {"status": false, "message": "Bad Request"}
  ```
* **Code:** 401 Unauthorized <br />
  **Content:** 
  ```json
  {"status": false, "message": "Unauthorized"}
  ```
* **Code:** 403 Forbidden <br />
  **Content:** 
  ```json
  {"status": false, "message": "Device Doesn't Exist"}
  ```
* **Code:** 500 Internal Server Error <br />
  **Content:** 
  ```json
  {"status": false, "message": "Internal Server Error"}
  ```

[1]: https://gitlab.com/naufalfmm
[2]: https://cs.ipb.ac.id
[3]: https://fmipa.ipb.ac.id
[4]: https://ipb.ac.id
[5]: https://nodejs.org/en/download/package-manager/
[6]: https://git-scm.com/downloads
