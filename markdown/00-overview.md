## High Level Overview

| Item        | Description                                                                                                                            |
|:------------|:---------------------------------------------------------------------------------------------------------------------------------------|
| Node        | A node is a program compiled to interact with ros topics.  Nodes can be run on different PC's and communicate over communication layer |
| Message     | particular data type that gets passed between nodes                                                                                    |
| Topics      | A category of messages that a node can subscribe to                                                                                    |
| Master      | the server that sends and receives messages and coordinates all communication                                                          |
| Package     | collections of nodes & data types that work together...project.  They are written in python and/or C++                                 |
| launch file | a method for starting up a number of ros nodes, services and topics. synchronizes the startup of ros stuff                             |


