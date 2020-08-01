---
layout: post
title:  Alibaba Distributed Middleware
date:   2020-07-31 23:03:36
categories: Distributed   Diamond
---
Before I joined in alibaba, the thing always in my mind is how the web service can meet such plenty of users and service need to ensure the quality of web service and accuracy. Recently, I have learned the middleware used in alibaba.inc, I have understood how these needs can be satisified. The shift from "stand-alone architecture" to "distributed architecture" solves this problem. This requires the decoupling of services, the splitting of large services or systems into small service interfaces or small systems, and finally the integration of services, that is, the distributed deployment of services, the diversion of requests, the separation of data operations (read-write separation), and the masking of many underlying services. This leads to the HSF high-speed service framework.

And the foundation of distributed architecture is network, in order to connect computers and let them work together, but the huge amount of connections of the network raises a new problem -- the transmission of network messages, including the sequence, delay and loss of message transmission. In the scenario of high multithreading concurrency, it is necessary to ensure that there is no deadlock problem caused by resource competition, which introduces the use of messaging middleware such as Notify and MetaQ to integrate messages into message queues and consume them one by one in the mode of delayed consumption.

At the same time, the storage capacity of a computer is limited, in distributed architechture, in the face of huge data source, storage capacity of a single one is not enough, so we introduce distributed database, like TDDL, not only ensure the performance of the relation database, but also improve the ability of taking risk. The application of distributed cache (Tair) can process a large amount of dynamic data and meet the network needs of users in the network era.

Finally, the application of Pandora is to isolate the connection between WebApp and middleware and between middleware itself, so as to ensure the system elasticity, maintain the security of architecture, and facilitate the later testing and upgrading.

In short, the essence of a distributed architecture is the collaborative operation of so many computers to accomplish tasks which are difficult for a stand-alone architecture to accomplish. For example, when you need to compute the sum from 1 to one billion, if you don't consider cross-border issues, you can use a for loop to complete, but it will be quite slow, may take several years to improve computing performance to shorten the calculating time significantly, but with the introduction of the distributed idea, application more machine to complete a piece of work can greatly shorten the operation time of the whole. What's more, the advantages of distributed architecture not only includes computing power, but also includes the data storage capacity, information processing ability, etc.

## About Diamond ##

Diamond's reliability and ease of use are inseparable from its design architecture, just as its design principle "Make it Simple". And its characters can ensure the operation of other Alibaba applications. With the increase of the company's business and the expansion of the size of the configuration services, while fully considering the network and practical applications may appear in various situations, to ensure the ability to deal with errors.

However, the biggest doubt in my mind is why we need it, I know a lot of applications in alibaba group need it, But why is it? The reason can be traced back to the emergence of Distributed Systems. In "Distributed Systems For System Architects", "Configuration Of Distributed Systems" has been mentioned, the concept and difference between static and dynamic configuration also be briefly discussed. In summary, the configuration is the behavior of dynamic adjustment ability, for the distributed system, the development of the whole line is a very time-consuming and huge process, the updates of the system don't like those single stand system which just need to restart the machine or process. To achieve sustained, painless to add new function or adjust existing function requires dynamic configuration management. Fundenmentally, dynamic configuration is configuration is not coupled to the software version, so configuration can be changed when the process running.

### Why Alibaba need Diamond ###

After checking a lot of materials, I found that diamond is the only one dynamic configuration center China, and it is also rare in the world. There are two reasons I found:

(1) The first is the rise of TDDL, which can partition the database and table, so the storage of configuration information after database and table fragmentation becomes a problem. Initially, Diamond is a part of ConfigSever, then Diamond is removed from it. In this process, we also figured out the influence of data persistence on product stability and the difference between Service Discovery and Dynamic Configuration Management.

(2) The connection of configure and the environment. In the configuration, some environments may need to set different values, but some environments may need consistent values. This difference can not be solved by configuration center, so the configuration management system needs to provide a convenient way to interact to ensure both demands. So I think the complexity of Alibaba's internal environment is also the reason for Diamond's emergence.
