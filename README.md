## Install MySQL and RabbitMQ
please follow up official doc to setup.

MySQL 5.7

RabbitMQ 3.5.3（生产的） 以上，本地用了3.6.5，版本影响不大

## DB schema setup
### create schema ‘test’ in MySQL
### create table
```javascript
create table if not exists `t_order` (
    `id` varchar(128) NOT NULL,
    `name` varchar(128) NOT NULL,
    `message_id` varchar(128) NOT NULL,
    PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

create table if not exists `broker_message_log` (
    `message_id` varchar(128) NOT NULL,
    `message` varchar(4000) DEFAULT NULL,
    `try_count` int(4) DEFAULT 0,
    `status` varchar(10) DEFAULT '',
    `next_retry` timestamp NOT NULL DEFAULT '0000-00-00 00:00:00',
    `create_time` timestamp NOT NULL DEFAULT '0000-00-00 00:00:00',
    `update_time` timestamp NOT NULL DEFAULT '0000-00-00 00:00:00',
    PRIMARY KEY (`message_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

## change configration
springboot-produce and springboot-consumer resources/application.properties
spring.rabbitmq.host={your local rabbit server IP}
spring.rabbitmq.port={your local rabbit server port}

## How to run demo
- start springboot-produce application
- start springboot-consumer application
- run ApplicationTests test case under springboot-produce
