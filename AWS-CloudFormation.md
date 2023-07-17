# AWS CloudFormation

Date: July 17, 2023
Last edited: July 17, 2023 4:06 PM
Tag: CloudFormation

AWS CloudFormation is a service provided by AWS that enables users to model and manage infrastructure resources in an automated and secure manner.

Using CloudFormation developers can define and provision AWS infrastructure resources  using JSON or YAML formatted infrastructure as code template. 

## How Does AWS CloudFormation work?

when creating a stack, AWS CloudFormation makes service calls to AWS to configure our resources. CloudFormation can only perform action that we have permission to do. 

Ex. to create EC2 instances by using CloudFormation we need permission to create instances. that permission are managed by `AWS identity and access management` (IAM).

### Example of CloudFormation Script

```yaml
AWSTemplateFormatVersion: 2010-09-09
Description: A simple EC2 instance
Resources:
  MyEC2Instance:
    Type: 'AWS::EC2::Instance'
    Properties:
      ImageId: ami-0ff8a91507f77f867
      InstanceType: t2.micro
```

Let's break down the code:

```yaml
AWSTemplateFormatVersion: 2010-09-09
```

This line specifies the version of the AWS CloudFormation template format being used, which is 2010-09-09 in this case.

```yaml
Description: A simple EC2 instance
```

This line provides a description or summary of the CloudFormation template. In this case, it describes that the template is for creating a simple EC2 instance.

```yaml
Resources:
```

This line marks the beginning of the "Resources" section, where you define the AWS resources to be provisioned.

```yaml
MyEC2Instance:
  Type: 'AWS::EC2::Instance'
  Properties:
    ImageId: ami-0ff8a91507f77f867
    InstanceType: t2.micro
```

This block defines a resource named "MyEC2Instance" of type "AWS::EC2::Instance". It specifies the properties of the EC2 instance, including the Amazon Machine Image (AMI) ID, which determines the operating system and software installed on the instance, and the instance type, which determines the hardware specifications of the EC2 instance.

In this example, the AMI ID is "ami-0ff8a91507f77f867", and the instance type is "t2.micro". The AMI ID and instance type can be customized according to your specific requirements.

Overall, this CloudFormation template creates a simple EC2 instance using the specified AMI and instance type.

### **Amazon SQS template snippets**

```yaml
MyQueue:
  Type: AWS::SQS::Queue
  Properties:
    VisibilityTimeout: value
```

This code snippet is written in YAML and describes the configuration of an Amazon Simple Queue Service (SQS) queue using AWS CloudFormation. Let's break it down:

- **`MyQueue`**: This is the logical name or identifier for the SQS queue resource. You can choose any name you want, but it should be unique within the CloudFormation stack.
- **`Type: AWS::SQS::Queue`**: This line specifies the resource type, indicating that we are creating an SQS queue.
- **`Properties`**: This section contains the configuration properties for the SQS queue.
    - **`VisibilityTimeout`**: This property specifies the duration (in seconds) that a message is invisible in the queue after a consumer receives it. The **`value`** placeholder should be replaced with an actual value, such as an integer representing the desired timeout in seconds.

By providing this code to AWS CloudFormation, you can create an SQS queue with the specified properties. The queue will have the logical name "MyQueue" and the specified visibility timeout.