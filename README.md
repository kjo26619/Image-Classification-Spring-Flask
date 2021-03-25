# Image-Classification-Spring-Flask

 Image classification TOY project using Java Spring Web, Python Flask REST API and Docker Compose.
 
## Requirements

 - JAVA : Openjdk-11
 - Maven
 - Docker
 - Docker Compose

## Architecture

전체 구조는 다음과 같다.

![imageArch](https://github.com/kjo26619/Image-Classification-Spring-Flask/blob/main/img/toy_arch.png)

Spring boot를 이용해서 Web을 구성한다.

분류할 이미지를 선택하면 Spring이 받아서 Flask로 재전송한다.

Flask에서 Pytorch 중 Imagenet으로 학습한 MobileNet V2 모델을 가지고 와서 분류한다.

분류한 결과는 Top 3 확률이 JSON으로 반환되며, Spring은 Flask에게 받은 JSON으로 View를 구성한다.
 
## Maven Build
 
 처음 Spring이 있는 ImageClassification 디렉토리로 들어가서 Maven Build를 진행한다.
 
 ```
 # mvn clean pacakge
 ```
 
 ![image1](https://github.com/kjo26619/Image-Classification-Spring-Flask/blob/main/img/toy1.PNG)

 Maven이 ImageClassification/target에 web-0.0.1-SNAPSHOT.jar를 만들어내면 된다.

## Docker compse up

```
# docker-compose up
```

docker-compose.yaml 파일이 있는 곳에서 docker-compose up을 실행하면 Spring과 Flask가 구동된다.

Image를 Build해서 Local Repository에 저장한다. Flask를 구성 중에 Pytorch가 높은 메모리를 차지하므로 주의할 것

( Spring Image : 695MB, Flask Image : 2.49GB )

Build 완료 시 Spring이 구동되는 것을 확인할 수 있다.

![image2](https://github.com/kjo26619/Image-Classification-Spring-Flask/blob/main/img/toy2.PNG)

# Result

localhost:8082/ 로 접속하면 된다.

![image3](https://github.com/kjo26619/Image-Classification-Spring-Flask/blob/main/img/toy3.PNG)

원하는 Image를 선택한 후 [제출] 버튼을 누른다.

제출하면 머신 러닝 학습이 끝난 뒤 결과를 반환해준다.

![image4](https://github.com/kjo26619/Image-Classification-Spring-Flask/blob/main/img/toy4.PNG)

결과는 Imagenet을 토대로 분류된다.

# Reference

- Imagenet : http://www.image-net.org/
- Pytorch MobileNet V2 : https://pytorch.org/hub/pytorch_vision_mobilenet_v2/
- Spring with Docker : https://spring.io/guides/gs/spring-boot-docker/
- Python with Docker : https://docs.docker.com/language/python/build-images/
- Maven build : https://sarc.io/index.php/cloud/1856-spring-boot-docker
- Wallaby Image : https://ko.wikipedia.org/wiki/%EB%B6%89%EC%9D%80%EB%AA%A9%EC%99%88%EB%9D%BC%EB%B9%84
