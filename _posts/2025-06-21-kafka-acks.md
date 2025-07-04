---
title: Kafka Producer option - Acks
date: 2025-06-21 14:21 +000
categories: [Server, Kafka]
tags: [Kafka]
---

## Acks 

- Acknowledgements
- Producer 가 보낸 메세지를 Kafka 가 잘 받았는지 확인(acks) 

| Option        | Description                                                                                           |
|---------------|-------------------------------------------------------------------------------------------------------|
| acks=1        | - 카프카 서버의 확인(acks) 응답을 기다리지 않음 <br>- 메시지 손실 가능성이 높지만 빠른 전송이 필요한 경우                                    |
| acks=0        | - 카프카가 잘 받았는지 확인(acks)을 함 <br>- 메시지 손실 가능성이 적고 적당한 속도의 전송이 필요한 경우 <br>- 아주 예외적인 경우 일부 메시지가 손실될 수 있음   |
| acks=all (-1) | - 프로듀서가 메시지를 전송하고 난 후 리더가 메시지를 받았는지 확인하고 추가로 팔로워까지 메시지를 받았는지 확인<br>- 전송 속도는 느리지만 메시지 손실이 절대 없어야 하는 경우 |


### `acks=all` 과 브로커 설정 
- `acks=all` 을 완벽하게 사용하기 위해서는 브로커 설정도 같이 조정해줘야 함 
- 브로커의 설정에 따라 응답 확인을 기다리는 수가 달라질 수 있음
  - `min.insyncs.replicas` : 최소 리플리케이션 팩터를 지정 

#### `min.insyncs.replicas=1`

- 리플리케이션이 3개인 경우 리더가 메세지를 받고 최소 하나의 리플리케이션 조건을 만족했기 때문에 acks 를 보냄
-  결론적으로 `acks=1` 과 동일하게 동작함 


#### `min.insyncs.replicas=2`

- 리더가 메세지를 저장하고, 다른 팔로워까지 메시지가 저장된 후 acks 를 보냄 (최소 리플리케이션 조건 만족)
- 만약 리더가 acks 를 보내자마자 리더 선출 작업이 발생하더라도 메세지를 받은 다른 팔로워가 있기 때문에 메시지 손실은 발생하지 않음
- 즉 1대 정도의 서버에 장애가 발생하더라도 손실 없는 메시지 전송을 유지할 수 있음 
- 아파치 카프카 문서에서 손실 없는 메시지를 전송하기 위한 권장 조건
  - 프로듀서 `acks=all`
  - 브로커 `min.insync.replicas=2`
  - 토픽의 리플리케이션 팩터 3


#### `min.insyncs.replicas=3`

- 카프카는 브로 하나가 다운되더라도 크리티컬한 장애 상황없이 서비스를 잘  처리할 수 있도록 구성되어 있는데, `acks=all`, `min.insyncs.replicas=3` 으로 설정하게 되면 브로커 하나만 다운되더라도 카프카로 메시지를 보낼 수 없는 클러스터 전체 장애와 비슷한 상황이 발생하게 됨 
