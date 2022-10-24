# SQS
Simple Queue Service
1. Pull Based Mechanism
2. Controller Over who sends and recieves messages
3. Message contents can be protected using SSE - Server Side Encryption
4. High Concurrent Access to Messages
5. High Availability for producing and consuming messages
6. Reliable
7. Customisable

### Architecture
3 main parts -
1. Components of distriutes system
  - Consumers
  - Producers
2. Queue (Distributed over Amazon Servers)
  - Standard Queue
  - FIFO Queues
3. Messages in a queue

> Messages in a queue are spread accross multiple servers in Amazon and the messages are duplicated all over the server

### Queues
1. Standard Queue 
  - Nearly Unlimited API method (`SendMessage`, `ReceiveMessage`, `DeleteMessage`) 
  - A message is delivered atleast once but ocassionally more than 1 copy is delivered
  - Ocassionally messages are delivered in order which it has been received
  - Decoples live user from enetring into background work

2. FIFO Queue - Order matters
  - Uses Batching
  - 3000 calls per second for every API method (`SendMessageBatch`, `ReceiveMessage`, `DeleteMessageBatch`) = 300 API Calls each with a batch of 10 messages
  - Order is critical (Order is on the basis of messgaes pushed in the queue)

### Message Lifecycle
`SendMessage` Producer Sends Message in a Queue 
`ReceiveMessage` Consumer Receives Message from the Queue 
`DeleteMessage` Consumer process the message and deletes the message within the `VisibilityTimeout`
`PurgeQueue` Remove all messages from queue keeping the queue in place

> **`VisibilityTimeout` - Default `30 sec` Min `0 sec` Max `12 hrs`**

Amazon SQS automatically deletes messages that have been in a queue for more than the `MessageRetentionPeriod`.

> **`MessageRetentionPeriod` - Default `4 days` Min `60 sec` Max `14 days`**

### In Flight Messages
1. Sent Messages by a Producer
2. Recieved Messages by a Consumer
3. Delete Message from the Queue

State btw 1 and 2 **Stored Message** - Unlimited Messages
State btw 2 and 3 **In Flight Message** - Limited Messages
  - Standard Queue - Max `1,20,000`
    - If via Short Polling - AWS SQS returns `OverLimit`
    - If via Long Polling - AWS SQS returns nothing
  - FIFO Queue - Max `20,000` - AWS SQS returns nothing

### Pricing
1. Cost of Interactions with S3
2. Cost of key management services
3. Number of requests/action     Standard       FIFO 
   0 - 1 Million                  Free         Free
   1 Million - 100 Billion        $0.40        $0.50
   100 Billion - 200 Billion      $0.30        $0.40
   200 Billion +                  $0.24        $0.35
4. Request = Action
  - API Action
    - Sending Message
    - Receiving Message
    - Deleting Message
    - Changing Visibility Message (For FIFO)
    - 1 Request can have 1-10 messages upto 256KB
    - Every 64KB 1 Action

### Short Polling
- The `ReceiveMessage` request queries only a subset of servers to find any new message
- AWS SQS right away sends a response back even if no message is found
- When `ReceiveMessage` sets `WaitTimeSeconds = 0` or `ReceiveMessageWaitTimeSeconds = 0`
- A lot of empty and false empty responses (because a subset is only queried) are recieved.

### Long Polling
- The `ReceiveMessage` request queries all of the servers to find any new message
- AWS SQS waits for atleast 1 message, up to maximum number of messages specified in the request.
- It returns with a empty response only if the olling time expires
- When `ReceiveMessage` sets `WaitTimeSeconds > 0 (Max 20 sec)` or `ReceiveMessageWaitTimeSeconds = 0`
- Reduces cost as it reduces the number of empty responses or false empty response

### Delay Queue
- Lets you postpone the delivery of a new message
- Gives time to the consumers to process the previous messages 
- `DelaySeconds = Default (0 sec) Max (15 min)`


> You can add metadata tags that identify a queue's purpose, owner, or environment

### IMP Metrics
- ApproximateNumberOfMessages
- ApproximateNumberOfMessagesDelayed
- ApproximateNumberOfMessagesNotVisible
- ApproximateNumberOfMessagesVisible


## Topics to write about
1. ~~Short Polling~~
2. ~~Long Polling~~
3. Visibility Timeout
4. Dead letter queue
5. ~~Delay Queue~~
6. Temporary Queue
7. Message Timmers
8. Retries
9. Queue and message identifiers
10. Message metadata
