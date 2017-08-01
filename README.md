# ChanaMQ Server

[ChanaMQ](http://https://github.com/qingmang-team/chana-mq) is an Akka based, AMQP messaging broker. It currently supports:

 * AMQP 0-9-1

## Status

 * ChanaMQ is still under the alpha phase.
 * Methods/Features are not supported yet:
   * Connection.SecureOk / Connection.Blocked / Connection.Unblocked
   * Channel.Flow
   * Exchange.Bind / Exchange.Unbind
   * ~~Basic.Reject~~ / ~~Basic.Nack~~ / Basic.RecoverAsync / Basic.Recover
   * Access.Request
   * Tx.Select / Tx.Commit / Tx.Rollback
   * ~~Confirm.Select~~ / ~~Confirm.SelectOk~~

## Building From Source and Packaging

 * sbt clean chana-mq-server/dist

## Installation

 * unzip chana-mq-server/target/universal/chana-mq-server-x.x.x.zip; 
 * cd conf; cp prod.conf application.conf
 * edit application.conf for your configuration
 * cd bin; ./chana-mq-server &
 * To enable persistent feature, you need to install Cassandra and create chanamq space and tables as [create-cassantra.cql](https://github.com/qingmang-team/chanamq/blob/master/chana-mq-server/src/main/resources/create-cassantra.cql)

## High Available

HA of ChanaMQ is based on Akka cluster HA. It does not support queue mirror, but the message will survive hardward failure and node down if its delivery mode is set to 2 (persistent), and the queue and exchange are both durable. Each message is located on a single node, but will be reloacted to another node and recovered from persistence when this single node is down.

## License

ChanaMQ server is licensed under the [Apache License version 2.0](LICENSE-APACHE2).

