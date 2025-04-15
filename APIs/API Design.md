
[Introduction](https://youtu.be/7QfswaV0re4?si=bVY6dJH1xOD3o5ti)

#### **What is an API?**

An **API (Application Programming Interface)** is a set of rules and protocols that allows different software applications to communicate with each other. It defines how requests and responses should be structured, enabling interoperability between systems.

---

#### **CRUD Operations**

CRUD stands for **Create, Read, Update, and Delete**, which represent the four basic operations in APIs:

- **Create** → Adding new data (e.g., `POST` request)
- **Read** → Retrieving data (e.g., `GET` request)
- **Update** → Modifying existing data (e.g., `PUT` or `PATCH` request)
- **Delete** → Removing data (e.g., `DELETE` request)

---

#### **HTTP Protocols in APIs**

APIs communicate over **HTTP(S)** using different methods:

- **GET** → Retrieve data
- **POST** → Create new resources
- **PUT** → Update/replace an existing resource
- **PATCH** → Partially update a resource
- **DELETE** → Remove a resource

These methods help define how a client interacts with a server.

---

#### **API [[Paradigms]]: Types, Advantages & Disadvantages**

1. **REST (Representational State Transfer)**
    - **Advantages:** Stateless, scalable, flexible, widely adopted
    - **Disadvantages:** Can be complex, over-fetching/under-fetching of data

2. **GraphQL**    
    - **Advantages:** Fetches only required data, reduces multiple requests
    - **Disadvantages:** More complex server-side implementation

3. **gRPC (Google Remote Procedure Call)**    
    - **Advantages:** High performance, supports streaming, ideal for microservices
    - **Disadvantages:** Harder to debug, not human-readable like JSON

4. **WebSockets**
    - **Advantages:** Real-time communication, bi-directional connection
    - **Disadvantages:** Can be resource-heavy, less suitable for simple APIs


---

#### **Key API Design Principles**

- **Idempotency:** API requests should produce the same result no matter how many times they are called (e.g., `PUT` and `DELETE` should not create duplicates).
    
- **Avoid Mutating Data in GET Requests:** `GET` should be **read-only** and never change data to prevent unintended side effects.
    
- **Backward Compatibility & Versioning:**
    
    - Avoid breaking changes in APIs to ensure older clients still function.
    - Use versioning (`v1`, `v2` in URLs or headers) to manage updates.
- **Rate Limiting:** Protects APIs from abuse by restricting the number of requests a user can make in a given time (e.g., 100 requests per minute).
    
- **CORS (Cross-Origin Resource Sharing):** Security mechanism that controls which domains can access an API, preventing unauthorized cross-site requests.
    

---

#### **In-Depth: REST API**

- **Stateless:** Each request must contain all necessary data (no session dependency).
- **Resource-Based:** Uses URLs to represent resources (e.g., `/users/123` for user data).
- **Uses JSON/XML:** Common formats for request/response bodies.
- **Layered Architecture:** Can include authentication, caching, and rate-limiting layers.

REST remains the most widely used API paradigm due to its simplicity and scalability.
