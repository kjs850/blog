---
title: Kafka Consumer offset reset - java code
---
date: 2018-11-28 18:09:53

## java로 특정 시간의 offset 부터 가져오기

```java

package com.example.kafkaoffsettest;

import org.apache.kafka.clients.consumer.ConsumerRecord;
import org.apache.kafka.clients.consumer.ConsumerRecords;
import org.apache.kafka.clients.consumer.KafkaConsumer;
import org.apache.kafka.clients.consumer.OffsetAndTimestamp;
import org.apache.kafka.common.TopicPartition;
import org.joda.time.DateTime;

import java.time.Instant;
import java.util.*;

import static com.example.kafkaoffsettest.KafkaConsumerUtil.TOPIC;
import static com.example.kafkaoffsettest.KafkaConsumerUtil.createConsumer;
import static java.time.temporal.ChronoUnit.DAYS;
import static java.time.temporal.ChronoUnit.MINUTES;

public class KafkaConsumerFromTime {

    public static void main(String[] args) {
        KafkaConsumer<String, String> consumer = createConsumer();
        consumer.subscribe(Arrays.asList(TOPIC));

        boolean flag = true;

        while (true) {
            ConsumerRecords<String, String> records = consumer.poll(100);

            if (flag) {
                Set<TopicPartition> assignments = consumer.assignment();
                Map<TopicPartition, Long> query = new HashMap<>();
                for (TopicPartition topicPartition : assignments) {
                    query.put(
                            topicPartition,
                            Instant.now().minus(1, DAYS).toEpochMilli());
                }

                Map<TopicPartition, OffsetAndTimestamp> result = consumer.offsetsForTimes(query);

                result.entrySet()
                        .stream()
                        .forEach(entry ->
                                consumer.seek(
                                        entry.getKey(),
                                        Optional.ofNullable(entry.getValue())
                                                .map(OffsetAndTimestamp::offset)
                                                .orElse(new Long(0))));

                flag = false;
            }


            for (ConsumerRecord<String, String> record : records) {
                long timestamp = record.timestamp();
                DateTime dateTime = new DateTime(timestamp);
                System.out.printf("dateTime = %s, offset = %d, key = %s, value = %s%n", dateTime, record.offset(), record.key(), record.value());
            }
        }


    }
}


```
## 결과
```bash
> date      
Wed Nov 28 18:20:25 KST 2018

//실행결과
dateTime = 2018-11-28T17:43:58.201+09:00, offset = 26, key = null, value = foo1
dateTime = 2018-11-28T17:43:58.208+09:00, offset = 27, key = null, value = foo2
dateTime = 2018-11-28T17:43:58.208+09:00, offset = 28, key = null, value = foo3
```
tags: [kafka, offset, java]
