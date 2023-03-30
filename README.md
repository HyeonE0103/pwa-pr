# PWA

## PWA란
Progressive Web App 줄여서 PWA  
웹사이트를 안드로이드/iOS 모바일 앱처럼 사용할 수 있게 만드는 일종의 웹개발 기술  
React를 이용해 만든 웹사이트를 모바일 앱으로 발행해서 쓰자는 의도  
다만 iOS, Android 앱으로 발행하는게 아니라 웹사이트 자체를 스마트폰 홈화면에 설치하는 것

## PWA장점
- 스마트폰, 태블릿 바탕화면에 웹사이트를 설치 가능
- 오프라인에서도 동작할 수 있음
- 설치 유도 비용이 매우 적음

## PWA 만들기

터미널에
```js
npx create-react-app 프로젝트명 --template cra-template-pwa
```
입력하여 프로젝트를 만듬  

프로젝트에 index.js파일 하단에 있는
```js
serviceWorkerRegistration.unregister();
```
를
```js
serviceWorkerRegistration.register();
```
로 변경  

터미널에
```js
npm run build
```
입력하여 build를 하면 manifest.json과 service-worker.js 파일이 자동으로 생성됨

## manifest.json파일
manifest.json 파일은 웹앱의 아이콘, 이름, 테마색등을 결정하는 파일

```js
{
  "version" : "앱의 버전
  "short_name" : "설치후 앱런처나 바탕화면에 표시할 짧은 12자 이름",
  "name" : "기본이름",
  "icons" : { 여러가지 사이즈별 아이콘 이미지 경로 },
  "start_url" : "앱아이콘 눌렀을 시 보여줄 메인페이지 경로",
  "display" : "standalone 아니면 fullscreen",
  "background_color" : "앱 처음 실행시 잠깐 뜨는 splashscreen의 배경색",
  "theme_color" : "상단 탭색상 등 원하는 테마색상",
}
```
말구도 여러가지를 결정할 수 있음

## service-worker.js
앱이 설치될때 앱 구동에 필요한 이미지, 데이터들이 전부 하드에 설치됨  
로고 같은 데이터를 서버에 요청하는게 아닌 하드에 이미 설치되어 있는걸 그대로 가져와서 쓰는것  
이것을 흉내내도록 도와주는 파일이 바로 service-worker파일  
이 파일에 설정을 잘 해주면 웹앱을 설치했을 때 어떤 CSS, JS, HTML, 이미지 파일이 하드에 설치될지 결정할 수 있음  
다음에 앱을 켤 때마다 서버에 CSS,JS,HTML 파일을 요청하는게 아니라 Cache Storage에 저장되어있던 CSS,JS,HTML 파일을 사용하게 됨 이로써 오프라인에서 사용이 가능해지는 것  

react가 알아서 해주기 때문에 설정은 이미 되어있음  
모든 HTML CSS JS 파일을 cache storage에 저장하도록 기본 셋팅이 되어있는데  
간혹 저장해두기 싫은, 자주변하는 파일들이 간혹 있을 경우 파일을 수정하면 됨  

## 개발자도구로 PWA 디버깅
build 했던 프로젝트가 PWA인지 살펴보고 싶다면 2가지 방법이 있음  
- 사이트를 호스팅받아 올리기
- VScode 익스텐션중에 live server 검색해서 설치
  1. build 폴더를 에디터로 오픈
  2. build 폴더에 있는 index.html을 우클릭 - live server로 띄우기

사이트에서 크롬 개발자도구를 켜시면 Application 이라는 탭이 있음 여기서 PWA와 관련된 모든걸 살펴볼 수 있음  
Manifest 메뉴에선 manifest.json 내용들을 확인 가능하고  
Service Worker 메뉴에선 service-worker 파일이 잘 있는지, 오프라인에선 잘 동작하는지 테스트 가능하고  
푸시알림 기능을 개발해놨다면 푸시알림도 샘플로 전송해볼 수 있음  
Cache Storage 메뉴에선 service-worker 덕분에 하드에 설치된 CSS, JS, HTML 파일들을 확인할 수 있음  
캐시된 파일 제거도 가능함