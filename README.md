# 출결 알리미 웹 애플리케이션

학생들의 출결 알리미를 관리하는 웹 애플리케이션입니다.

## 기능

### 학생 기능
- 출결 알리미 신청 (학번, 이름, 병명 입력)
- 내 알리미 목록 확인 및 검색
- 알리미 상태 확인 (대기 중, 승인됨, 거절됨)

### 교사 기능
- 전체 학생들의 출결 알리미 목록 확인
- 알리미 승인/거절 처리
- 실시간 업데이트

## 기술 스택

- **Frontend**: HTML5, CSS3, JavaScript (ES6+)
- **UI Framework**: Tailwind CSS
- **Backend**: Firebase (Firestore, Authentication)
- **Build Tool**: CDN 기반 (별도 빌드 불필요)

## 설치 및 실행

### 1. Firebase 프로젝트 설정

1. [Firebase Console](https://console.firebase.google.com/)에서 새 프로젝트 생성
2. Firestore Database 활성화
3. Authentication에서 익명 로그인 활성화
4. 프로젝트 설정에서 웹 앱 추가

### 2. Firebase 설정 업데이트

`test20250628.html` 파일의 Firebase 설정을 실제 프로젝트 정보로 업데이트:

```javascript
const firebaseConfig = {
    apiKey: "YOUR_ACTUAL_API_KEY",
    authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT_ID.appspot.com",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
    appId: "YOUR_APP_ID"
};
```

### 3. 실행

1. 파일을 웹 서버에 업로드하거나 로컬 서버에서 실행
2. 브라우저에서 `test20250628.html` 접속

## 배포

### GitHub Pages 배포

1. 이 저장소를 GitHub에 업로드
2. Settings > Pages에서 Source를 선택
3. Branch를 선택하고 Save

### 보안 고려사항

- Firebase API 키는 공개적으로 노출되지만, Firestore 보안 규칙으로 보호
- 교사 모드 접근을 위한 비밀번호는 클라이언트 사이드에 하드코딩되어 있음 (실제 운영 시 서버 사이드 검증 필요)

## 사용법

### 학생 모드
1. 학번, 이름, 병명을 입력하여 출결 알리미 신청
2. "나의 알리미 목록 확인하기" 버튼으로 제출한 알리미 확인
3. 검색 기능으로 특정 알리미 필터링

### 교사 모드
1. 우측 상단 "교사 모드로 전환" 버튼 클릭
2. 비밀번호 입력 (기본값: 1225)
3. 전체 학생들의 알리미 목록 확인
4. 각 알리미에 대해 승인/거절 버튼으로 처리

## 라이선스

MIT License

## 기여

이슈 리포트나 풀 리퀘스트를 통해 기여해주세요. 