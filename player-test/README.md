# Video.js Player Test Environment

Seeking 제한 + 배속 기능 테스트 환경

## 실행 방법

### 방법 1: 직접 브라우저에서 열기
```
index.html 파일을 브라우저로 드래그 앤 드롭
```

### 방법 2: 로컬 서버 실행 (CORS 이슈 방지)
```bash
# Python 3
python -m http.server 8080

# Node.js (http-server 설치 필요)
npx http-server -p 8080

# VS Code Live Server 확장 사용
```

이후 http://localhost:8080 접속

## 테스트 항목

### 1. 배속 기능
- [x] 0.5x ~ 2.0x 배속 변경
- [x] 배속 변경 시 이벤트 로그 확인
- [x] HLS 스트리밍에서 배속 동작 확인

### 2. Seeking 제한
- [x] 토글로 제한 ON/OFF
- [x] 시청하지 않은 구간으로 이동 시 차단
- [x] 이미 시청한 구간은 자유롭게 이동 가능
- [x] 최대 시청 위치 추적

## 기술 스펙

- Video.js 7.8.2 (프로젝트와 동일 버전)
- @videojs/http-streaming (HLS 지원)
- 순수 JavaScript (외부 의존성 없음)

## 프로젝트 적용 시 참고

### Seeking 제한 핵심 로직
```javascript
// seeking 이벤트에서 체크
player.on('seeking', function() {
    var targetTime = player.currentTime();
    if (targetTime > maxWatchedTime) {
        player.currentTime(maxWatchedTime);
    }
});
```

### 배속 설정 핵심 로직
```javascript
// 배속 변경
player.playbackRate(1.2);  // 1.2배속

// 현재 배속 조회
var rate = player.playbackRate();
```
