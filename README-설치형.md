# 더샵 송도그란테르 G5 옵션몰 — 설치형 (온라인 키오스크)

웹버전(`claude/gifted-brahmagupta-accsi0` 브랜치)과 별도로, **실제 이미지를 로컬 번들**해서 키오스크에 설치하는 버전이다.

- 진입: `index.html` (레포 루트) — 정적 서버로 서빙하거나 브라우저로 바로 열기
- 네트워크: 온라인 키오스크 기준 — VR(XROO)·폰트(Pretendard CDN)는 인터넷 사용, **이미지는 로컬 번들**
- 데이터·옵션·견적 로직은 웹버전과 동일

---

## 이미지 넣는 위치 (파일만 넣으면 자동 표시, 없으면 플레이스홀더)

### 1) 평면도 — `assets/plans/`
- 타입별: `assets/plans/<타입>.png` (예: `assets/plans/118K.png`, `assets/plans/84B.png`)
- 공통 샘플: `assets/plans/_sample.png` (타입별 파일이 없을 때 대체)
- 표시 위치: 분양 고유번호 조회 결과 카드

### 2) 옵션 결과 이미지 — `assets/options/<그룹키>/<옵션id>.jpg`
- 썸네일 타입에서 각 옵션 그룹 하단에 "선택 옵션 이미지"로 표시(선택 변경 시 이미지 교체)
- 그룹키 / 옵션id 매핑:

| 그룹 | 그룹키(폴더) | 옵션 id(파일명) |
|------|-------------|----------------|
| 시스템에어컨 | `aircon` | `no`(미선택) `std`(일반형) `prm`(고급형) |
| 바닥마감 | `floor` | `no` `gw`(광폭강마루) `wd`(원목마루) |
| 프리미엄리빙 | `living` | `no` `sel` |
| 프리미엄키친 | `kitchen` | `no` `sel` |
| 현관 중문 | `door` | `no` `m`(수동) `a`(자동) |
| 프리미엄바스(욕실1) | `bath1` | `no` `sel` |
| 프리미엄바스(욕실2) | `bath2` | `no` `sel` |
| 스마트 감성조명 | `lighting` | `no` `sel` |
| 전동커튼 | `curtain` | `no` `sel` |
| 에코세이버 | `eco` | `no` `std` `prm` |
| 욕실복합환풍기 | `bathfan` | `no` `1` `2` `3` |
| 인덕션 3구 | `induction` | `no` `s`(삼성) `l`(LG) |
| 전기오븐 | `oven` | `no` `s` `l` |
| 키친핏 냉장고 | `kitchenfit` | `no` `s` `l` |
| 식기세척기 | `dishwasher` | `no` `s` `l` |

예) 바닥 원목마루 이미지 → `assets/options/floor/wd.jpg`
- 권장: 16:10 비율, 가로 1200–1600px, JPG

### 3) 가이드 — `assets/guide/`
- 영상 썸네일: `assets/guide/video.jpg` (16:9)
- 이미지: `assets/guide/img-1.jpg`, `assets/guide/img-2.jpg` (16:10)

### 4) 로고 (이미 포함)
- `assets/logo-thesharp-dark.png` (헤더), `assets/logo-thesharp.png` (예비)

---

## 실행
- 간단 확인: `index.html`을 브라우저로 열기(이미지 상대경로 로드)
- 키오스크 서빙: 아무 정적 서버 (예: `python3 -m http.server`) 로 루트를 서빙 후 전체화면(kiosk mode)

## 이미지 제공 방법
- 위 구조대로 파일을 이 브랜치에 커밋(또는 zip으로 전달)하면 반영한다.
- 파일이 없는 슬롯은 자동으로 플레이스홀더가 표시되어 레이아웃은 유지된다.
