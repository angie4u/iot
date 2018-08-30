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
여러가지의 IoT 관련 컴포넌트들이 Azure상에 있지만 그중에서도 솔루션 형태로 제공되는 것은 두가지가 있다. 
PaaS 형태의 솔루션인 [Azure IoT solution accelerators](https://azure.microsoft.com/en-us/features/iot-accelerators/)와 SaaS 형태의 솔루션인 [Azure IoT Central](https://azure.microsoft.com/ko-kr/services/iot-central/)이다. Azure IoT solution accelerator는 구 IoT suite으로 불련던 것인데 최근에 개명했다. -_-

## IoT Hub Messaging
Device to Cloud, Cloud to Device 모두 지원하며 **최소 한번 이상 메세지 배달**을 보장한다. 

### Device-To-Cloud
device-facing endpoint (/devices/{deviceId}/messages/events)를 사용하여 메세지 전송 및 라우팅 규칙 적용가능, IoT Hub는 Service Bus 보다는 Event Hub와 더 닮아있다. streaming 메세지 패턴을 이용하여 메세지를 전달하며 기본값으로 7일간 메세지를 저장한다. 클라우드로 전송하는 메세지는 최대 256KB까지 전송 가능하며, 몇개의 메세지를 묶어서 함께 전송할 수 도 있다.

Event Hub와의 가장 큰 차이점을 말하자면, IoT Hub는 기기별로 인증을 요구하며 접근 제어가 가능하다. 또한 최대 10개 까지의 custom endpoint를 생성할 수 있다. Event Hub에 비해 동시에 더 많은 디바이스 접속을 허용한다. (Event Hub는 AMQP의 경우 네임스페이스 별로 5000 개가 제한이다.) 또한, 임의로 파티셔닝 하는것을 허용하지 않으며, 스케일링 방식도 약간 다르다.

### Cloud-To-Device
service-facing endpoint (/messages/devicebound)로 메세지를 전송하면, 각 디바이스들은 device-specific endpoint (/devices/{deviceId}/messages/devicebound)를 통해 메세지를 받는다. 

최소 한번 이상의 메세지 전송을 보장하는데 방식은 다음과 같다. 
![image](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/770ab10a5ea89bcb94ebb18dd280b90f/asset-v1:Microsoft+DEV225x+2T2018+type@asset+block/Mod1_CloudToDeviceMessaging.png)

자세한 정보는 다음의 링크에서 참고할 수 있다. 
* [https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-devguide-messaging](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-devguide-messaging)

## Azure IoT Management Tools
* IoTHub-Explorer: CLI Tool, 디바이스 관리 및 등록
* Device Explorer app for IoT Hub devices: 로컬 PC에 설치하여 사용하는 프로그램으로 Azure IoT Hub에서와는 조금 다른 정보들을 보여준다. 이것을 사용해 Device Identity 관리, device to cloud 메세지 받기, cloud to device 즉, device로 메세지 전송 가능
* Azure CLI 2.0 - Azure Resource 관리용 CLI 

## Message and Device Security
IoT 시나리오에서는 다음의 세가지 포인트에서 보안을 고려해야한다. 각각의 IoT Device에서의 Security, Device와 Cloud간의 연결시 보안 관점, 마지막으로 Cloud 상에 데이터가 저장될 때. 각각의 세부사항은 다음과 같다.

### Device Security
Device는 Azure IoT Hub와 통신할때 반드시 Security Token을 이용하거나, 혹은 X.509 인증서를 사용하여 통신해야 한다. 

### Connection Security
TLS를 이용하여 통신한다. (TLS 1.2, 1.1, 1.0 지원) 

### Cloud Security 
각 Security Key 별로 권한 제어가 가능하다. RegistryRead / RegistryReadWrite / ServiceConnect / DeviceConnect 용도별로 권한 제어가 가능하다. 





