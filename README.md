<div align="center">
<img src="https://img.shields.io/badge/-Arduino-00979D?style=for-the-badge&logo=Arduino&logoColor=white">
</div>

---
### 08-27(화)
아두이노 서보모터 제어 세부코드 내용

```C++
#include <Servo.h>

int servoLRpin = 9, servoUDpin = 10;
Servo servoLR, servoUD;
int LEDpin_1 = 11, LEDpin_2 = 12, LEDpin_3 = 15, LEDpin_4 = 16;

void setup() {
  Serial.begin(9600);
  servoLR.attach(servoLRpin);
  servoUD.attach(servoUDpin);
  servoLR.write(90); // 서보 초기 위치 설정
  servoUD.write(90); // 서보 초기 위치 설정
  pinMode(LEDpin_1, OUTPUT);
  pinMode(LEDpin_2, OUTPUT);
  pinMode(LEDpin_3, OUTPUT);
  pinMode(LEDpin_4, OUTPUT);
  digitalWrite(LEDpin_1, LOW); // LED1를 끈 상태로 초기화
  digitalWrite(LEDpin_2, LOW); // LED2를 끈 상태로 초기화
  digitalWrite(LEDpin_3, LOW); // LED3를 끈 상태로 초기화
  digitalWrite(LEDpin_4, LOW); // LED4를 끈 상태로 초기화
}

void loop() {
  if (Serial.available() > 0) {
    char command = Serial.read(); // 명령어를 읽어옴
    Serial.println(command);
    switch (command) {
      case '1': // 서보를 좌우 리셋
        servoLR.write(90);
        break;
      case '2': // 서보를 위아래 리셋
        servoUD.write(90);
        break;
      case 'L': // 서보를 왼쪽으로 20 이동
        servoLR.write(max(0, servoLR.read() - 20));
        break;
      case 'R': // 서보를 오른쪽으로 이동
        servoLR.write(min(180, servoLR.read() + 20));
        break;
      case 'U': // 서보를 위쪽으로 이동
        servoUD.write(max(40, servoUD.read() - 20));
        break;
      case 'D': // 서보를 아래쪽으로 이동
        servoUD.write(min(130, servoUD.read() + 20));
        break;
      case 'a': // LED1을 켠다
        digitalWrite(LEDpin_1, HIGH);
        break;
      case 'b': // LED1을 끔
        digitalWrite(LEDpin_1, LOW);
        break;
      case 'c': // LED2을 켠다
        digitalWrite(LEDpin_2, HIGH);
        break;
      case 'd': // LED2를 끔
        digitalWrite(LEDpin_2, LOW);
        break;
      case 'e': // LED3를 켠다
        digitalWrite(LEDpin_3, HIGH);
        break;
      case 'f': // LED3를 끔
        digitalWrite(LEDpin_3, LOW);
        break;
      case 'g': // LED4를 켠다
        digitalWrite(LEDpin_4, HIGH);
        break;
      case 'h': // LED4를 끔
        digitalWrite(LEDpin_4, LOW);
        break;
    }
  }
}

```
