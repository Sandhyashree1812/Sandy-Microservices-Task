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


Microservices Testing Assignment

================================ 


Steps:

Step 1: Clone the Repo

run: git clone the Url

run: git clone https://github.com/Sandhyashree1812/Sandy-Microservices-Task.git

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
CMD ["node", "app.js"]

==========================
note: each service uses its own port

The actual routes/ports are:

Service	                                      Internal port	Endpoint
------------------------------------------------------------------------
User Service	                                   3000	/users
Product Service	                                 3001	/products
Order Service	                                   3002	/orders
Gateway Service                                  3003	/health, /api/users, /api/products, /api/orders


============================== 

Step 3: Create a file under Microservices: docker-compose.yml 

Paste the below code:

services:
  user-service:
    build: ./user-service
    ports:
      - "3000:3000"
    networks:
      - microservices-network

  product-service:
    build: ./product-service
    ports:
      - "3001:3001"
    networks:
      - microservices-network

  order-service:
    build: ./order-service
    ports:
      - "3002:3002"
    networks:
      - microservices-network

  gateway-service:
    build: ./gateway-service
    ports:
      - "3003:3003"
    depends_on:
      - user-service
      - product-service
      - order-service
    networks:
      - microservices-network

networks:
  microservices-network:
    driver: bridge
---------------------------- 

Step 4: Build and start the application

Run: docker --version

<img width="404" height="29" alt="image" src="https://github.com/user-attachments/assets/e7ced0de-9435-432c-96a3-1a67e47c78d3" />


Run: docker compose config

<img width="638" height="363" alt="image" src="https://github.com/user-attachments/assets/2eebfc69-6603-4913-837b-04b50380449d" />

Run: docker compose up --build -d 


<img width="622" height="313" alt="image" src="https://github.com/user-attachments/assets/32d675c0-4476-4b46-8a0d-b29b35e21d9b" />


<img width="639" height="173" alt="image" src="https://github.com/user-attachments/assets/ff2da45d-bc00-4b0f-a4e8-121b08e1fc88" />


Run: docker compose ps


<img width="627" height="161" alt="image" src="https://github.com/user-attachments/assets/e29aec2f-2280-4dee-9279-b204ba6bdc84" />



Step 5: Test the Gateway 

in browser: open http://localhost:3003/health


<img width="302" height="114" alt="image" src="https://github.com/user-attachments/assets/ba406ee0-63d1-4761-b06c-d47d80fc8be6" />


Open: http://localhost:3003/api/users

<img width="403" height="143" alt="image" src="https://github.com/user-attachments/assets/874d13a7-9b94-4ad9-a57b-535d85a99e55" />


Open http://localhost:3003/api/products


<img width="559" height="188" alt="image" src="https://github.com/user-attachments/assets/3975c83c-eb24-4288-8901-d958287a87e1" />

Run:
Invoke-RestMethod http://localhost:3003/health
Invoke-RestMethod http://localhost:3003/api/users
Invoke-RestMethod http://localhost:3003/api/products




<img width="635" height="284" alt="image" src="https://github.com/user-attachments/assets/799b0808-5136-42c7-891b-9e2285d10498" />


Run: Invoke-RestMethod http://localhost:3003/api/orders
This gives an empty list.

Let's create a Test order.

Step 6: Create a test order

--------------------------- 

Run: 
$body = @{
    userId = 1
    productId = 1
} | ConvertTo-Json

Invoke-RestMethod `
    -Uri http://localhost:3003/api/orders `
    -Method Post `
    -ContentType "application/json" `
    -Body $body

---------------------------------------- 


<img width="642" height="191" alt="image" src="https://github.com/user-attachments/assets/675323ae-c4ab-4da0-91d9-3c025cbacd46" />


Step 7: Retrieve the orders: 

Run:  Invoke-RestMethod http://localhost:3003/api/orders 


<img width="629" height="93" alt="image" src="https://github.com/user-attachments/assets/94f4f5fe-d45d-4a4c-9dbc-faefc6cf30aa" />


Step 8: Verify all four containers

Run:  docker compose ps

<img width="635" height="161" alt="image" src="https://github.com/user-attachments/assets/6b357621-de63-4806-b4e5-1ad92459ff60" />

Step 9: Update and push your GitHub repository

Run:
git status

<img width="551" height="211" alt="image" src="https://github.com/user-attachments/assets/8f29b11d-2bcd-4423-958c-704e6de3ced9" />



Run: git add .
Run: git commit -m "Containerize microservices using Docker Compose"


<img width="645" height="209" alt="image" src="https://github.com/user-attachments/assets/da94cac6-fd5d-4162-b288-4e349a2cc521" />


Run: git push origin main

<img width="492" height="149" alt="image" src="https://github.com/user-attachments/assets/d3c62cae-1f04-4625-aaf2-3b9351de3d57" />



Run: git status

<img width="414" height="80" alt="image" src="https://github.com/user-attachments/assets/6cb19fd1-bf25-4f52-84b7-5847ac529d73" />
