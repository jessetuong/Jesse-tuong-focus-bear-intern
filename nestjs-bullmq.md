1. Why is BullMQ used instead of handling tasks directly in API requests?

BullMQ allows time-consuming operations to run asynchronously in the background instead of making the client wait for the operation to finish. This keeps API responses fast and prevents long-running tasks from blocking normal request processing.

1. How does Redis help manage job queues in BullMQ?

Redis acts as the data store and coordination mechanism for BullMQ. It stores queued jobs and their states, allowing workers to retrieve jobs and update their status as they move between waiting, active, completed, and failed states.

3. What happens if a job fails? How can failed jobs be retried?

When a job fails, BullMQ records it as a failed job. Jobs can be configured with an attempts option so BullMQ automatically retries them a specified number of times. This is useful for temporary failures such as network or external service errors.

4. How does Focus Bear use BullMQ for background tasks?

BullMQ can be used by Focus Bear to move time-consuming tasks such as sending notifications, processing analytics, or synchronising data outside the main API request. The API can add a job to the queue and immediately respond, while a worker processes the task asynchronously.