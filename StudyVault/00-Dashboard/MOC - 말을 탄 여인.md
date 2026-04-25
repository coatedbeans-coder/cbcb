---
source_pdf:
  - Alan Hendrickson - Mechanical Design for the Stage (2007) - libgen.li.pdf
  - Arduino Cookbook_ Recipes to Begin, Expand, and Enhance Your Projects.pdf
  - Dustyn Roberts - Making Things Move DIY Mechanisms for Inventors, Hobbyists, and Artists (2010, McGraw-Hill_TAB Electronics) - libgen.li.pdf
  - Gordon McComb, Myke Predko - Robot Builder's Bonanza (2006, McGraw-Hill_TAB Electronics) [10.1036_0071468935] - libgen.li.pdf
  - Henry T. Brown - 507 Mechanical Movements. Mechanisms and Devices (2012, INscribe Digital_Dover Publications) - libgen.li.pdf
  - Simon Monk - Programming Arduino Next Steps_ Going Further with Sketches (2016, McGraw-Hill Education) - libgen.li.pdf
  - W. Bolton - Mechatronics_ Electronic Control Systems in Mechanical and Electrical Engineering (2018, Pearson Education) - libgen.li.pdf
part: all
keywords: MOC, study map, mechatronics art, horse rider, woman riding horse
---

# 🐎 말을 탄 여인 — 메카트로닉스 아트 스터디 맵

#dashboard #project #mechatronics

> [!important] 프로젝트 목표
> **말을 탄 여인(Woman Riding a Horse)** 메카트로닉스 아트 작품 제작
> 핵심 과제: 말의 갤럽 운동 + 라이더 상체 움직임을 Arduino로 제어

---

## 🗺️ 프로젝트 구조도 *(개념도 — 실제 구동체 수는 설계 단계에서 확정)*

```
[전원] → [Arduino 제어보드]
              ↓
      ┌───────┼───────┐
   [모터A]  [모터B]  [모터C]
      ↓        ↓        ↓
  [앞다리  [뒷다리  [라이더
   크랭크]  캠]     서보]
      └───────┴───────┘
              ↓
        말+라이더 프레임
```

---

## 📚 Topic Map

| 섹션              | 출처                                                                  | 개념 노트                                                                                              | 상태  |
| --------------- | ------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- | --- |
| 기구학 — 크랭크·캠·링키지 | Making Things Move Ch.8                                             | [[1.기본 기계요소 6가지]], [[2.크랭크와 왕복운동]], [[3.캠과 팔로워]], [[4.4절 링크장치]]                                            | [ ] |
| 기어와 동력전달        | Making Things Move Ch.1, Mechatronics Ch.8                          | [[5.기어와 동력전달]], [[6.507 운동 레퍼런스]]                                                                      | [ ] |
| 운동역학 — 힘·토크·마찰  | Making Things Move Ch.4, Hendrickson Part I                         | [[7.힘과 토크]], [[8.속도와 가속도]], [[9.마찰과 베어링]], [[10.무대기계 운동 원리]]                                                | [ ] |
| 구조·재료           | Making Things Move Ch.2-3, Robot Bonanza Ch.3                       | [[11.재료 선택과 특성]], [[12.체결과 접합]], [[13.프레임 설계]]                                                              | [ ] |
| 액추에이터·모터        | Making Things Move Ch.6, Arduino Cookbook Ch.8, Mechatronics Ch.7-8 | [[14.DC 모터]], [[15.서보 모터]], [[16.스테퍼 모터]], [[17.모터 선택 가이드]]                                                    | [ ] |
| Arduino 제어      | Arduino Cookbook Ch.8, Arduino Next Steps                           | [[18.Arduino 기초와 구조]], [[19.서보 제어 프로그래밍]], [[16.스테퍼 모터]], [[20.PWM과 DC 모터 제어]], [[21.타이머와 인터럽트]], [[22.I2C와 SPI 통신]] | [ ] |
| 센서·신호처리         | Mechatronics Ch.2-4, Arduino Cookbook Ch.6                          | [[23.센서 종류와 선택]], [[24.신호 조정]]                                                                           | [ ] |
| 전원·전자회로         | Making Things Move Ch.5, Robot Bonanza Ch.2                         | [[25.전원 시스템과 배터리]], [[26.모터 드라이버와 H-Bridge]]                                                             | [ ] |
| 프로젝트 설계         | 통합                                                                  | [[말을탄여인 프로젝트 개요]], [[말 갤럽 메커니즘 설계]], [[라이더 동작 설계]], [[제어 시퀀스 설계]], [[부품 목록 BOM]]                   | [ ] |

