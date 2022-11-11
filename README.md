# front_performance_lecture

강의 내용 메모: 프론트엔드 개발자를 위한, 실전 웹 성능 최적화(feat. React) - Part. 1

---

## 배울것들

<img src="https://user-images.githubusercontent.com/50893303/197386638-b66044fc-9f5f-44d8-bee8-45084c4f901b.png" width="300">

<br/>

# :book: 0-4) 포인트

로딩 성능: HTML, JS, CSS 파일 불러오기

렌더링 성능: 불러온 파일 웹에 그려주기

# 📖 참고) Performance 탭

![image](https://user-images.githubusercontent.com/50893303/201566739-3d2c4210-1611-4671-b3f4-bf4cebe691f7.png)

- 스크린샷
- 메모리
- 쓰레기통 아이콘: 가비지 컬렉터 강제 수행: 성능 측정할 때 누르면 Major GC 라고 Main프레임 차트에 보여질거임

<br/>

![image](https://user-images.githubusercontent.com/50893303/201566269-a9bf6df2-373f-406e-ace3-0d8ea10008e9.png)

설정 누르면 나오는 4개의 옵션

- Disavle JavaScript samples: 메인 스레드 영역의 우리가 알 필요 없는 사소한 작업들 측정 안됨
- Enable advanced paint Instrumentation
- Network: 네트워크 보틀넥 설정
- CPU: 씨피유 보틀넥 설정

<br/>

![image](https://user-images.githubusercontent.com/50893303/201563493-d400d6fd-c02a-4345-bd60-f2e99f58c9e2.png)

- 노랑: 자바스크립트 실행 영역
- 보라: 레이아웃 작업 영역
- 초록: 페인트나 컴포짓 영역

<br/>

![image](https://user-images.githubusercontent.com/50893303/201563627-8af1e6c4-e5c3-42b8-8e0f-285bf240ec20.png)

Network: 네트워크 타임라인

- 가느다란 왼쪽 선: 네트워크 요청 보내기 전 커넥션 준비
- 흰색 박스: 네트워크 요청 보내고 기다리는 시간
- 회색: 컨텐츠 실제로 다운
- 가느다란 오른쪽 선: 메인 스레드에서 컨텐츠 처리하는 시간

<br/>

![image](https://user-images.githubusercontent.com/50893303/201564113-e818f86b-5ce9-45cd-b549-e356d14aa08a.png)

Timings: 크롬에서 측정하는 몇 가지 측정기준 있음

- DCL: Dom Contents Loaded :
- FP: First Paint : 최초 요소가 페이지에 그려지는 시점 표시
  리액트의 경우 컴포넌트가 어떻게 실행되었는지, 어떤 함수 호출되었는지 보여주기도

Main: 자바스크립트 메인 스레드에서 벌어지는 작업들

<br/>

![image](https://user-images.githubusercontent.com/50893303/201564505-88d70d7f-527d-4417-8416-443ad4db22a2.png)

Summary: Main의 프레임 차트 클릭 or 드래그(shift 누르면 선택됨)한 부분의 작업을 비율로 보여줌

Bottom-Up: 작업들을 역순으로 보여줌. 트리를 타고 가면 해당 작업을 호출한 루트 태스크가 나옴

Call Tree: 바텀업과는 반대로 실행된 정상적인 순서대로 보여줌

<br/>

![image](https://user-images.githubusercontent.com/50893303/201565190-93845af8-e40c-478a-8bc8-f62cc9ae4f55.png)

해당 옵션 선택하고 성능 측정 돌리고 프레임에 영역 하나 클릭하면 Layers 볼 수 있음  
 : 브라우저가 여러개의 레이어 만들고 컴포짓(합침)하는데 그 레이어가 어떻게 구성되어 있는지 보여줌
<br/>

![image](https://user-images.githubusercontent.com/50893303/201565388-cce672a4-2cc1-4a0f-a980-f05ed054a07a.png)

Paint 작업 클릭 ⇒ 레이아웃 단계 이후 페인트 작업 어떤 단계로 이루어지는지 보여줌

<br/>
