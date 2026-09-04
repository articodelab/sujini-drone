# 7인치 자율비행 대드론(요격) 레이싱드론 - 부품 리스트 및 견적 (고사양)

> ⚠️ **법적/안전 주의사항**: 타 비행체를 자동으로 요격(충돌)하는 시스템은 다수 국가에서 항공법·전파법·방위사업법상 규제 대상입니다. 실제 운용 전 관할 기관(국토부, 국방부, 방사청 등)의 허가/승인 여부를 반드시 확인하세요. 아래 부품 구성은 하드웨어 플랫폼 제작을 위한 참고용이며, **최종 충돌/요격 판단은 사람이 승인하는 Human-in-the-loop 구조**를 권장합니다.

## 컨셉
- **기체**: 7인치 프레임, 고출력/고속 FPV 레이싱 플랫폼
- **자율비행 스택**: PX4 (Flight Controller) + ROS2 (Companion Computer)
- **시뮬레이션**: PX4 HITL ↔ NVIDIA Isaac Sim (실기체 투입 전 표적 추적/접근 로직 검증)
- **컴패니언 컴퓨터**: NVIDIA Jetson Orin Nano (비전 인식/표적 추적, 접근 기동 유도)
- **목표**: 적 드론을 탐지·추적하여 고속으로 접근, **사람 승인 후** 충돌 요격
- **등급**: 고사양 (내구성·속도·페이로드 우선, 비용 高)

---

## 1. 프레임 (Frame)
| 항목 | 추천 제품 | 예상 단가 (KRW) | 비고 |
|---|---|---|---|
| 7인치 레이싱 프레임 | Armattan Rooster 7" / TBS Source One V5 7" | 180,000 ~ 250,000 | 카본 3K, Jetson 탑재 공간 확보된 스택형 |
| 프레임 보강 플레이트 | 알루미늄 스탠드오프 세트 | 20,000 | 진동 저감, 페이로드 마운트용 |

## 2. 동력계 (Propulsion)
| 항목 | 추천 제품 | 예상 단가 (KRW) | 비고 |
|---|---|---|---|
| 모터 (4개) | T-Motor F90 Pro 1750KV or iFlight XING2 2812 | 280,000 (4개 합) | 고속·고토크, 6S 대응 |
| ESC (4in1) | T-Motor F55A Pro II 4in1 60A | 150,000 | 6S 지원, BLHeli32 |
| 프로펠러 (예비 포함 3세트) | HQProp 7x4x3 or Gemfan 7042 | 45,000 | 고속형 |

## 3. 비행 컨트롤러 & 센서 (FC/Sensors)
| 항목 | 확정 제품 | 예상 단가 (KRW) | 비고 |
|---|---|---|---|
| Flight Controller | **Holybro Kakute H7 v1.5** | 130,000 | PX4 공식 지원(`make holybro_kakuteh7_default`), STM32H743, IMU: MPU6000, HITL 시뮬레이션과 동일 펌웨어 사용. **내장 마그네토미터 없음** → 외장 컴퍼스 필수 |
| ESC (4in1) | **Tekko32 F4 Metal 4in1 65A** | 120,000 | PX4 문서상 Kakute H7 공식 권장 페어링 ESC, BLHeli32/DShot, ESC 텔레메트리(UART7) 지원 |
| GPS/나침반 모듈 (외장 필수) | Holybro M9N/M10 GPS w/ Compass | 90,000 | Kakute H7에 마그네토미터가 없어 완전자율(GPS 웨이포인트) 비행을 위해 필수. UART4(GPS1)에 연결 |
| 텔레메트리 (FC↔GCS) | Holybro 900MHz Telemetry Radio | 90,000 | TELEM1(UART1) 연결, 장거리 통신 |
| Optical Flow + 거리 센서 | Holybro PM07/거리 라이다 (TF-Luna 등) | 60,000 | 저고도 안정화 보조, GPS 신호 저하 구간(교량 하부 등) 대비 |

## 4. 컴패니언 컴퓨터 & 비전 (Autonomy)
| 항목 | 추천 제품 | 예상 단가 (KRW) | 비고 |
|---|---|---|---|
| 컴패니언 컴퓨터 | NVIDIA Jetson Orin Nano Super (8GB) | 350,000 | ROS2 + PX4 오프보드 제어, 표적(적 드론) 인식 |
| 캐리어 보드 (경량화) | Jetson Orin Nano 전용 소형 캐리어보드 (Seeed reComputer 등) | 200,000 | 항공기용 경량 설계 |
| 비전 센서 | Intel RealSense D435i (뎁스) or 글로벌셔터 카메라(OAK-D Lite) | 300,000 | 표적 탐지/추적, VIO 보조 |
| FC-Orin 통신 | FTDI/UART 케이블, MAVLink 브릿지 | 10,000 | MAVROS2 연동 |
| 방열/쿨링 | 소형 히트싱크+블로워팬 | 30,000 | 비행 중 발열 대응 |

