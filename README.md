## Simple Static Blog

Next.JS를 이용한 Simple Static Blog 입니다. ([구현 페이지 미리보기](https://next-markdown-blog-teal.vercel.app/))  
Next.js 사이트 바로가기 : [Next.js](https://nextjs.org/)

## Getting Started
아래 명령어 실행 후 [http://localhost:3000](http://localhost:3000)로 접속하여 확인한다.

```bash
npm run dev
# or
yarn dev
```

## 파일 구조
NEXT JS를 이용하는 디렉토리 구조 관련
```bash
# NEXT-MK-BLOG

public # static 데이터&파일 보관
   └── images

# Nextjs에서는 Routing 시스템이 파일/폴더 구조로 되어있다.
pages  # 페이지를 담당하는 컴포넌트(폴더구조로 url 결정)      
├── blog
│     └── [slug].js
├── _app.js   # 화면별 공통 컴포넌트 설정
└── index.js  # /root

styles  # 스타일 관련 파일(css)
├── globals.css
└── Home.module.css

# 개인 생성 폴더 (모듈화 용도)
components # 공용 컴포넌트 사용 용도
utils

# Next 관련 폴더
.next
out # build 된 결과 남는 곳
```

## NEXT JS 관련 정보와 생각

1. 기존 CSR을 이용하는 SPA에서 처리하기 어려웠던 SEO 관련 된 부분을 SSR로 미리 서버에서 처리하기 때문에 SEO에 유리한 사이트 제작이 가능한것 같다.  
  1.1. **Static Generation(SSG)** - HTML파일이 최초 빌드시 생성되고 매 요청마다 HTML파일이 재사용된다.(성능에 이점을 가짐)  
  1.2. **Server-side Rendering(SSR)** - 매 요청마다 새로운 HTML파일을 프리렌더링한다(정적 사용이 불가능 할때 사용하도록 유도).  
  1.3. 페이지의 용도와 목적에 맞게 SSG, SSR을 사용한다. **Hydrate**라는 것도 있는데 공부가 필요할 듯 하다.
2. `_app.js`로 공통 레이아웃을 빠르게 설정 가능하다.
3. PreRendering 메서드, `getInitialProps` => 현재는 `getStaticProps`, `getStaticPaths`, `getServerSideProps`로 사전에 불러와야할 데이터(인바운드 데이터?)를 서버에서 미리 연산한다. PreRendering 메서드에서는 클라이언트에서 불가능한 Node.js의 `fs`, `path`와 같은 서버쪽 모듈을 사용가능하게 준비해준것 같다.  
  3.1. 서버사이드 연산 덕분에 빠른 속도로 처리가 가능해진다(연산은 서버가 브라우저는 로딩만 처리).  
  3.2. 사전 데이터를 서버에서 다 보내주었기 때문에 프론트 단에서 코드가 깔끔해 질 수 있다(`null`, `undefined` 등 처리).  

> **ServerSide 동작 원리 (구버전)** ([참고 LINK](https://velog.io/@kirin/Next.js-%ED%8E%98%EC%9D%B4%EC%A7%80-%EA%B5%AC%EC%A1%B0))
>1. Next Server가 GET 요청을 받는다.
>2. 요청에 맞는 Page를 찾는다. (기본은 index.js)
>3. _app.js의 getInitialProps가 있다면 실행한다.
>4. Page Component의 getInitialProps가 있다면 실행한다. pageProps들을 받아온다.
>5. _document.js의 getInitialProps가 있다면 실행한다. pageProps들을 받아온다.
>6. 모든 props들을 구성하고, _app.js > page Component 순서로 rendering.
>모든 Content를 구성하고 _document.js를 실행하여 html 형태로 출력한다.
