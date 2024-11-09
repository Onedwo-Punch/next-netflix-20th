# 5 ~ 6주차 미션: Next-Netflix

<br>

## [🪄 결과물](https://next-netflix-20th-onedwo.vercel.app)

### 🩵 구현 기능

- 피그마 화면 구현

- SSR을 적용해서 구현

- Open api를 사용해서 데이터 패칭을 진행

- 동적 라우팅으로 상세 페이지 구현

### 🩵 느낀 점

**[송유선]** 협업으로 진행하는 첫 스터디 과제라 우여곡절이 많았던 것 같다. 초기 세팅을 맞출 때부터 오류가 많이 나서 당황했지만, 같이 극복하는 과정에서 배운 것도 많았다. (public 폴더의 위치에 따른 경로 설정부터, next.js 의 파일 구조까지...) 이번에 Next.js, Tailwind.css, OpenAPI 등 처음 써 보는 게 너무 많아서 더 애를 먹었던 것 같다. 효율적인 코드를 작성하고 싶었는데 맞게 작성하고 있는지 확신할 수가 없어서 답답했다.. 나는 main과 detail 페이지를 작업했는데, 고민을 했던 부분 중 하나는 랜딩에서 혼합되어 있는 컨텐츠들의 상세 페이지를 어떻게 라우팅할지였다. 종류가 movie랑 tv로 섞여 있는데 getContents에서 불러오는 정보에는 영화인지 티비 프로그램인지 알려주는 부분이 없었지만 detail 정보를 요청하기 위해서는 id 앞에 종류를 써야 했다. 그래서 아예 상세 페이지를 라우팅할 때 미리 정의한 media_type을 (`const media_type = category.includes('/tv') ? 'tv' : 'movie';`) id와 함께 주소에 넣고 넘긴 뒤 params로 작업했는데... 버셀에서 배포할 때 오류가 났다..^^ 로컬에선 아무 문제 없었는데, 배포 시에는 더 엄격한 타입 검증을 해서 그런 것 같다. params 말고 props 각각 타입 지정해보기도 하고 여러 방법을 써 봤는데 아직 만족스럽게 해결하지 못 했다... (결국 eslintrc 에 any 쓸 수 있도록 규칙 추가함...) 이 부분은 다음 주에 가능하면 좀 더 괜찮은 방향으로 수정해보고 싶다. 추가로, 이번에는 스켈레톤이나 로딩 중에 보여줄 화면을 따로 만들지 못했는데 다음 주에 간단하게라도 추가해보고 싶다.
<br/><br/>
**[최지원]** ...
<br/>

## 💡Key Questions

### 1️⃣ React 18 버전의 변경점에 대해 설명해주세요.(+ 19 버전에 대한 추가 설명도 좋습니다)

### 2️⃣ nextJS 13 이후의 app routing 방식의 특징과 기능에 대해 설명해주세요.

Next.js 13 버전은 기존의 페이지 라우팅 방식에서 벗어나 새로운 App Routing 방식을 도입하여 개발자 경험과 성능을 향상시켰다. 우선 첫째로, 디렉터리를 구성하는 방식에 변화가 생겼다.

13 이전 버전에서는 pages 디렉터리를 중심으로 라우팅이 이루어졌다. pages 디렉터리 내부에 파일이나 디렉터리를 생성하면 해당 경로가 자동으로 라우팅되었다. (pages/main.js 파일을 생성하면 /main 경로로 접근하는 방식) 그러나 13에서는 새로운 app 디렉터리를 도입하여 해당 방식을 개선하였다. 우선 각 디렉터리 내에 layout.js 파일을 생성하여 해당 경로의 공통 레이아웃을 정의할 수 있고, loading.js와 error.js 파일을 통해 로딩 상태와 에러 처리를 디렉터리별로 관리할 수 있으며, 파일 상단에 'use client'; 지시어를 사용하여 클라이언트 컴포넌트를 정의할 수도 있다.

Next.js 13에서는 기본적으로 서버 컴포넌트(서버에서 렌더링되며, 비동기 함수로 정의 가능)를 사용하며, 필요에 따라 클라이언트 컴포넌트('use client'; 지시어를 사용하여 정의하며, 브라우저에서 실행됨)를 정의한다. 서버 컴포넌트에서는 데이터베이스 접근, API 호출 등 서버 측 로직을 직접 구현할 수 있다. 이를 통해 서버리스 함수를 작성할 수 있으며, 별도의 백엔드 서버 없이도 백엔드 로직을 구현할 수 있다.

또한, 패러랠 라우트(동일한 레벨에서 여러 경로를 동시에 렌더링할 수 있도록 하는 기능)와 인터셉팅 라우트(기존의 네비게이션 흐름을 가로채어 다른 UI를 렌더링할 수 있게 함)도 구현 가능하다. 각각 [[]]나 (())를 사용하여 라우트를 정의하면 된다.

SSR은 서버 사이드 렌더링으로, 요청 시점에 서버에서 HTML을 생성하여 클라이언트에게 전달하는 방식이다. Next.js에서는 기본적으로 페이지 컴포넌트를 비동기 함수로 정의하고, 내부에서 데이터를 패칭하여 SSR을 구현한다. SSG는 빌드 시점에 HTML을 생성하여 CDN에 배포하는 방식으로, 빠른 응답 속도와 캐싱에 유리하다는 장범이 있다. Next.js에서 이걸 구현하려면 getStaticProps나 generateStaticParams를 사용하면 된다.

### 3️⃣ vercel, netlify 같은 호스팅 플랫폼의 특징과 내부 구현 원리에 대해 설명해주세요(+ aws의 스토리지와 인스턴스 등 생태계에 대해서도 알려주세요)
