# Journal Mate

웹페이지와 논문 PDF를 요약·번역하고 문서 비교까지 지원하는 Chrome Side Panel 기반 연구 보조 확장 프로그램입니다.

## Overview
- 웹/논문 텍스트 추출 -> 요약/번역 -> 비교 분석까지 브라우저 내에서 처리
- 스트리밍 출력으로 결과를 실시간 확인
- 요약 길이 선택 지원(짧게/보통/길게)

## ScreenShots

| URL | PDF | PDF |
|----------|----------|----------|
| <img src="https://github.com/user-attachments/assets/4f741913-b444-4723-b09d-373b69fc6665" width="100%"> | <img src="https://github.com/user-attachments/assets/010aedc8-99ba-449b-a345-2dfe34351aa7" width="100%"> | <img src="https://github.com/user-attachments/assets/1c595029-1da6-4000-aad5-6ef47b01a08e" width="100%"> ||

| Full Page View |
|----------|
| <img src="https://github.com/user-attachments/assets/8b8d269d-642f-4b6b-8bcc-ef9fb59a2ff9" width="100%"> |





## Core Features
- 현재 탭 웹페이지 본문 요약/번역
- 다중 PDF 업로드 후 문서별 요약/번역
- 여러 문서 공통점/차이점 비교 분석

## Multi-Agent Design (3 Agents)
 
| Agent | 역할 | 산출물 |
|---|---|---|
| Summarizer Agent | 문서 핵심 내용을 구조화해 요약 | 초안 요약 |
| Translator Agent | 요약 결과 번역 및 표현 정리 | 번역 요약 |
| Verifier Agent | 사실/논리/문체 검증 및 수정 피드백 | 검증 완료 결과 |

### Collaboration Loop
1. Summarizer가 초안 생성
2. Translator가 번역/표현 보정
3. Verifier가 검증/수정
4. 필요 시 재생성 후 최종 확정

## Extension Structure
<img src="https://github.com/user-attachments/assets/b1e273b6-9487-4e4b-adc6-80175e877e21" alt="Extension Structure" width="100%" />

## System Architecture
<img src="https://github.com/user-attachments/assets/c5fe4f82-f10a-43ec-b13a-11c155c5e743" alt="System Architecture 1" width="100%" />
<img src="https://github.com/user-attachments/assets/c69769b6-089b-4d20-aba5-b0a8432c3a86" alt="System Architecture 2" width="100%" />


## Model Selection
| 모델 | 품질 | 속도 | 비용 효율 | 권장 영역 |
|---|---|---|---|---|
| `gpt-4o` | 매우 높음 | 상대적으로 느림 | 상대적으로 높음 | 정밀 비교/고난도 분석 |
| `gpt-4o-mini` | 높음 | 빠름 | 높음 | 기본 요약/번역, 실시간 응답 |
| 경량/구세대 GPT 계열 | 보통 | 빠름 | 매우 높음 | 단순 저비용 작업 |

### Why `gpt-4o-mini`
- 스트리밍 UX에 유리한 응답 속도
- 반복 요청(요약/번역)에 적합한 비용 효율
- 한국어 품질이 실사용 수준으로 안정적
- Verifier Agent 결합으로 품질 리스크 완화 가능
