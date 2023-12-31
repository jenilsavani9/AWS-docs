# AWS SQS

Date: July 17, 2023
Last edited: July 17, 2023 1:59 PM
Tag: SQS

Amazon Simple Queue Service (Amazon SQS) offers a secure, durable, and available hosted queue that lets you integrate and decouple distributed software systems and components.

# **Amazon SQS architecture**

## ****Distributed queues****

three major parts in distributed messaging queues

- components of distributed system.
- Queue
- message in the queue

![ArchOverview](https://github.com/jenilsavani9/AWS-docs/assets/74345702/71566743-2a55-4c25-95c6-7cf79203f080)

in our system there are many producers, consumers and queue which holds the message.

### Message Lifecycle

![sqs-message-lifecycle-diagram](https://github.com/jenilsavani9/AWS-docs/assets/74345702/c7a62c1f-efa6-4a24-98d6-848ac665a34a)

`1` A producer (component 1) sends message A to a queue.

`2` When a consumer (component 2) is ready to process messages, it consumes messages from the queue, and message A is returned. While message A is being processed, it remains in the queue and isn't returned to subsequent receive requests for the duration of the visibility timeout.

`3` The consumer (component 2) deletes message A from the queue to prevent the message from being received and processed again when the visibility timeout expires.

## **Amazon SQS queue types**

Amazon SQS supports two types of queues – **`standard`** queues and **`FIFO`** queues.

![Screenshot 2023-07-17 122732](https://github.com/jenilsavani9/AWS-docs/assets/74345702/f0945abe-09e3-4a7a-9171-99c5563f299b)

## **Send Messages Between Distributed Applications with Amazon Simple Queue Service (SQS)**

use case : storage of incoming orders from an e-commerce application.

Login to the amazon SQS console. click on get started now.

## Create Amazon SQS queue

In amazon SQS console write queue name and select queue type to standard queue. after that click on Quick create queue.

![tmt_send-receive-async-messages_2c 64fe49350b38fa4e8fd12406a5d90f85cbaa1714](https://github.com/jenilsavani9/AWS-docs/assets/74345702/bd574fac-10cb-45e9-b35a-2511d2c7ae7f)

new queue is created and selected in the queue list.

![tmt_send-receive-async-messages_2d 3de4b5035ad88e4b5284e86628bb7a4727626eb6](https://github.com/jenilsavani9/AWS-docs/assets/74345702/bb4b0610-a722-446f-90b9-0ecda56f5e5c)

## Send Message to the queue

for sending the message in the queue select queue actions and select send a message. the send message to orders dialog box is displayed.

on the message body enter the order details. click on send message.

![tmt_send-receive-async-messages_3b 7ff48cee9d639646b39c41f0fe6bb7616fde47c7](https://github.com/jenilsavani9/AWS-docs/assets/74345702/86d1f7f3-3269-45b7-b711-a2b9ec80336e)

## Creating an Amazon SQS queue (AWS CloudFormation)

for creating a aws queue we have to use `AWS::SQS::Queue` resource in aws CloudFormation. 

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Resources:
  MyQueue:
    Properties:
      QueueName: MyQueue.fifo
      FifoQueue: true
      ContentBasedDeduplication: true
    Type: AWS::SQS::Queue
Outputs:
  QueueName:
    Description: The name of the queue
    Value:
      Fn::GetAtt:
        - MyQueue
        - QueueName
  QueueURL:
    Description: The URL of the queue
    Value:
      Ref: MyQueue
  QueueARN:
    Description: The ARN of the queue
    Value:
      Fn::GetAtt:
        - MyQueue
        - Arn
```

if we want to create a `FIFO` queue than queue name should be ending with fifo. if we want to create a standard queue than we have to remove `FifoQueue` and `contentBasedDeduplication`. 

Here, resource type is SQS queue and name is MyQueue.fifo. 

In output we receive, Queue Name, Queue URL, Queue ARN.
