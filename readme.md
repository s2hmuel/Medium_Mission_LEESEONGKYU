# 미션1

## 회원작업

- [x] GET /member/join : 가입 폼
- [x] POST /member/join : 가입 폼 처리
- [x] GET /member/login : 로그인 폼
- [x] POST /member/login : 로그인 폼 처리
- [x] POST /member/logout : 로그아웃

## 글 작업

- [x] GET / : 홈
  - 최신글 30개 노출
- [x] GET /post/list : 전체 글 리스트
  - 공개된 글만 노출
- [x] GET /post/myList : 내 글 리스트
  - 내 글 목록 조회
- [x] GET /post/1 : 1번 글 상세보기
- [x] GET /post/write : 글 작성 폼
- [x] POST /post/write : 글 작성 처리
- [x] GET /post/1/modify : 1번 글 수정 폼
- [x] PUT /post/1/modify : 1번 글 수정 폼 처리
- [x] DELETE /post/1/delete : 1번 글 삭제

## 블로그 작업

- [x] GET /b/user1 : 회원 user1 의 전체 글 리스트
  - 특정 회원의 글 모아보기
- [x] GET /b/user1/3 : 회원 user1 의 글 중에서 3번글 상세보기

## 추가 작업

- [x] 조회수
- [x] 추천수
- [x] 댓글 작성
- [x] 댓글 수정
- [x] 댓글 삭제

# 미션2
## [x]필수미션 1 : Member 클래스에 private boolean isPaid 필드를 추가
- 해당 필드가 true 인 사람이 로그인할 때, ROLE_PAID 권한도 가지도록(스프링 시큐리티)
- 해당 필드가 true 이면 유료 멤버십 회원 입니다.

## [x]필수미션 2 : Post 클래스에 private boolean isPaid 필드를 추가
- 해당 필드가 true 인 글은 유료회원이 아닌사람에게는 상세보기(GET /post/1)에서 본문(content)이 나올 자리에 이 글은 유료멤버십전용 입니다. 라는 문구가 나온다.

### 엔드 포인트
- GET /post/list
  - 멤버십 회원이 아니라도 글 리스트에서는 멤버십 전용글을 볼 수 있습니다.

- GET /post/1
  - 유료 멤버십 회원이고 1번 글이 멤버십전용글 이라면 볼 수 있다.
  - 그 외에는 이 글은 유료멤버십전용 입니다. 노출

## [x]필수미션 3 : NotProd 에서 유료멤버십 회원(샘플 데이터)과 유료글(샘플 데이터)을 각각 100개 이상 생성 

## [ ]선택미션 1 : 검색 필터링, 정렬
### 엔드 포인트
- GET /post/list?sortCode=idDesc&kwType=title&kw=검색어
  - 정렬 : id 최신순, 검색범위 : 제목
- GET /post/list?sortCode=hitAsc&kwType=body&kw=검색어
  - 정렬 : id 오래된순, 검색범위 : 내용
- GET /post/list?sortCode=hitDesc&kwType=title,body&kw=검색어
  - 정렬 : 조회수 높은순, 검색범위 : 제목과 내용
- GET /post/list?sortCode=likeCountAsc&kwType=title,body,author&kw=검색어
  - 정렬 : 추천수 낮은순, 검색범위 : 제목과 내용과 작성자 아이디

## [ ]선택미션 2 : 글 본문에 마크다운 에디터 적용
- 토스트 UI 에디터 적용

## [ ]선택미션 3 : 토스트 UI 에디터에 이미지 파일 업로드 기능 적용
- 토스트 UI 에디터의 파일업로드 기능 구현
- 기본적으로 토스트 UI 에디터는 업로드한 이미지를 base64 인코딩하여 표시한다.
- 그러면 본문의 내용이 너무 길어져서 문제가 된다.
- addImageBlobHook 활용
- https://ui.toast.com/tui-editor

## [ ]선택미션 4 : 카카오 로그인
## [ ]선택미션 5 : 위 모든 기능의 뷰를 타임리프 뿐 아니라 별도의 도메인에서 스벨트킷으로도 구현
- /api/v1 로 시작하는 URL에서 API 구현
- 루트 폴더에 frontapp 폴더 생성, 그 안에 스벨트킷 프로젝트 생성
- next.js 까지는 허용

- ## [ ]선택미션 6 : 배포, 도메인 연결, 젠킨스 CI/CD
- ## [ ]선택미션 7 : 배포, 도메인 연결, 쿠버네티스, 깃허브액션, 무중단 CI/CD
- ## [ ]선택미션 8 : 정산기능구현
- 정산기능을 토스페이먼츠를 이용해서 구현해주세요(자동결제, 빌링)
- 자동결제로 하셔도 되고, 카드결제로 하셔도 됩니다.
- 한달에 1번(15일 0시 0분), 유료글 작성자에게 해당 유료글의 전달 조회수를 기준으로 멤버십수익을 통해 얻은 수익을 나눠줍니다.(정산)
- 미디엄이 수익의 50%을 가지고, 나머지 50%을 각각 유료사용자들에게 캐시로 나눠줍니다.(절대로 바로 돈으로 은행송금하지않습니다.)
- 그 외의 구현방식은 자유입니다.