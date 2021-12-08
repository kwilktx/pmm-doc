# MongoDB read tickets are higher than 128.

## Description
This check returns a warning if the number of read tickets is higher than 128. This can cause performance issues.
Ideally the number of tickets should be based on the number of CPU's available.
The default read ticket is 128.
It can be adjusted for your mongod and your mongos nodes.

[https://docs.mongodb.com/manual/reference/parameters/#mongodb-parameter-param.wiredTigerConcurrentReadTransactions](https://docs.mongodb.com/manual/reference/parameters/#mongodb-parameter-param.wiredTigerConcurrentReadTransactions)



## Rule
MONGODB_GETPARAMETER

`db.adminCommand( { setParameter: 1, "wiredTigerConcurrentReadTransactions": "128"  } )`

## Resolution
Please Perform the steps mentioned below to adjust the number of read tickets configured for use.

This change can be done online while running or it can be done in the config file to take effect after the next restart.

A. To make this change while running/online without downtime, please use the following command:

`mongo> db.adminCommand( { setParameter: 1, "wiredTigerConcurrentReadTransactions": "128"  } );`

B. To make this change go into effect after the next restart, use the following steps:

1. As an example, Set to default. 
Edit mongod.conf and set the below parameter.
```
          setParameter:
            wiredTigerConcurrentReadTransactions: 256
```
2. If resetting the read ticket in your mongod config file, be aware that this will not take effect until the next restart.