---

## 📝 문제풀이 세트

| 문제셋 | 문항 수 | 링크 |
|--------|---------|------|
| 기구학 | 8문항 | [[기구학 문제풀이]] |
| 운동역학 | 8문항 | [[운동역학 문제풀이]] |
| 구조·재료 | 8문항 | [[구조-재료 문제풀이]] |
| 액추에이터·모터 | 8문항 | [[액추에이터 문제풀이]] |
| Arduino 제어 | 10문항 | [[Arduino 문제풀이]] |
| 센서·신호처리 | 8문항 | [[센서 문제풀이]] |
| 전원·전자 | 8문항 | [[전원-전자 문제풀이]] |

---

## 🛠️ Study Tools

| 도구 | 설명 | 링크 |
|------|------|------|
| 설계 함정 | 초보자가 자주 실수하는 설계 포인트 | [[설계 함정]] |
| 빠른 참조 | 공식·단위·핵심 코드 치트시트 | [[빠른 참조]] |

---

## 🏷️ Tag Index

| Tag | 관련 주제 | 규칙 |
|-----|-----------|------|
| `#mechanism` | 기구학 전체 | 상위 태그 |
| `#linkage` | 4절 링크, 크랭크-슬라이더 | `#mechanism` 와 함께 |
| `#cam` | 캠, 팔로워 | `#mechanism` 와 함께 |
| `#gear` | 기어, 체인, 벨트 | `#mechanism` 와 함께 |
| `#dynamics` | 힘, 토크, 가속도 | 상위 태그 |
| `#torque` | 토크 계산 | `#dynamics` 와 함께 |
| `#materials` | 재료 선택 | 상위 태그 |
| `#structure` | 프레임, 구조 설계 | `#materials` 와 함께 |
| `#fastener` | 체결·접합 | `#materials` 와 함께 |
| `#motor` | 모터 전체 | 상위 태그 |
| `#motor-dc` | DC 모터 | `#motor` 와 함께 |
| `#motor-servo` | 서보 모터 | `#motor` 와 함께 |
| `#motor-stepper` | 스테퍼 모터 | `#motor` 와 함께 |
| `#arduino` | Arduino 프로그래밍 | 상위 태그 |
| `#control` | 제어 시스템 | `#arduino` 와 함께 |
| `#sensor` | 센서 | 상위 태그 |
| `#signal` | 신호 처리 | `#sensor` 와 함께 |
| `#power` | 전원 | 상위 태그 |
| `#project` | 프로젝트 전용 노트 | 단독 사용 |
| `#dashboard` | 대시보드 | 단독 사용 |
| `#practice` | 문제풀이 | 단독 사용 |
| `#exam-traps` | 함정 노트 | `#dashboard` 와 함께 |

> **태그 규칙**: 세부 태그 사용 시 반드시 상위 도메인 태그를 함께 부착. 예: `#cam #mechanism`

---

## ⚠️ 취약 영역

- [ ] 말 갤럽 보행 패턴의 타이밍 → [[말 갤럽 메커니즘 설계]] → [[설계 함정]]
- [ ] 토크 계산 및 모터 사이징 → [[7.힘과 토크]] → [[17.모터 선택 가이드]]
- [ ] 서보 vs 스테퍼 선택 기준 → [[17.모터 선택 가이드]] → [[설계 함정]]
- [ ] PWM 신호 vs 서보 라이브러리 차이 → [[19.서보 제어 프로그래밍]] → [[설계 함정]]
- [ ] 구조 하중 계산 → [[7.힘과 토크]] → [[13.프레임 설계]]

---

## 🚫 Non-core Topic Policy

| 출처 | 내용 | 처리 방침 |
|------|------|-----------|
| Arduino Cookbook Ch.9 | 오디오 출력 | **제외** — 이 프로젝트에 불필요 |
| Arduino Cookbook Ch.14-15 | WiFi/Ethernet/IoT | **필요 시 참조** — 전시 원격 모니터링·긴급 정지 구현 시 유용 |
| Arduino Cookbook Ch.10 | 원격 IR 제어 | **참고 수준** — 리모컨 추가 시 활용 |
| Robot Bonanza | 로봇 자율주행, 휠 로코모션 | **제외** — 고정 아트 작품 |
| Mechatronics Ch.7 | 공압·유압 시스템 | **제외** — 전기 액추에이터만 사용 |
| 507 Mechanical Movements | 전체 507가지 중 | **선별 참조** — 갤럽/왕복 관련 운동만 |
