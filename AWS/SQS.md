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
  - Provide best-effort ordering which ensures that messages are generally delivered in the same order as they are sent. Occasionally (because of the highly-distributed architecture that allows high throughput), more than one copy of a message might be delivered out of order.
  - guarantee that a message is delivered at least once and duplicates can be introduced into the queue.
  - allow nearly-unlimited number of transactions per second.
  - are available in all the regions.
  - supported by all AWS services.
2. FIFO Queue - Order matters

### Message Lifecycle
Producer Sends Message in a Queue --- `SendMessage` ------ `ReceiveMessage` ---> Consumer Receives Message from the Queue ---`DeleteMessage`---> Consumer process the message and deletes the message within the Visibility Timeout Period
> **Visibility Timeout Period - Default `30 sec` Min `0 sec` Max `12 hrs`**

Amazon SQS automatically deletes messages that have been in a queue for more than the maximum message retention period.

> **Maximum Message Retention Period - Default `4 days` Min `60 sec` Max `14 days`**

### In Flight Messages
1. Sent Messages by a Producer
2. Recieved Messages by a Consumer
3. Delete Message from the Queue

State btw 1 and 2 **Stored Message** - Unlimited Messages
State btw 2 and 3 **In Flight Message** - Limited Messages

Standard Queue - Max `1,20,000`
1. If via Short Polling - AWS SQS returns `OverLimit`
2. If via Long Polling - AWS SQS returns nothing

FIFO Queue - Max `20,000` - AWS SQS returns nothing