## 5. FPV 영상 시스템
| 항목 | 추천 제품 | 예상 단가 (KRW) | 비고 |
|---|---|---|---|
| 디지털 FPV 시스템 | DJI O3 Air Unit + Goggles 2 | 550,000 | 조종사 모니터링/백업 수동조작용 |
| FPV 카메라(백업 아날로그) | Foxeer Razer Nano | 40,000 | 신호 이중화 |

## 6. 배터리 & 전원
| 항목 | 추천 제품 | 예상 단가 (KRW) | 비고 |
|---|---|---|---|
| 리포 배터리 (2개) | Tattu 6S 1800mAh 130C | 130,000 (2개) | 고속/고부하 대응 |
| 배터리 충전기 | ISDT Q8 / SkyRC | 180,000 | 다중 셀 급속 충전 |
| Jetson 전용 전원 모듈 | 별도 5V/5A급 UBEC (Matek 5V/6A 등) | 45,000 | Kakute H7 내장 BEC(5V 2A)는 용량 부족 → Jetson Orin Nano는 배터리 직결 별도 UBEC 권장 |

## 7. 통신/조종
| 항목 | 추천 제품 | 예상 단가 (KRW) | 비고 |
|---|---|---|---|
| RC 송수신기 | TBS Crossfire / ExpressLRS 2.4GHz | 120,000 | 장거리·저지연 |
| 조종기 | RadioMaster TX16S | 350,000 | 다중 스위치, 페일세이프 설정 |

## 8. 예비 부품 & 공구
| 항목 | 예상 단가 (KRW) |
|---|---|
| 예비 모터/ESC/프롭 | 150,000 |
| 납땜/조립 공구 세트 | 100,000 |
| 진동 감쇠 마운트(Jetson/카메라용) | 30,000 |

---

## 총 예상 견적 (1대 기준)

| 구분 | 금액 (KRW) |
|---|---|
| 프레임 | 270,000 |
| 동력계 | 475,000 |
| FC/센서 (Kakute H7 + Tekko32) | 490,000 |
| 컴패니언 컴퓨터/비전 | 890,000 |
| FPV | 590,000 |
| 배터리/전원 | 355,000 |
| 통신/조종 | 470,000 |
| 예비품/공구 | 280,000 |
| **합계** | **약 3,820,000원** |

> 가격은 2025년 기준 국내 리테일 평균가 참고치이며, 환율/재고/수입 여부에 따라 변동될 수 있습니다. 조종기(TX16S)와 충전기는 여러 대 제작 시 1회성 투자로 재사용 가능합니다.

## PX4 HITL ↔ Isaac Sim 연동 워크플로우
1. **펌웨어**: Kakute H7 v1.5에 Betaflight 부트로더 제거 후 PX4 부트로더 플래싱 → `make holybro_kakuteh7_default` 빌드/업로드 (Betaflight 출고 상태이므로 최초 1회 부트로더 교체 필요)
2. **HITL 모드**: PX4 `SYS_HITL=1` 설정, FC를 USB로 Isaac Sim 호스트 PC에 연결
3. **Isaac Sim**: PX4 HITL 플러그인(Isaac Sim PX4 Bridge)으로 가상 표적 드론 시나리오 구성, IMU/GPS/카메라 센서 데이터를 FC로 스트리밍
4. **검증 항목**: 표적 탐지·추적 정확도, 고속 접근 기동 시 자세 안정성, 오탐(false positive) 대응 로직을 시뮬레이션에서 먼저 검증 후 동일 파라미터를 실기체에 이식
5. **실기체 전환 시 주의**: HITL은 FC 내부 센서(IMU) 대신 시뮬레이션 값을 사용하므로, 실기체에서는 **외장 GPS+컴퍼스 캘리브레이션을 반드시 재수행**

## 다음 단계 제안
1. **PX4 파라미터/믹서 설정** — Kakute H7 UART 매핑(GPS1=UART4, TELEM1=UART1, ESC 텔레메트리=UART7) 확정, 6S 고속 모터 튜닝, 페일세이프 정책
2. **PX4 HITL + Isaac Sim 환경 구축** — 가상 표적 드론 시나리오 제작, 접근/요격 미션 스크립트 작성
3. **ROS2 + MAVROS2 연동 아키텍처** — Jetson ↔ FC 오프보드 제어 흐름 설계
4. **비전 기반 표적 추적 파이프라인** — 탐지(YOLO 등) → 추적 → **사람 승인 후** 접근 기동(반자율 구조)
5. **배선도(Wiring Diagram) 작성** — Kakute H7 ↔ Tekko32 4in1 ↔ Jetson Orin Nano ↔ GPS/컴퍼스 연결도
