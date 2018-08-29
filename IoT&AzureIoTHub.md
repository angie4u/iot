# IoT and Azure IoT Hub
## IoT란 무엇인가?
  Remote Device로 부터 -> Sense Things 감지하고 -> Get Insight 정보와 인사이트를 얻고 -> Take Action 그에 걸맞는 행동을 취함  

> So what is the Internet of Things? For now you can think of IoT as a system that uses the infrastructure of the Internet to establish a connection to and between our electronic devices. 

## IoT Reference Architecture
![image](https://user-images.githubusercontent.com/16282358/44759226-bf11be80-ab73-11e8-8331-a39112708889.png)
* [IoT Reference Architecture Youtube 영상](https://www.youtube.com/watch?time_continue=122&v=l7OaSNeTcas)
* IoT HUb
  * Bi-directional device <-> cloud
  * 10억(10 million)개의 장치 연결 가능
  * 원격으로 측정된 데이를 보고, 명령을 내릴수 있는 기능등을 제공
  * 장치 등록하고 식별 가능
  * 장치 관리 가능
  * MQTT/AMQP/HTTPS 프로토콜 지원

![image2](https://user-images.githubusercontent.com/16282358/44759452-31cf6980-ab75-11e8-9098-f9dd14a4a3fb.png)
* Data를 분석에 활용하는 시나리오
  * Cold Path: IoT 장비에서 측정된 데이터를 분석 및 활용
  * Hot Path: IoT 장비에서 측정되고 있는 데이터를 실시간으로 분석 및 활용

## IoT 시나리오에서 이용해 볼 수 있는 여러 Azure Service들
![image](https://user-images.githubusercontent.com/16282358/44759739-ae167c80-ab76-11e8-83ac-9e921d57031c.png)

## 적절한 Data Storage 선택하기
1. Relational DB - SQL DB, SQL Server Stretch DB
2. Big Data - Data Lake Store, SQL DW 
3. Key-value DB - Table Storage, Redis Cache
4. Document DB - Document DB, Cosmos DB / Two dimensional row-columns, 선언적 스키마, 입증된 안정성 및 보안 
4. Blob Storage - Azure Blob Storage / 비 구조화된 이미지 등등의 데이터, REST API로 접근 가능, Streaming 혹은 Random Acess 지원

## 여러 Azure IoT 솔루션 비교
* [https://docs.microsoft.com/en-us/azure/iot-fundamentals/iot-services-and-technologies](https://docs.microsoft.com/en-us/azure/iot-fundamentals/iot-services-and-technologies)
