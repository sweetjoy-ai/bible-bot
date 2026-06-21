# Bible Bot 진행 상황

## 프로젝트 개요
- **목적**: 한국어/영어 성경 필사(transcription) 웹앱
- **배포 URL**: spacejoy.withlinkus.com/bible
- **GitHub**: github.com/sweetjoy-ai/bible-bot
- **서버**: AWS Lightsail (Ubuntu, FastAPI + nginx)
- **서버 파일 경로**: /home/ubuntu/spacejoy/dashboard/public/bible/index.html

## 완료된 작업

### 핵심 기능
- [x] 해시 기반 라우팅: `#bible` → `#bible/genesis` → `#bible/genesis1`
- [x] 66권 전체 BOOK_MAP (한국어명 → [영문 slug, 권번호])
- [x] 한국어 성경 API: getbible.net v2 (개역한글)
- [x] 영어 성경 API: wldeh/bible-api (WEBUS) + getbible.net 폴백
- [x] 필사 UI: 절번호 + 한글 본문 + 한글 입력 + 영문 본문 + 영문 입력
- [x] Enter 키로 다음 칸 이동, 마지막 절 후 저장 팝업
- [x] 로컬스토리지 진행상황 저장

### UX 개선
- [x] 오프라인 캐시: 한 번 본 챕터는 localStorage에 저장 (bibleText:slug:chapter)
- [x] 다크모드 영문 텍스트 색상 개선: `#e8dab8` (warm ivory)
- [x] 한국어 IME 버그 수정: `e.isComposing || e.keyCode === 229` + `setTimeout`
- [x] 국립공원꼬미 폰트 base64 내장 (KNPSKkomi.otf → 870KB)

### 배포
- [x] GitHub 백업 완료 (sweetjoy-ai/bible-bot)
- [x] nginx 설정 (alias 디렉티브로 정적 파일 서빙)
- [x] 파일 권한 설정 (chmod 755 디렉토리, 644 파일)

## API 정보 (공개 정보)
- 한국어: `https://api.getbible.net/v2/korean/{bookNum}/{chapter}.json`
- 영어: `https://cdn.jsdelivr.net/gh/wldeh/bible-api/bibles/en-WEBUS/books/{slug}/chapters/{chapter}.json`

## 남은 작업
- [ ] 다크모드 수정본 서버 업로드 (scp로 /tmp/bible01.html → 서버)
- [ ] 손글나래, 교보손글씨2025 폰트 추가 (선택사항)

## 서버 업로드 명령어 (IP는 직접 입력)
```bash
cp "/Users/sweetjoy/Desktop/무제 폴더/bible-bot/bible01.html" /tmp/bible01.html
scp -i ~/Downloads/Sweetjoy_Bot.pem /tmp/bible01.html ubuntu@[서버IP]:~/spacejoy/dashboard/public/bible/index.html
```

## 주의사항
- 서버 IP, PEM 키 경로는 이 파일에 적지 말 것
- 민감 정보는 맥 터미널에서 직접 입력
