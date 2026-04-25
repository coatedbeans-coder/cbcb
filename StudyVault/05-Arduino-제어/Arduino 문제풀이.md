---
source_pdf: Arduino Cookbook_ Recipes to Begin, Expand, and Enhance Your Projects.pdf
part: Chapter 1, 2, 8
keywords: practice, Arduino, servo, stepper, PWM, millis, interrupt
---

# Arduino 제어 문제풀이 (10문항)

#practice #arduino

## Related Concepts
- [[18.Arduino 기초와 구조]]
- [[19.서보 제어 프로그래밍]]
- [[21.타이머와 인터럽트]]
- [[20.PWM과 DC 모터 제어]]
- [[22.I2C와 SPI 통신]]

> [!hint]- 핵심 패턴 (클릭하여 보기)
> | 키워드 | 답 |
> |--------|-----|
> | 서보 라이브러리 | `#include <Servo.h>`, `myServo.write(angle)` |
> | 논블로킹 타이밍 | `millis() - last >= interval` |
> | PWM 핀 (Uno) | 3, 5, 6, 9, 10, 11 |
> | I2C 핀 (Uno) | SDA=A4, SCL=A5 |
> | ISR 규칙 | 짧게, volatile 변수, delay() 금지 |

---

## Q1 - 서보 라이브러리 [recall]
> 서보 모터를 90도로 이동시키는 올바른 코드는? 다음 중 선택하세요.
>
> A) `analogWrite(9, 90);`
> B) `myServo.write(90);`
> C) `digitalWrite(9, 90);`
> D) `myServo.writeMicroseconds(90);`

> [!answer]- 정답 보기
> **B) `myServo.write(90);`**
>
> - A: `analogWrite()`는 PWM(0~255), 서보에 사용 불가 (손상 가능)
> - C: `digitalWrite()`는 HIGH/LOW만 출력
> - D: `writeMicroseconds()`는 펄스폭(μs)을 직접 지정 — 90μs가 아닌 1500μs가 90도
>
> `Servo` 라이브러리의 `write(angle)`이 유일하게 올바른 방법.

---

## Q2 - millis() 논블로킹 [recall]
> 다음 코드에서 버그를 찾아라:
>
> ```cpp
> unsigned long lastTime = 0;
> const long INTERVAL = 500;
>
> void loop() {
>   if (millis() >= lastTime + INTERVAL) {
>     lastTime = millis();
>     doSomething();
>   }
> }
> ```

> [!answer]- 정답 보기
> **버그: millis() 오버플로우 취약**
>
> `millis() >= lastTime + INTERVAL`는 millis()가 약 49.7일 후 0으로 리셋될 때 오류 발생.
>
> **수정:**
> ```cpp
> if (millis() - lastTime >= INTERVAL) {  // 빼기 방식
>   lastTime = millis();
>   doSomething();
> }
> ```
>
> 빼기 방식은 오버플로우 시에도 `unsigned long` 연산으로 안전.

---

## Q3 - ISR 규칙 [recall]
> Arduino에서 인터럽트 서비스 루틴(ISR)에서 금지되는 것 3가지는?

> [!answer]- 정답 보기
> 1. **`delay()` 금지** — ISR 실행 중 타이머 정지됨
> 2. **`Serial.print()` 금지** — 버퍼 접근 충돌 가능
> 3. **긴 처리 로직 금지** — ISR은 최대한 짧게 (플래그만 세우기)
>
> ISR에서 수정하는 변수는 반드시 `volatile` 선언.

---

## Q4 - PWM 핀 확인 [recall]
> Arduino Uno에서 `analogWrite()`(PWM)를 사용할 수 있는 핀 번호를 모두 나열하라.

> [!answer]- 정답 보기
> **핀 3, 5, 6, 9, 10, 11** (총 6개)
>
> 이 핀들은 `~` 기호로 표시되어 있음.
> 나머지 디지털 핀은 `HIGH`/`LOW`만 출력 가능.

---

## Q5 - 다중 서보 타이밍 [application]
> 갤럽 주기 1000ms에서 우뒤다리(0ms 시작)와 우앞다리(500ms 오프셋)를 동시에 논블로킹으로 제어하는 코드 구조를 설명하라.

