# Microservices-Task

## Overview
This document provides details on testing various services after running the `docker-compose` file. These services include User, Product, Order, and Gateway Services. Each service has its own endpoints for testing purposes.

---

## Services and Endpoints

### **User Service**
- **Base URL:** `http://localhost:3000`
- **Endpoints:**
  - **List Users:**  
    ```
    curl http://localhost:3000/users
    ```
    Or open in your browser: [http://localhost:3000/users](http://localhost:3000/users)

---

### **Product Service**
- **Base URL:** `http://localhost:3001`
- **Endpoints:**
  - **List Products:**  
    ```
    curl http://localhost:3001/products
    ```
    Or open in your browser: [http://localhost:3001/products](http://localhost:3001/products)

---

### **Order Service**
- **Base URL:** `http://localhost:3002`
- **Endpoints:**
  - **List Orders:**  
    ```
    curl http://localhost:3002/orders
    ```
    Or open in your browser: [http://localhost:3002/orders](http://localhost:3002/orders)

---

### **Gateway Service**
- **Base URL:** `http://localhost:3003/api`
- **Endpoints:**
  - **Users:**  
    ```
    curl http://localhost:3003/api/users
    ```
  - **Products:**  
    ```
    curl http://localhost:3003/api/products
    ```
  - **Orders:**  
    ```
    curl http://localhost:3003/api/orders
    ```

---

## Instructions
1. Start all services using the `docker-compose` file:
   ```
   docker-compose up
   ```
2. Once the services are running, use the above endpoints to verify the functionality.

Happy testing! 

============================================= 


Microservices Testing 

================================ 


Steps:

Step 1: Clone the Repo

run: git clone the Url

<img width="578" height="157" alt="image" src="https://github.com/user-attachments/assets/8d5ac6c5-448a-4bda-826a-86119480c7dd" />


Step 2: Create in each services a file named: Dockerfile with the below code and Port numbers should be added for each service.
eg: EXPOSE 3000 for User Service

---------------------- 
Dockerfile:
--------------
FROM node:22-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE PORT_NUMBER
CMD ["npm", "start"] 

==========================


The actual routes are:

Service	                                      Internal port	Endpoint
------------------------------------------------------------------------
User Service	                                   3000	/users
Product Service	                                 3001	/products
Order Service	                                   3002	/orders
Gateway Service                                  3003	/health, /api/users, /api/products, /api/orders


============================== 

Step 3: Create a file under Microservices: docker-compose.yml 

Paste the below code:





