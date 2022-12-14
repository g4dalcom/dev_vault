---
keyword : Java, Spring
class : CS
---


### 쿠키와 세션(Cookie & Session)


| 분류     | 쿠키(Cookie)                                                                            | 세션(Session)                                                                                                                                                   |
| -------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 설명     | 클라이언트에 저장될 목적으로 생성한 작은 정보를 담은 파일                               | 서버에서 일정시간 동안 클라이언트 상태를 유지하기 위해 사용                                                                                                     |
| 저장위치 | 클라이언트 (웹 브라우저)                                                                | 웹서버                                                                                                                                                          |
| 사용 예  | 사이트 팝업의 "오늘 다시보지 않기" 정보 저장                                            | 로그인 정보 저장                                                                                                                                                |
| 만료시점 | 쿠키 저장 시 만료일시 설정 가능 (브라우저 종료시도 유지 가능)                           | 다음 조건 중 하나가 만족될 경우 만료됨 1. 브라우져 종료 시까지 2. 클라이언트 로그아웃 시까지 3. 서버에 설정한 유지기간까지 해당 클라이언트의 재요청이 없는 경우 |
| 용량제한 | 브라우져 별로 다름 (크롬 기준) - 하나의 도메인 당 180개 - 하나의 쿠키 당 4KB(=4096byte) | 개수 제한 없음 (단, 세션 저장소 크기 이상 저장 불가능)                                                                                                          |
| 보안     | 취약 (클라이언트에서 쿠키 정보를 쉽게 변경, 삭제 및 가로채기 당할 수 있음)              | 비교적 안전 (서버에 저장되기 때문에 상대적으로 안전)                                                                                                            |
