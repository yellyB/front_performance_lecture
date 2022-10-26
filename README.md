# front_performance_lecture
강의 내용 메모: 프론트엔드 개발자를 위한, 실전 웹 성능 최적화(feat. React) - Part. 1

---
![image](https://user-images.githubusercontent.com/50893303/197386638-b66044fc-9f5f-44d8-bee8-45084c4f901b.png)
### :book: 0-4) 포인트

로딩 성능: HTML, JS, CSS 파일 불러오기

렌더링 성능: 불러온 파일 웹에 그려주기
  
### :book: 1-2) 측정 방법 소개

[성능 측정]  
network 탭  
perfomance 탭  
audit(light house) 탭  
webpack-bundle-analyzer → 웹팩 라이브러리, 웹팩으로 번들링된 파일들이 어떤 코드를 담고 있는지 한눈에 보여줌  
  
  
### :book: 1-4) Lighthouse 툴 사용하기  
  
[검사하기]  
  
Lighthouse(Audits) - 성능 측정 & 성능 향상 가이드  
 - Categories 중에 Performance 주로 사용. 여기 체크해서 측정하자. ⇒ 세팅 다 하면 검사 버튼 ㄱㄱ
  
[검사 결과]  
  
제일 위 숫자: 성능 점수. 항목들 설명 자세히 볼 수도 있음

그 아래 스샷: 페이지 로드되는 흐름  
  
Opportunities랑 DIAGNOSTICS는 가이드 제시 (근데 오퍼튜니티는 왜 안보이지. 추측하기로는 위에 Performance 가 렌더링, 아래 Best Practies(여기서 USER EXPERIENCE항목) 가 로딩 인듯?)  
- Opportunities는 리소스 관점(=로딩 성능)  
- Diagnostics는 페이지 실행 관점(=렌더링 성능)  
- PASSED AUDITS 는 이미 잘 적용된 항목  
  
  
### :book: 1-5) 이미지 최적화(Opportunities의 문제점들 해결)  

**Properly size images  
:** 이미지를 적절한 사이즈로 압축해서 시간 줄이란 내용  
이미지는 보여줄 크기보다 너비기준 두배 사이즈로 불러오는게 적절  
⇒ 근데 어떻게 줄임?  
이미지가 정적 이미지였다면 그냥 자르면 되는데, api에서 받아오는 경우는 어캄?  
  
방법1) Image CDN  
: 내가 원하는 결과 정보(지금은 width랑 height)를 파라미터로 넘겨서 이미지 가공 받기  
- 우리가 직적 구축하는건 어려우니까 솔루션 사용 가능. 대표적으로 imgIX 라는 솔루션 있음.
  
방법2) CDN사용 X  
- 이미지 태그에서 프로퍼티로 getParametersForUnsplash(나중에 참고할 일 있을 때 깃헙 들어가서 검색해보자) 함수 같이 넘김. 여기서 크기 수정하면됨.  
- [함수 파라미터 참고](https://unsplash.com/documentation#supported-parameters) 이 unsplash 가 이미지CDN 역할 해줌
  
  
  
### :book: 1-6) 느린 자바스크립트 어떻게 최적화? Performance 탭  
  
일단 Opportunities 남은것들:  
  
**Minify JavaScript**  
: 공백, 주석 제거(CRA 하면 알아서 해줌)  
  
**Preconnect to required origins**  
: 미리 리소스 주소 프리커넥트해라 (다른 강의에서 나올거임)  
  
이제 Diagnostics 보자  
  
**Minimize main-thread work** : 메인 스레드 작업을 좀 줄여라. 어떤 작업에서 오래 걸렸나 나옴  
  
**Serve static assets with an effcient cache policy** : 캐시 안되어있는거 캐시해라  
  
**Reduce JavaSciprt execution time**  
: 어디서 얼마나 걸렸나 보여줌. (아래 chrome 어쩌구는 우리 서비스와 관련 없는 크롬 확장프로그램 문제임. 여긴 패스하자)  
  
⇒ 문제점들은 알았지만 구체적으로 어떤 코드에서 문제인지는 모름  
⇒ 그래서 필요한게 Performance 탭  
  
  
### Performance 탭  
  
페이지가 로드되면서 실행되는 작업들을 타임라인과 차트 형태로 보여줌  
사용법: 왼쪽 위 새로고침 아이콘 누르면 분석됨  
맨 위는 타임라인 - 드래그로 일부 선택, 더블클릭으로 전체 선택  
  
[구체적 그래프 살펴보기]  
- Timings에 파랑, 초록 버튼?들 부분에 **FP(First Paint)시점**부터 페이지가 그려짐  
- 프레임 차트의 Network 쪽 보면 api 통신 볼 수 있음  
  
  
<img width="952" alt="image" src="https://user-images.githubusercontent.com/50893303/197130551-cb022c41-afbb-4a5f-a6d3-3c1e283e0e4f.png">
  
  
예시화면에서 Article 은 하나의 작업인데 너무 많은 리소스를 사용하다보니 가비지컬렉터에 의해 중간중간 끊긴것.  
이미지 보면 Minor GC 가 보임. 메모리의 여유가 없어서 정리해주는 작업.  
  
![image](https://user-images.githubusercontent.com/50893303/197130984-8d363aa0-a310-4121-83dc-81e65563fc63.png)
  
  
  
### :book: 1-7) 1-6을 최적화  
  
Performance에서 분석한대로 컴포넌트 안 함수 찾아서 최적화하자  
 ⇒ 원하는 기능을 효과적으로 사용(ex 정규식, 라이브러리 등)  
 ⇒ 반복문 성능 개선시키기  
  
  
