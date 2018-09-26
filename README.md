# Atomic-Design
Vue.js, React 프레임워크로 프로젝트를 시작할때 구조에 대한 고민을 합니다.

디자인 패턴을 찾아보던 도중 아토믹 디자인 패턴을 보고 해당 프레임워크와 잘 맞겠다는 생각이 들었습니다.

## Vue.js 아토믹 디자인 방식으로 구조 잡기
아토믹 디자인에는 5가지 구성 요소가 있습니다. 가장 작은 단위 순으로 나열 했습니다.

이해하기 쉽게 간단하게 설명을 적었습니다.

- ATOMS
- MOLECULES
- ORGANISMS
- TEMPLATES
- PAGES

### Atoms (원자)
Button, Input, Label, Span 같은 작은 단위의 요소 입니다.

### Molecule (분자)
원자 요소가 모여 분자를 구성하듯이 Button, Input, Label 등의 여러가지 태그를 결합하여 집합을 구성합니다.

이 집합을 예로 들자면 Input 태그와 전송 버튼이 합쳐진 Form 이라고 볼 수 있습니다.

<img width="250" alt="2018-08-23 7 41 40" src="https://user-images.githubusercontent.com/25811028/44520724-b81a2480-a70b-11e8-985f-0a4397c510ec.png">;

### Organism (유기체)
분자들이 모여 UI를 구성하는 인터페이스 생성합니다.
프로필 이라는 템플릿 안에 프로필 설정이라는 Organism 입니다.
따라서 Organism 는 템플릿 속에 존재하는 하나의 컴포넌트입니다.

<img width="500" alt="2018-08-23 7 47 26" src="https://user-images.githubusercontent.com/25811028/44521254-5eb2f500-a70d-11e8-9358-dab608619ea4.png">;

### Template & Page
템플릿과 페이지를 나눠야할 필요성을 느끼지 못하여 하나로 합쳐서 생각했습니다.
유기체, 분자들이 모여 하나의 페이지를 이룹니다.

<img width="700" alt="2018-08-23 8 33 40" src="https://user-images.githubusercontent.com/25811028/44523135-d2580080-a713-11e8-92b2-9deb347270d9.png">;

## 폴더 구조
Vue.js 프레임워크를 사용했습니다. 아래 구조는 Webpack를 사용했습니다.
- Src
- actions
   - `Organism 대한 XHR 요청 처리와 결과 데이터를 정리해서 컴포넌트에게 전달합니다.`
   - ..
- assets
   - css `컴포넌트의 Css 파일을 정의합니다`
    - ..
   - static
    - .. `정적 파일을 제공합니다 로고 이미지 등.. `

- components
   - atomic
    - `원자 단위의 컴포넌트를 정의합니다. 예를들어 공통으로 사용할 등록, 취소 버튼을 정의합니다.`
   - Molecule
    - `분자 단위의 컴포넌트입니다. 여러가지 태그가 모여 하나의 입력 폼 같은것을 컴포넌트화 시킵니다.`
   - Organism
    - `분자, 원자 단위가 합쳐저 하나의 인터페이스를 이룹니다. 해당 컴포넌트에서는 actions을 사용할 수 있습니다.`
   - Template
    - `Organism에 속하는 컴포넌트들이 모여서 레이아웃을 이룹니다. 해당 템플릿은 View에서 사용하여 웹페이지에 표시합니다.`
- directives
   - `Vue.js 에서 사용하는 디렉티브들을 모아놓습니다.`
   
- middleWare
   - `미들웨어입니다. 예를드면 인증 같은 절차를 해당 미들웨어에 추가해서 다룹니다.`
   
- router
   - `템플릿 폴더 마다 라우팅 폴더가 생성됩니다. /components/template/user..`
   
이렇게 구조를 잡고 프로젝트를 진행하니 원자, 분자에서 공통적으로 사용하는 부분을 유기체에서 가져와 사용해서
일관적인 인터페이스를 유지할 수 있어 사용자가 웹 어플리케이션에 익숙해 지는 시간이 빠르다고 느껴졌습니다.
