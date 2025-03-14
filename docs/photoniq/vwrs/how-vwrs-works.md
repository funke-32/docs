---
sidebar_position: 5
title: How VWRs Works
---

Macrometa PhotonIQ Virtual Waiting Rooms (VWRs) are an advanced prioritization service that manages visitors entering a site. VWRs serves as a protective layer for your origin server, effectively managing high traffic volumes to prevent server overload.

## Solution Overview

The waiting room solution includes essential aspects:

- **Origin Service**: The website for which you want to set up a virtual waiting room.
- **Origin Metrics Service**: Allows you to retrieve information about a specific waiting room.
- **Waiting Room Page**: The endpoint (URL) with the waiting room attached.

![VWR Solution Architecture](/img/photoniq/vwr/vwr-solution-architecture.png)

## How It Works

The VWRs workflow ensures that users are directed to the appropriate origin service while ensuring fairness in the queue and providing metrics and alerts to the administrator.

1. Akamai EdgeWorkers check the virtual waiting room service to see if a waiting room is enabled for an origin service.
2. If there is no waiting room, then the EdgeWorker sends the request directly to the origin service. If a waiting room is enabled, then the EdgeWorker sends the request to the waiting room service.
3. The waiting room service adds the request to the waiting room.
4. When the user accesses the waiting room page, the page polls the virtual waiting room service for the latest waiting time and waiting room depth.
5. The waiting room page displays the waiting time and waiting room depth to the user.
6. When the waiting time is near zero, or the user is at the front of the queue, the waiting room page forwards the user to the origin service.
7. When the request is released, the waiting room service removes a request from the queue.
8. If a duplicate request is detected, then the waiting room service checks to see if the user has an active session.
   1. If it does, then the waiting room service returns the user's position in the queue.
   2. If it does not, then the waiting room service creates a new session and adds the request to the appropriate queue.
9. The waiting room service periodically checks the sessions to remove requests for expired sessions from the queues.
10. The waiting room service calculates the waiting time and queue depth every second and updates the telemetry for the origins and waiting rooms.
11. The waiting room service collects the metrics for each waiting room.
12. The administrator can turn customer waiting rooms on or off through Configuration APIs.
13. Requests are served from the queue for the users, based on the join time. You can configure the queue to be FIFO, random, or lottery.
