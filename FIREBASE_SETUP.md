# Firebase 설정 가이드

## 1. Firebase 프로젝트 생성

1. [Firebase Console](https://console.firebase.google.com/)에 접속
2. "프로젝트 만들기" 클릭
3. 프로젝트 이름 입력 (예: "attendance-notifier-app")
4. Google Analytics 사용 여부 선택 (선택사항)
5. "프로젝트 만들기" 클릭

## 2. 웹 앱 추가

1. 프로젝트 대시보드에서 "웹" 아이콘 클릭
2. 앱 닉네임 입력 (예: "attendance-notifier-web")
3. "앱 등록" 클릭
4. Firebase SDK 설정 정보 복사

## 3. Firebase 설정 정보 업데이트

`index.html` 파일의 Firebase 설정 부분을 실제 프로젝트 정보로 업데이트:

```javascript
const firebaseConfig = {
    apiKey: "실제_API_KEY_입력",
    authDomain: "실제_PROJECT_ID.firebaseapp.com",
    projectId: "실제_PROJECT_ID",
    storageBucket: "실제_PROJECT_ID.appspot.com",
    messagingSenderId: "실제_MESSAGING_SENDER_ID",
    appId: "실제_APP_ID"
};
```

## 4. Firestore Database 설정

1. Firebase Console에서 "Firestore Database" 클릭
2. "데이터베이스 만들기" 클릭
3. 보안 규칙 선택:
   - **테스트 모드**: 개발 중에만 사용 (모든 읽기/쓰기 허용)
   - **프로덕션 모드**: 실제 운영 시 사용 (보안 규칙 필요)
4. 데이터베이스 위치 선택 (가까운 지역 선택)

## 5. Authentication 설정

1. Firebase Console에서 "Authentication" 클릭
2. "시작하기" 클릭
3. "로그인 방법" 탭에서 "익명" 활성화
4. "저장" 클릭

## 6. Firestore 보안 규칙 설정 (선택사항)

Firestore Database > 규칙 탭에서 다음 규칙 설정:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // 출결 알리미 컬렉션에 대한 규칙
    match /artifacts/{appId}/public/data/attendance_requests/{document} {
      // 인증된 사용자만 읽기/쓰기 가능
      allow read, write: if request.auth != null;
    }
  }
}
```

## 7. 도메인 허용 설정 (GitHub Pages 배포 시)

1. Firebase Console에서 "Authentication" 클릭
2. "설정" 탭 클릭
3. "승인된 도메인" 섹션에서 "도메인 추가" 클릭
4. GitHub Pages URL 추가 (예: `your-username.github.io`)

## 8. 테스트

1. `index.html` 파일을 웹 서버에서 실행
2. 브라우저 개발자 도구 콘솔에서 오류 확인
3. 출결 알리미 제출 테스트
4. Firestore Database에서 데이터 확인

## 문제 해결

### "제출 중"에서 멈추는 경우:
1. Firebase 설정 정보가 올바른지 확인
2. 브라우저 콘솔에서 오류 메시지 확인
3. Firestore Database가 활성화되었는지 확인
4. 네트워크 연결 상태 확인

### 인증 오류가 발생하는 경우:
1. Authentication에서 익명 로그인이 활성화되었는지 확인
2. Firestore 보안 규칙 확인

### 도메인 오류가 발생하는 경우:
1. Authentication 설정에서 도메인이 허용되었는지 확인
2. HTTPS 연결 확인 (GitHub Pages는 자동으로 HTTPS 제공) 