> [!answer]- 정답 보기
> ```cpp
> unsigned long timer1 = 0;      // 우뒤 타이머
> unsigned long timer2 = 500;    // 우앞 타이머 (500ms 오프셋)
>
> void loop() {
>   unsigned long now = millis();
>
>   // 우뒤 다리
>   if (now - timer1 >= 1000) {
>     servo1.write(UP_ANGLE);
>     timer1 = now;
>   }
>   // 우앞 다리 (500ms 뒤처져 시작)
>   if (now - timer2 >= 1000) {
>     servo3.write(UP_ANGLE);
>     timer2 = now;
>   }
>
>   // 다른 코드도 동시에 실행 가능!
> }
> ```
>
> 핵심: 각 서보마다 독립 타이머 변수 + 초기값으로 오프셋 설정.

---

## Q6 - PCA9685 설정 [recall]
> PCA9685 서보 드라이버를 사용할 때 `setPWMFreq()`에 설정해야 하는 주파수와 그 이유는?

> [!answer]- 정답 보기
> **50 Hz**
>
> 이유: 취미용 서보 모터의 표준 신호 주파수는 50Hz (주기 20ms).
>
> ```cpp
> pwm.setPWMFreq(50);  // 서보용 50Hz 설정
> ```
>
> 50Hz 이외로 설정하면 서보가 오작동 또는 손상될 수 있음.

---

## Q7 - 인터럽트 핀 [recall]
> Arduino Uno에서 외부 인터럽트(`attachInterrupt()`)를 사용할 수 있는 핀은?

> [!answer]- 정답 보기
> **핀 2, 핀 3** (총 2개)
>
> - 핀 2: Interrupt 0
> - 핀 3: Interrupt 1
>
> `digitalPinToInterrupt(2)` 함수로 변환 후 사용 권장:
> ```cpp
> attachInterrupt(digitalPinToInterrupt(2), myISR, FALLING);
> ```

---

## Q8 - 아날로그 입력 변환 [application]
> 포텐시오미터 값(0~1023)을 서보 각도(0°~180°)로 변환하는 코드를 작성하라.

> [!answer]- 정답 보기
> ```cpp
> int potValue = analogRead(A0);           // 0~1023
> int angle = map(potValue, 0, 1023, 0, 180);  // 0~180
> myServo.write(angle);
> ```
>
> `map(value, fromLow, fromHigh, toLow, toHigh)` 함수가 범위 변환을 담당.
> 주의: `map()`은 정수 연산 → 소수점 버림.

---

## Q9 - `volatile` 키워드 [recall]
> ISR에서 사용하는 변수에 `volatile` 키워드가 필요한 이유는?

> [!answer]- 정답 보기
> 컴파일러 최적화 방지가 목적.
>
> 컴파일러는 변수가 예상치 못하게 변경될 것을 모르면, 레지스터에 캐시하거나 코드를 최적화.
> ISR이 해당 변수를 변경해도 메인 코드가 변경사항을 인식 못할 수 있음.
>
> `volatile` 선언 → 컴파일러에게 "이 변수는 외부에서 언제든 바뀔 수 있음" 알림
> → 매번 메모리에서 직접 읽도록 강제.

---

## Q10 - I2C 장치 구별 [analysis]
> 동일한 I2C 버스에 MPU-6050(주소 0x68)과 PCA9685(주소 0x40)를 동시에 연결할 수 있는가? 가능하다면 어떻게 구별하는가?

> [!answer]- 정답 보기
> **✅ 가능하다.**
>
> I2C는 주소 기반 프로토콜 — 같은 SDA/SCL 선에 127개까지 장치 연결 가능.
>
> 각 장치는 고유 주소로 구별:
> ```cpp
> Wire.beginTransmission(0x68); // MPU-6050 선택
> // ... MPU 통신
> Wire.endTransmission();
>
> // PCA9685는 Adafruit_PWMServoDriver(0x40)로 별도 객체
> ```
>
> 주소 충돌 시: 장치의 주소 핀(A0, A1, A2)을 설정해 다른 주소로 변경.

---

> [!summary]- 패턴 요약 (클릭하여 보기)
> | 키워드 | 답 |
> |--------|-----|
> | 서보 제어 | `Servo` 라이브러리, `write(angle)` |
> | 논블로킹 | `millis() - last >= interval` (빼기 방식) |
> | PWM 핀 (Uno) | 3, 5, 6, 9, 10, 11 |
> | 외부 인터럽트 핀 (Uno) | 2, 3 |
> | I2C 구별 | 7비트 주소 (0x40, 0x68 등) |
> | `volatile` | ISR 변수에 필수 |
