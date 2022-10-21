# front_performance_lecture
강의 내용 메모: 프론트엔드 개발자를 위한, 실전 웹 성능 최적화(feat. React) - Part. 1

---

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




