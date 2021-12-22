> Individual work:
>
> https://online.manchester.ac.uk/webapps/discussionboard/do/message?action=list_messages&course_id=_67618_1&nav=discussion_board&conf_id=_396126_1&forum_id=_556822_1&message_id=_1824188_1

主题：系统DIAMOND，识别驾驶违法行为后的驾驶员的身份

基本逻辑：使用测速摄像头，捕捉超速车辆的驾驶员面部照片，交叉比对DVLA数据库（Driver and Vehicle licensing Agency），如果驾驶员数据库中没有信息，则到Idendity and Passport Service搜寻，如果那里也没有，则到Home Office 的 Foreign Nationals数据库查找外国人的照片信息。若还是没找到，则向该测速摄像头所在的区域的地方当局发送报告。

追加信息：在加油站、停车场和警车上安装自动车牌识别传感器ANPR(Automatic Number Plate Recognition)。通过这部分识别到的数据可以帮助追踪车辆。

文章提出的要求：审查报告确定应向谁发送处罚通知。资源不局限于已经提到的。每个要素都必须经过严格的连接隐私调查POCS(Privacy of Connection Survey)，创建详细的风险评估和处理计划，并配备测试设备，确保风险处理方法有效。



# Requirements analysis 

## 1. Introduction

### 1.1 Purpose of this document

To clarify system requirements, arrange project planning and progress, organize system development and testing. To get an overview of the whole system.

This document is for the reference of project managers, designers and developers.

### 1.2 Project background

Project owners: *fill_in*

Project actors: *fill_in*

Project customers: *fill_in*

This project aims to design a DIAMOND (Driver Identification after monitoring Offence using Numerous Database) system that identifies each driver that gets out of speeding.

This project involves both software and hardware support.

### 1.3 definition of keywords

DIAMOND (Driver Identification after monitoring Offence using Numerous Database)

DVLA (Driver and Vehicle licensing Agency)

IPS (Idendity and Passport Service)

ANPR (Automatic Number Plate Recognition)

POCS (Privacy of Connection Survey)

### 1.4 References

a. Project approved plan, assignment, contract or approval of superior authority

b. Project development plan

c. *fill_in_if_theres_any*

## 2. Task Overview

### 2.1 Target

To expand the design of the DIAMOND system, consider every aspect as much as possible, and come up with a reasonable design of the whole system. Especially taking security issues into account.

### 2.2 Operating environment

#### Software:

Operating system：Microsoft Windows 2000 Advanced Server

Support：IIS 5.0

Database：Microsoft SQL Server 2000

#### Hardware:

Cameras: speed cameras that supports data transfering through networks.

*(Any other things...)*

### 2.3 Conditions and limitations

 

## 3．Data Description

### 3.1 Static data

*(given databases, what datasets can we use...)*

### 3.2 Dynamic data

*(including expected inputs and outputs...)*

### 3.3 Database introduction

*(Give the name and type of database to use...)*

### 3.4 Data dictionary

*(list the attributes in a designed database)*

### 3.5 data acquisition

*(How you collect the data in need)*

## 4．(Most important) Functional module requirement

### 4.1 module division

*(different aspects of modules...)*

### 4.2 module description

*(decribe what each module does, e.g. `DatabaseWriter` is responsible for transfering data from the speed camera to a database that records people getting out of speed.)*

## 5．Performance requirements

### 5.1 Data accuracy

*(Accept all kinds of photos captured or capture for several times until it's clear. If there's a need to accpet a photo with no face captured, etc.)*

### 5.2 Time characteristics

*(such as the required response time: for how long it should take between detecting the event and the local office receive a report of the event. Update processing time, data conversion and transmission time, running time, etc.)*

### 5.3 adaptability

*(It shall be able to adapt to changes in operation mode, operation environment, interface with other software and development plan...)*

## 6．Operation requirements

### 6.1 User interface

*(Does it have a user interface, what kind of design should it be in, should it be easy to use or as simple as possible, or it should look official...)*

### 6.2 Hardware interface

*(Different kinds of hardwared involved.)*

### 6.3 Software interface

*(Is there only one suite of software or many different versions for different usages.)*

### 6.4 Troubleshooting

*(What are the possible approaches to deal with unexpected issues, e.g. Backing up the system on a daily basis...)*

## 7．Other requirements

*(such as usability, security, maintainability, portability, etc.)*

 

##  Requirements

1. it's a plan, you don't need to implement it
2. make a cookbook, consider some of the details (e.g. encryption, decryption)
3. Normal functional requirements, normal challenges(e.g.the principle of planned obsolescence, if a company's products last forever, they wouldn't make much money)
4. 6 principles of the process, 6 elements of governance



who's responsible for what, what level, (e.g. agencies, manipulations)



strategy, do we use the cloud, governance decisions ( what is allowed, what will be used)

used what standard, e.g. ISO/IEC 25010