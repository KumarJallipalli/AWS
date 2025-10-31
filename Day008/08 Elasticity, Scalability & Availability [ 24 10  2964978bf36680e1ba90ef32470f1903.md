# 08. Elasticity, Scalability & Availability [ 24/10/2025 ]

---

## Elasticity

- `Elasticity` → Increasing or decreasing the No of servers based on workload
- Elasticity can be achieved in AWS using `Auto-Scaling`
- Auto-Scaling → Scale Out [ Increasing No of Servers ] & Scale In [ Decreasing No of servers ]
    - Here, Scale Out comes first → As we Won’t directly Scale In, which is reducing the Servers → Increasing Load
- Elasticity is also known as `Horizantal-Scaling`
- Elasticity is short term
- This Elasticity is seen during Big Billion Day sales where No of servers will be increased for just 2 - 7 days

## Scalability

- `Scalability` → Increasing or Decreasing the capacity of the Server [ like from 8GB RAM to 32GB RAM ]
    - ex: Standalone Servers like DB servers
        - Where, DB Server is very largely configured like 10TB ROM, 8 CPU’s & 16GB RAM [ due to large data & high performance ]
        - Hence, increasing the NO. of DB servers is NOT a good idea [ due to replication & cost ]
            - But, we will have multiple DB Servers & Separate LB pointing to DB’s [ ⇒ Multiple LB’s ] to achieve High Availability
- Scalability → Scale Up & Scale Down
- Scalability is also known as `Vertical Scaling`
- It [ Scalability ] requires Downtime
- Scalability is Long Term
- In AWS, Scalability is Achieved by Changing the Instance Type
    - Instance Type → Memory [ RAM ] + CPU
- This scalability is majorly seen in standalone servers

![image.png](image.png)

## High Availability

- `High Availability` → The period of time for which the service is available to the customer
- The period of time for which the service is NOT Available to the customer is called `Downtime`
- HA is always measured in percentage [ % ]

Let’s say, we have a customer named “Akshay”, who have an application But reached us to deploy it & give him the URL

- We deployed the app in a server & it’s IP address of server is `192.168.10.20` & gave him URL as → http://192.168.10.20/index.html
- It is working fine for some time & then suddenly URL crashed → URL is NOT working → Server is NOT working
- Then we have deployed the same app in multiple servers & gave him those 3 URL’s, So when if 1 fails he can use the other 2 URL’s [ Redundancy ]
- Hence, We have introduced a LB to distribute the incoming traffic actoss these 3 servers
- But remembering these 3 URL’s is difficult & Prone to Fraud
- Hence, We gave him a domain name which is assigned to LB → http://akshay.com

![image.png](image%201.png)

## How to Achieve High Availability

To achieve HA, we require 3 things `RMF`

- `Redundancy` → Duplicate || same || copy || repeating → keeping/hosting the same application on multiple servers
- `Monitoring` → Checking whether the Application is reachable or not
    - LB will always monitor using health checks of application [ NOT the Server ]
    - How does LB know that the application is down..?
        - It will monitor continuously with specified intervals of time with the help of health checks [ i.e., through status codes like 200 ]
- `Failover` → redirecting the incoming requests to available server, when one of the server goes down
    - If One Server goes down, Other Server will take the request

<aside>
💡

NOTE:

- LB will monitor [ will Do the health checks of ] Application but NOT the server
    - Because, If we monitor the application we will be monitoring server too, as App will reside inside the server
- LB will Do/Manage the Failover
- LB is a Service in AWS called ELB [ Elastic Load Balancer ]
</aside>

But what if all the servers goes down → then HA is NOT achieved

- Hence, To achieve 100% HA → we will implement `auto-scaling` on top of RMF
- i.e., Zero Downtime is achieved using auto-scaling on top of RMF, which is also known as `Fault Tolerance` → Achieving Zero Downtime

![image.png](image%202.png)

![image.png](image%203.png)

![image.png](image%204.png)

![image.png](image%205.png)

![image.png](image%206.png)

In this way, we need to implement architecture in such a way that,

- Even if half of the infrastructure is down,
- Application (or) Customer should NOT be impacted → 100% HA