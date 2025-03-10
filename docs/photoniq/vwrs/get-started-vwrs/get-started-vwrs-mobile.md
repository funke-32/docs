---
sidebar_position: 20
title: Get Started with VWRs and Mobile Apps
---

This guide details how to integrate Macrometa PhotonIQ Virtual Waiting Rooms (VWRs) with your mobile applications. Unlike web-based apps, mobile apps are developed for specific platforms using platform-specific UI frameworks. Mobile apps require direct API interactions to manage user experiences effectively during high traffic periods.

## Before You Begin

Ensure you have completed the following prerequisites before starting the integration process:

- **Coordinate with Macrometa Personnel:** Secure the necessary credentials and access rights by engaging with Macrometa personnel.
- **Plan Your Waiting Room:** Identify the appropriate [queue type](../queue-types.md) for your application, determine which endpoints will incorporate the waiting room, and decide on the priority handling mechanisms.
- **Collect Information:** Gather essential information, including API endpoints and expected traffic metrics, to facilitate a smooth setup.

## Integration Overview

Integrate VWRs with your mobile applications by following these steps:

1. **API Key Creation:** Start by creating an API key to access the VWRs system, as this key is essential for all API interactions. For instructions on creating an API key, refer to [Create an API Key](https://www.macrometa.com/docs/apiVwrs#/operations/createAPIKey).

2. **Create and Configure a Waiting Room:** Create your waiting room. This step allows you to fine-tune how the waiting room operates and integrates with your site. For comprehensive guidance on waiting room configuration, refer to [Configure a Waiting Room](../configure-waitingroom.md).

3. **API Usage for Queue Management:** Use the VWRs API to manage the user's position in the waiting room. This involves making periodic API calls to check the queue status and manage the user experience accordingly.

  - [Get initial position in waiting room](https://www.macrometa.com/docs/apiVwrs#/paths/api-vwr-v1-position-waitingroom_key/get)
  - [Get current position in waiting room](https://www.macrometa.com/docs/apiVwrs#/paths/api-vwr-v1-position-waitingroom_key---request_id/get)

## Pseudo-Code Example

Here is a pseudo-code example illustrating how a mobile app interacts with the VWR API to manage a user's waiting experience:

```javascript
// Initial request specifying the waiting room.
let waitingRoom = "shopping";
let result = GET("/api/vwr/v1/position/" + waitingRoom);

// Loop while the user is still in the waiting room.
while (result.position > 0) {
    // Notify the user of their current position and expected wait time.
    notifyUser(result.position, result.waiting_time);

    // Wait for the specified refresh interval before checking the position again.
    sleep(result.refresh_interval);

    // Re-check the user's position using the visitor_id received from the initial call.
    result = GET("/api/vwr/v1/position/" + waiting_room + "/" + result.visitor_id);
}

// Proceed with accessing the protected resource once the user is out of the waiting room.
accessResource();
```

## Next Steps

Once your virtual waiting room is operational, consider monitoring and managing its performance to ensure optimal functionality:

- **Metrics and Analytics:** Regularly check the VWRs metrics to assess the performance and effectiveness of your waiting room. For more information on accessing VWRs metrics, refer to [VWRs Metrics](../vwrs-metrics.md).
- **Review Usage Patterns:** Analyze usage data to optimize settings and improve user experiences. Access hourly, daily, or monthly usage statistics through the following links:
  - [Hourly Usage](https://www.macrometa.com/docs/apiVwrs#/operations/getHourlyUsage)
  - [Daily Usage](https://www.macrometa.com/docs/apiVwrs#/operations/getDailyUsage)
  - [Monthly Usage](https://www.macrometa.com/docs/apiVwrs#/operations/getMonthlyUsage)
