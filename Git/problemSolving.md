# error : src refspec master does not match any 에러 해결 방법

## 문제 상황

- 로컬 저장소에서 깃 초기화
- 로컬 저장소에서 파일 수정 후 커밋
- 원격 저장소와 로컬 저장소 연결
- 로컬 저장소에서 원격 저장소로 푸쉬했을 때 "error : src refspec master does not match any" 에러 메세지 발생

## 해결한 방법

- 원격 저장소를 먼저 생성하고(깃허브 홈페이지에서)
- **git clone 원격저장소주소 디렉터리명** 명령으로 원격 저장소를 로컬 환경에 복제
- 디렉터리 이동 후 파일 생성, 수정, 저장
- 디렉터리에서 커밋
- 디렉터리에서 **git push**로 커밋한 내용 원격 저장소로 푸쉬
