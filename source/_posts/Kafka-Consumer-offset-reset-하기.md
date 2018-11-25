---
title: Kafka Consumer offset reset 하기
---
date: 2018-11-22 16:25:22
## 그룹 지정하여 토픽 수신
```bash
 ✘ jake.ko@jakekoui-MacBook-Pro  ~  kafka-console-consumer --bootstrap-server localhost:9092 --topic test --group testGroup --from-beginning
aaa
bbb
ccc
``` 

## 컨슈머 그룹별 offset 상태 확인
```bash
✘ jake.ko@jakekoui-MacBook-Pro  ~  kafka-consumer-groups --bootstrap-server localhost:9092 --group testGroup --describe

TOPIC           PARTITION  CURRENT-OFFSET  LOG-END-OFFSET  LAG             CONSUMER-ID                                     HOST            CLIENT-ID
test            0          3               3               0               consumer-1-39ea110a-7f65-4ec3-8a9d-22c82d8be469 /172.26.113.148 consumer-1

```
- TOPIC: 토픽 이름
- PARTITION: consumer group 내의 각 consumer가 할당된 파티션 번호
- CURRENT-OFFSET: 현재 consumer group의 consumer가 각 파티션에서 마지막으로 offset을 commit한 값
- LOG-END-OFFSET: producer쪽에서 마지막으로 생성한 레코드의 offset
- LAG: LOG-END-OFFSET에서 CURRENT-OFFSET를 뺀 값.

## 컨슈머 그룹의 offset reset
```bash
kafka-consumer-groups --bootstrap-server localhost:9092 --group testGroup --topic test --reset-offsets --to-earliest --execute

```
- --topic 대신 --all-topics를 지정하면 모든 토픽에 대해서 실행이 가능하다.
- --execute 옵션을 제거하고, --dry-run옵션으로 실행하면 실제 반영되지 않고 어떻게 변할지 결과만 출력하는 dry run이 가능하다.
```bash
 jake.ko@jakekoui-MacBook-Pro  ~  kafka-consumer-groups --bootstrap-server localhost:9092 --group testGroup --topic test --reset-offsets --to-earliest --dry-run

TOPIC                          PARTITION  NEW-OFFSET
test                           0          0

```
- 주의사항: 해당 그룹의 컨슈머를 멈추고 리셋해야 한다.(consumer group이 실행중인 상태에 offset reset을 진행하는 경우 reset은 실패한다.)
```bash
 jake.ko@jakekoui-MacBook-Pro  ~  kafka-consumer-groups --bootstrap-server localhost:9092 --group testGroup --topic test --reset-offsets --to-earliest --dry-run
Error: Assignments can only be reset if the group 'testGroup' is inactive, but the current state is Stable.

TOPIC                          PARTITION  NEW-OFFSET
 jake.ko@jakekoui-MacBook-Pro  ~ 
```

## 샘플
기존의 프로듀서가 지속적으로 메시지 생산
```bash
jake.ko@jakekoui-MacBook-Pro  ~  kafka-console-producer --broker-list localhost:9092 --topic test
>aaa
>bbb
>ccc
>ddd
>eee
>
```

중간부터 컨슘
```bash
✘ jake.ko@jakekoui-MacBook-Pro  ~  kafka-console-consumer --bootstrap-server localhost:9092 --topic test --group testGroup
ddd
eee

```

리셋 후 처음부터 컨슘하도록 변경
```bash
jake.ko@jakekoui-MacBook-Pro  ~  kafka-consumer-groups --bootstrap-server localhost:9092 --group testGroup --topic test --reset-offsets --to-earliest --execute

TOPIC                          PARTITION  NEW-OFFSET
test                           0          0
 jake.ko@jakekoui-MacBook-Pro  ~ 
 
```
컨슘 재개 후 결과 (offset 리셋되어, 처음부터 컨슘한다.)
```bash
 ✘ jake.ko@jakekoui-MacBook-Pro  ~  kafka-console-consumer --bootstrap-server localhost:9092 --topic test --group testGroup
aaa
bbb
ccc
ddd
eee
```
오프셋의 위치를 재설정하기 위한 아래와같은 상세 옵션들이 있다.

- --shift-by <Long: number-of-offsets> 형식 (+/- 모두 가능)
- --to-offset <Long: offset>
- --to-current
- --by-duration <String: duration> : 형식 ‘PnDTnHnMnS’
- --to-datetime <String: datetime> : 형식 ‘YYYY-MM-DDTHH:mm:SS.sss’
- --to-latest
- --to-earliest

--to-datetime의 경우 kafka에서 데이터를 읽어서 다른곳에 저장하는 중에 데이터 유실 또는 중복 write 등이 발생한 경우에 날짜 단위로 데이터를 다시 불러와서 재처리하고 싶은 경우 매우 유용하다.

## CLI가 아닌 Java 코드로 offset reset하기
Kafka의 경우 사용 형태에 따라 Consumer API와 Stream API 두가지를 제공한다.

- Consumer API
  - 개별 이벤트 단위의 low level 처리가 필요한 경우
  - datetime, offset 을 지정해서 원하는 대로 reset 가능
- Stream API
  - Stream processing이 필요한 경우
  - offset reset 기능 없음 (위에서 언급한 CLI tool을 사용해야함)

Consumer API를 사용할때 Java코드 레벨에서 programmatical하게 offset을 리셋하는 방법은 다음과 같다.
먼저 KafkaConsumer가 생성한 후에
```
KafkaConsumer<Object, Object> consumer = new KafkaConsumer<>(properties, keyDeser, valueDeser);
 
```
consumer loop에 진입하여 consumer.poll()을 부르기 전에, 생성된 consumer 객체에 대해 offset을 변경하는 다음 함수들을 호출하여 offset을 원하는 대로 설정할 수 있다.

- seekToBeginning: earliest로 reset
- seekToEnd: latest로 reset
- seek : 지정 offset으로 reset
- offsetsForTimes: datetime 기준으로 reset


### reference
- [https://www.letmecompile.com/kafka-consumer-offset-reset/](https://www.letmecompile.com/kafka-consumer-offset-reset/)
- https://gist.github.com/marwei/cd40657c481f94ebe273ecc16601674b
- http://blog.sysco.no/integration/kafka-rewind-consumers-offset/


tags: kafka, offset

