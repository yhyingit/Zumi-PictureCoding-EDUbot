# ZUMI PictureCoding EDUbot
---
[TeamAlphaZUMI]

한양대학교 ERICA 로봇공학과 박병우, 유호연, 이영준 

# 개요

---

한양대학교 ERICA 로봇공학과 로봇프로그래밍 수업의 일환으로 제작되었습니다. 

ZUMI는 Robolink사의 제품으로 이를 활용하여 ROS 패키지 제작 프로젝트를 진행하였습니다.

인공지능과 프로그래밍 교육이라는 기능을 확장하기 위해 Picture Coding을 활용하여 ZUMI의 사용 연령층을 확장시켰습니다.

Picture Coding은 그림 카드를 ZUMI에게 보여줌으로 로봇의 행동을 프로그래밍처럼 제어할 수 있는 기능입니다.

ZUMI는 각 그림 카드를 인식한 후 사용자에게 자신이 인식했다는 사실을 상호작용을 통하여 전달합니다.

# 하드웨어 개발환경

---

## ZUMI

---

- 아두이노 UNO
- RaspberryPi Zero W
- DC 모터 2개
- IR 6개
- LED 2개
- PiCam
- 디스플레이 Adafruit ssd1306

# 소프트웨어 개발환경

---

## Computer

---

- Ubuntu 18.04 Bionic
- ROS Melodic Morenia
- Arduino 1.8.10
- OpenCV 3.4.0
- Python 2.7
- Keras 2.2.4
- Theano 1.0.4
- Tensorflow 1.13.1

## ZUMI

---

- Raspbian Jessie (debian 8)
- ROS Kinetic Kame

# ROS 의존파일

---

- CV_bridge
- ros_serial

# 설치 및 사용 방법

---

## 설치

github의 Repo를 복사하여 사용합니다.

    git clone https://github.com/yhyingit/Zumi-PictureCoding-EDUbot.git
    
## 사용법

ZUMI에서 카메라 켜기

    rosrun Zumicam Zumicam.py

서버PC에서 영상 받은 후 차선 검출 결과 표현

    rosrun asdf asdf.py
    

# 기능

---

이 시스템은 PC와 ZUMI의 이 기종 통신으로 작동합니다.

### 1. PictureCoding

- Coding 카드를 ZUMI에게 보여줌으로 카드를 인식시킵니다.
- CNN 활용하여 PictureCoding 카드를 인식하는 알고리즘을 가집니다..
- '시작' 카드를 인식시켜 코딩 단계에 돌입하며 '끝' 카드로 코딩단계를 종료합니다.
- 코딩 단계에서 사용자와 ZUMI와 상호작용을 통해 카드 인식상태를 확인할 수 있습니다.

### 2. 자율 주행 기능

- ZUMI에 탑재된 PiCam을 활용하여 차선을 검출합니다.
- 검출된 차선을 인식하여 도로 주행합니다.
- PictureCoding에서 프로그래밍한 방식으로 맵에서 자율적으로 주행합니다.

### 3. ZUMI 표정 표현

- Adafruit SSD1306 디스플레이를 활용하여 ZUMI의 표정을 표현합니다.
- 인식된 카드의 모양을 디스플레이에 표현합니다.
- 인식된 카드 모양을 화면에 표현한 후 상황에 맞는 표정 및 움직임을 표현합니다.

[ ZUMI디스플레이 표현](https://www.notion.so/50861e024bcd44c2af302d7f1b26876c)

[ZUMI 감정 표현](https://www.notion.so/98cd471a58834eaf897d699f9848e860)


### 4. GAZEBO MAP

- Gazebo map editor를 활용하여 제작되었습니다.
- 조합하여 맵을 확장할 수 있습니다.

### 5. ZUMI URDF

- 솔리드웍스를 사용하여 ZUMI를 구현합니다.
- 모델을 활용하여 GAZEBO 환경에서 시뮬레이션합니다.

### Card

- "좌로 이동", "우로 이동"은 ZUMI의 구조와 물리적 특징 상 이동 불가 하기 때문에 이와 같은 카드들을 인식하면 의문을 갖는 표정을 띄웁니다.
- "시작"카드를 보여주며 프로그래밍의 시작을 인식시킵니다.
- "직진"과 "후진"카드를 보여주어 인식이 되는 경우 맵의 처음 교차로부터 다음 교차로 까지 한 블럭을 이동합니다.
- "시계방향으로 90도 회전"과 "반시계방향으로 90도 회전" 카드는 ZUMI를 90도 만큼 회전시킵니다.
- "시작"카드는 프로그래밍이 시작한다는 것을 알려주는 카드 입니다.
- "끝"카드는 프로그래밍을 끝남을 알려주는 카드입니다.
- "하트"카드는 좌우로 움직이며 ZUMI가 애교를 부리는 행동입니다.
- "아니"카드는 직전에 인식시킨 프로그래밍을 취소할 때 사용하는 카드입니다.
- "뮤직"카드를 보여주면 ZUMI가 두 바퀴를 회전하면서 LED를 깜빡거리고 부저를 작동시킵니다.
- "일반적 표정"은 ZUMI의 일반적인 표정을 나타냅니다.
- "웃는 표정"은 ZUMI가 정상적인 인식을 할 경우와 프로그램이 시작할 때 짓는 표정입니다.



# Node

## PC

LineDetect : /video 토픽으로부터 이미지를 영상 정보를 선 검출을 한 뒤, 검출된 라인의 정보를 영상으로 표현합니다.

## ZUMI

video_pub :  영상정보인 /video 토픽을 퍼블리시합니다.

img_sub : /video 토픽을 서브스크라이브하여 영상을 출력합니다.

# Topic

/video : 영상이미지입니다.

# 참고

ZUMI : [https://www.robolink.com/zumi/](https://www.robolink.com/zumi/)

PictureCoding 학습 CNN Model : [https://github.com/asingh33/CNNGestureRecognizer](https://github.com/asingh33/CNNGestureRecognizer)

LineDetection : [https://github.com/windowsub0406/SelfDrivingCarND](https://github.com/windowsub0406/SelfDrivingCarND)
