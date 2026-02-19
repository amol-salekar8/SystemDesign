# API Gateway
## Content
1) [Q. Why Do We Need an API Gateway?](#why-do-we-need-an-api-gateway)
2) [Without an API Gateway:](#without-an-api-gateway)
3) [With an API Gateway:](#with-an-api-gateway)
4) [Core Features of an API Gateway](#Core Features of an API Gateway)
   1) [ Authentication and Authorization](#1-authentication-and-authorization)
   2) [ Rate Limiting](#2-rate-limiting)
   3) [ Load Balancing](#3-load-balancing)
   4) [ Caching](#4-caching)
   5) [ Request Transformation](#5-request-transformation)
   6) [ Service Discovery](#6-service-discovery)
   7) [ Circuit Breaking](#7-circuit-breaking)
   8) [ Logging and Monitoring](#8-logging-and-monitoring)
5) [How Does an API Gateway Work?](#how-does-an-api-gateway-work)

### Why Do We Need an API Gateway?
 Modern applications, especially those built using microservices architecture, **have multiple backend services managing different functionalities**.

**For example, in an e-commerce service:**
1) One service handles user accounts.
2) Another handles payments.
3) Another manages product inventory. 
### Without an API Gateway:

![](image/withoutAPIGateway.png)

1) Clients would need to know the location and details of all backend services. 
2) Developers would need to manage authentication, rate limiting, and security for each service individually.

### With an API Gateway:

![](image/withAPIGateway.png)

1) Clients send all requests to one place – the API Gateway. 
2) The API Gateway takes care of **routing, authentication, security, and other operational tasks, simplifying both client interactions and backend management**.

### Core Features of an API Gateway

![](image/basicUseAPIGateway.png)

#### 1. Authentication and Authorization
API Gateway secures the backend systems by ensuring only authorized users and clients can access backend services.

It handles tasks like:
1) **Authentication :** Verifying the identity of the client using tokens (e.g., OAuth, JWT), API keys, or certificates. 
2) **Authorization :** Checking the client’s permissions to access specific services or resources.

By centralizing these tasks, the **API gateway eliminates the need for individual services to handle authentication,** reducing redundancy and ensuring consistent access control across the system.

#### 2. Rate Limiting
1) **To prevent abuse and ensure fair usage of resources**, most API Gateways implement rate limiting.
2) **This feature:**
    - **Controls the frequency of requests** a client can make within a given timeframe.
    - **Protects backend services from being overwhelmed by excessive traffic** or potential denial-of-service (DoS) attacks.
3) **Example :**
   - a public API might allow a maximum of 100 requests per minute per user. 
   - If a client exceeds this limit, the API Gateway will block additional requests until the rate resets.

#### 3. Load Balancing
1) High-traffic applications rely on load balancing to distribute incoming requests evenly across multiple instances of a service.
2) The API Gateway can:
   - Redirect requests to healthy service instances while avoiding ones that are down or overloaded.
   - Use algorithms like round-robin, least connections, or weighted distribution to manage traffic intelligently.

#### 4. Caching
1) To improve **response times and reduce the strain on backend services**, most API Gateways provide caching.
2) They temporarily store frequently requested data, such as:
    - Responses to commonly accessed endpoints (e.g., product catalogs or weather data).
    - Static resources like images or metadata.
3) **NOTE** Caching helps in **reducing latency and enhancing user experience** while lowering the operational cost of backend services.

#### 5. Request Transformation
1) In systems with **diverse clients and backend services, request transformation is essential for compatibility.**
2) An API Gateway can:
   - Modify the structure or format of incoming requests to match the backend service requirements.
   - Transform responses before sending them back to the client, ensuring they meet the client’s expectations.
3) **NOTE** For instance, it might convert XML responses from a legacy service into JSON for modern frontend applications.

#### 6. Service Discovery
1) The service discovery feature of an API Gateway **dynamically identifies the appropriate backend service instance** to handle each request.
2) This ensures seamless request routing even in environments where services frequently scale up or down.

#### 7. Circuit Breaking
1) Circuit breaking is a mechanism that temporarily stops sending requests to a backend service when it detects persistent failures, such as:
   - Slow responses or timeouts. 
   - Server errors (e.g., HTTP 500 status codes). 
   - High latency or unavailability of a service.
2) The API Gateway continuously monitors the health and performance of backend services and uses circuit breaking to block requests to a failing service.

#### 8. Logging and Monitoring
1) API Gateways provide robust monitoring and logging capabilities to **track and analyze system behavior.**
2) These capabilities include:
   - Logging detailed information about each request, such as source, destination, and response time. 
   - Collecting metrics like request rates, error rates, and latency.
3) This data **helps system administrators detect anomalies, troubleshoot issues, and optimize the system’s performance.** 
4) Many API Gateways also integrate with monitoring tools like Prometheus, Grafana, or AWS CloudWatch.

## How Does an API Gateway Work?

1) **Step 1: Request Reception**
   - The API Gateway receives the request as the single entry point to the backend system.
2) **Step 2: Request Validation**
   - Before forwarding the request, the API Gateway validates it to ensure:
        - The required parameters or headers are present. 
        - The data is in the correct format (e.g., JSON). 
        - The request conforms to the expected structure or schema.
   - If **any information is missing or incorrect, the gateway immediately rejects the request and notifies the app** with an appropriate error message.
3) **Step 3: Authentication & Authorization**
- The gateway now **verifies your identity and permissions** to ensures only legitimate user can go further
    - It forwards your authentication token (e.g., OAuth or JWT) to an identity provider to confirm your identity.
    - It checks your permissions to ensure you’re authorized to use the app for placing an order.
    - If authentication or authorization **fails, the API Gateway sends a 401 Unauthorized or 403 Forbidden** error back to the app.
4) **Step 4: Rate Limiting**
- To prevent abuse, the API Gateway **checks how many requests you’ve made recently**.
  - **For example:** If you’ve made 10 "Place Order" requests in the last minute (maybe by accident), the gateway **might block additional requests temporarily and return 429 Too Many Requests response.**
- This ensures the system remains **stable and fair for all users** specially during traffic spikes or **malicious attacks, such as distributed denial-of-service (DDoS) attempts**.
5) **Step 5: Request Transformation (if needed)**
- If any of these backend services require specific data formats or additional details, the API Gateway **transforms the request**.
- **Example :**
  - The app sends the delivery address in plain text, but the Delivery Service expects GPS coordinates. 
  - The API Gateway converts the address into coordinates before forwarding the request.
6) **Step 6: Request Routing**
- The API Gateway now needs to **coordinate several backend services to process your order**.
- Using **service discovery**, it identifies:
  - Order Service: To create a new order record. 
  - Inventory Service: To check if the restaurant has your selected items available. 
  - Payment Service: To process your payment. 
  - Delivery Service: To assign a delivery driver to your order.
- The gateway dynamically routes the request to these services using a **load balancing algorithm**, ensuring it connects to available and healthy service instances.
7) **Step 7: Response Handling**
- Once the API Gateway receives the response(s) from the backend service(s), it performs the following tasks:
  - **Transformation:** Adjusts the response format or structure to match the client’s requirements.
  - **Caching (Optional):** Stores the response temporarily for frequently accessed data, reducing future latency.
8) **Logging & Monitoring**
- Throughout this process, the gateway records important metrics to track each request.

Finally, after completing all the steps API Gateway sends the processed response back to the client in a format they can easily understand.


