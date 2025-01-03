# Amazon Linux

#### Linux operating system from AWS. It provides a security-focused, stable, and high-performance execution environment to develop and run cloud applications.

<img src="https://d1.awsstatic.com/Amazon-Linux_1200x900_Logo-2.71696520835a68e1fcd9b7eda847db9dd81e95b0.png" alt="Amazon Linux 파트너 - Amazon Web Services(AWS)" style="zoom:30%;" />



## Why?

- **Stability and security**

  Amazon Linux is designed to be stable and secure, by using the latest security policies 

- **Integration with AWS**

  Amazon Linux includes packages that enable easy integration with AWS

  - `aws-cli` :AWS Command Line Interface
  - `aws-sdk-java`: Java SDK for AWS services
  - `ec2-utils` : EC2 instance utilities
  - `ec2-instance-connect` :For secure SSH connections
  - `awslogs` : CloudWatch Logs agent

- **Ongoing updates**

  AWS provides ongoing security and maintenance updates for all instances running Amazon Linux.





## AL2 vs AL2023

#### 1. Kernel Version

- AL2023 uses kernel 5.15 by default, while AL2 uses kernel 5.10
- Both kernels are LTS (Long Term Support) versions, but 5.15 includes newer features and security updates

<br/>

#### 2. Package Management

- AL2: Uses `YUM` package manager
- AL2023: Uses `DNF` package manager
  - DNF is the successor to YUM

<br/>

#### 3. Network System Service

- AL2: Uses `ISC dhclient` or `dhclient`
- AL2023: Uses `systemd-networkd`

<br/>





