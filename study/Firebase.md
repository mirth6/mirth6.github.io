# Firebase

https://brunch.co.kr/@second-space/5

[TOC]

## Firebase

모바일 앱/웹 서비스를 구축하는데 필요한 여러가지 기능을 갖추고 있는 클라우드 서비스



### Firestore

NoSQL 데이터베이스 지원

json형태

소켓으로 연결되어 실시간 서비스를 구축하기 좋음

다중 컬럼 검색 불가능

정렬색인 따로 지정해 줘야함

반응 속도 느림



### Storage

클라이언트 단에서 바로 파일을 올리기 쉬움



### Authentication(계정연동)

이메일/비밀번호, 전화/SNS로그인, 익명로그인 방식 제공

이메일 인증, 비밀번호 재설정, 이메일 주소 변경, SMS인증 등 제공

인증 받은 사용자만 firestore, storage접근 가능 하도록 



### Hosting

프론트 앤드 기반의 웹 소스를 올릴 수 있는 서비스

CDN에 등록 됨->속도 이슈 생각하지 않아도 됨



### Cloud Messaging