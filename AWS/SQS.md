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

### Message Lifecycle
Producer Sends Message in a Queue ---`SendMessage`---> Consumer Receives Message from the Queue ---`DeleteMessage`---> Consumer process the message and deletes the message within the Visibility Timeout Period
> **Visibility Timeout Period - Default `30 sec` Min `0 sec` Max `12 hrs`**

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
