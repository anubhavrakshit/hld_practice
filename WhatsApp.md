## High Level design of WhatsApp messaging platform

# Functional Requirements
1. Users of the platform should be able to send each other messages.
1. Users are uniquely identified by phone number. 
1. Messages might be text/images/audio/video.
1. Users get notified of Message Delivery and Message Read.
1. Users can create groups. Messages can be send/recv from groups.
1. Messages can be backed up to a third party storage.
1. Messages should be delivered in ordered fashion.

# Non Functional Requirements
1. Platform should have low latency for good user experience
1. Highly scalable to allow a very large user base
1. Platform should be available and reliable.
1. Platform should honor data privacy

# Back of the envelope calculations
1. Lets assume 100M users of the platform.Assume per user data ~1K(Phone number, Photo)
   **Total user data** to store 100M x 1k = **100 GB**
2. Lets assume ~80M DAU. Assume each user sends 100 Messages per day. Each Message is ~10KB.
   80M * 100 * 10K = 8TB. 8TB per day is the **data transferred**. So 8T / (3600 * 24) is **~92MB/sec**.
3. **QPS** is 80M * 100 / (3600 * 24) is **~92K QPS**.
4. The workload will be **write heavy**

# Key services
1. Request Route service is going to send a new chat message to Chat Message Q service.
1. Request Route service will send  creation/deletion of Group, disconnect of user to Presence Service.
1. Messages With multimedia content are sent to Media Ingest service by the Message Q service. This will compress and store large content
1. If target user of a message is disconnected Message will get Archived.
1. Notification Service will send new chat messages and delivery notifications. Large media content will be downloaded from Media service.

# High Level Diagram
[link](./WhatsApp_hld.pdf)