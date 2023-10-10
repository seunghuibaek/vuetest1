popaos1

USP_Mod_GnrlCashGudsPymnt_002
USP_Mod_GnrlCashGudsPymntForChnlg_002
USP_Mod_EvntCashGudsPymnt_002
USP_Mod_LxryCashGudsPymnt_002

B_COIN


118.129.153.86,9190
SSM_castBookMark_execute_D_DD      팝콘 sp
JBN_JSON_castBookMark_enrollment    api 서버에서 사용하는 sp

CastOnLists 
추가조회 필드
pAdultFileName(방송자 성인 썸네일이 있니)
isAdult

팝콘 주간랭킹 SP
변경이 필요한 프로시저
[B_CASTDATA].[dbo].[USP_GetList_WkMlyRnkg_003]
B_CASTDATA.dbo.castOnData(VW_CastOnLists)
118.129.153.93,9190

-----------------------


PC
커밋: 3bc28c2d7ff4a5488444049a81939c9b4eaf6f62 [3bc28c2]
상위 항목: 26df2a9640
작성자: 백승희 <sh.back@theenm.com>
날짜: 2023년 9월 20일 수요일 오전 9:44:37
커밋한 사람: 백승희

MW
커밋: e41e364d22183fe8dcbcefc84ac73c2b632d1aca [e41e364]
상위 항목: 6187d90501
작성자: 백승희 <sh.back@theenm.com>
날짜: 2023년 9월 20일 수요일 오전 9:38:22
커밋한 사람: 백승희

[B_VOD].[dbo].[LHY_WEB_vodCategory_Listrandom]
118.129.153.91,9190


100032	린크_대상_여부	RnkTgtYn
100033	린크_앱스토어_버전	RnkAppstorVer
100034	린크_앱스토어_다운로드_URL	RnkAppstorDwnlUrl
100035	린크_구글플레이_버전	RnkGglplyVer
100036	린크_구글플레이_다운로드_URL	RnkGglplyDwnlUrl
100037	린크_플러스_대상_여부	RnkPlusTgtYn
100038	린크_플러스_앱스토어_기업_프로그램_버전	RnkPlusAppstorEntrPgmVer
100039	린크_플러스_앱스토어_기업_프로그램_다운로드_URL	RnkPlusAppstorEntrPgmDwnlUrl
100040	린크_플러스_원스토어_버전	RnkPlusOnestorVer
100041	린크_플러스_원스토어_다운로드_URL	RnkPlusOnestorDwnlUrl
100042	린크_플러스_원스토어_심사_진행_여부	RnkPlusOnestorInspPrgrYn
100043	린크_플러스_원스토어_심사_버전	RnkPlusOnestorInspVer
100044	린크_플러스_갤럭시스토어_버전	RnkPlusGlxstorVer
100045	린크_플러스_갤럭시스토어_다운로드_URL	RnkPlusGlxstorDwnlUrl
100046	린크_플러스_갤럭시스토어_심사_진행_여부	RnkPlusGlxstorInspPrgrYn
100047	린크_플러스_갤럭시스토어_심사_버전	RnkPlusGlxstorInspVer
100048	린크_플러스_안드로이드_수동_다운로드_앱_버전	RnkPlusAndrdPssivDwnlAppVer
100049	린크_플러스_안드로이드_앱_수동_다운로드_URL	RnkPlusAndrdAppPssivDwnlUrl


15	린크_플러스_앱스토어_기업_프로그램
16	린크_앱스토어
17	린크_구글플레이
18	린크_플러스_원스토어
19	린크_플러스_갤럭시스토어
20	린크_플러스_안드로이드_수동_다운로드_앱



172.17.11.52
121.134.158.29


114.141.29.100
114.141.29.101
114.141.29.109
114.31.50.115

# Vue3 템플릿 with Webpack

## Versions

- [Default](https://github.com/ParkYoungWoong/vue3-webpack-template/tree/master)<br>
- [+ESLint](https://github.com/ParkYoungWoong/vue3-webpack-template/tree/eslint)<br>
- [+ESLint+Vuex](https://github.com/ParkYoungWoong/vue3-webpack-template/tree/vuex)<br>
- [+ESLint+Vuex+VueRouter](https://github.com/ParkYoungWoong/vue3-webpack-template/tree/vue-router)<br>

## Installation

```bash
# Default.
$ npx degit ParkYoungWoong/vue3-webpack-template DIRECTORY_NAME

# With ESLint, Add `#eslint`.
$ npx degit ParkYoungWoong/vue3-webpack-template#eslint DIRECTORY_NAME

# With ESLint + Vuex, Add `#vuex`.
$ npx degit ParkYoungWoong/vue3-webpack-template#vuex DIRECTORY_NAME

# With ESLint + Vuex + VueRouter, Add `#vue-router`.
$ npx degit ParkYoungWoong/vue3-webpack-template#vue-router DIRECTORY_NAME

# Start!
$ cd DIRECTORY_NAME
$ npm i
$ npm run dev
```

## Specs

- Vue3
- Webpack
- SCSS
- Babel
- PostCSS
- Autoprefixer
- ESLint __(+ESLint)__
- Vuex __(+Vuex)__
- Vue Router __(+VueRouter)__

## Packages

__webpack__: 모듈(패키지) 번들러의 핵심 패키지<br>
__webpack-cli__: 터미널에서 Webpack 명령(CLI)을 사용할 수 있음<br>
__webpack-dev-server__: 개발용으로 Live Server를 실행(HMR)<br>

__html-webpack-plugin__: 최초 실행될 HTML 파일(템플릿)을 연결<br>
__copy-webpack-plugin__: 정적 파일(파비콘, 이미지 등)을 제품(`dist`) 폴더로 복사<br>

__sass-loader__: SCSS(Sass) 파일을 로드<br>
__postcss-loader__: PostCSS(Autoprefixer)로 스타일 파일을 처리<br>
__css-loader__: CSS 파일을 로드<br>
__style-loader__: 로드된 스타일(CSS)을 `<style>`로 `<head>`에 삽입<br>
__babel-loader__: JS 파일을 로드<br>
__vue-loader__: Vue 파일을 로드<br>
__vue-style-loader__: Vue 파일의 로드된 스타일(CSS)을 `<style>`로 `<head>`에 삽입<br>
__file-loader__: 지정된 파일(이미지)을 로드<br>

__@babel/core__: ES6 이상의 코드를 ES5 이하 버전으로 변환<br>
__@babel/preset-env__: Babel 지원 스펙을 지정<br>
__@babel/plugin-transform-runtime__: Async/Await 문법 지원<br>

__sass__: SCSS(Sass) 문법을 해석(스타일 전처리기)<br>
__postcss__: Autoprefixer 등의 다양한 스타일 후처리기 패키지<br>
__autoprefixer__: 스타일에 자동으로 공급 업체 접두사(Vendor prefix)를 적용하는 PostCSS의 플러그인<br>

__vue__: Vue.js 프레임워크<br>
__@vue/compiler-sfc__: .vue 파일(SFC, 3버전)을 해석<br>

__eslint__: 정적 코드 분석 도구 __(+ESLint)__<br>
__eslint-plugin-vue__: Vue.js 코드 분석 __(+ESLint)__<br>
__babel-eslint__: ES6 이상의 코드(Babel)를 분석 __(+ESLint)__<br>

__vuex__: 중앙 집중식 저장소 __(+Vuex)__<br>
__vue-router__: 라우터 __(+VueRouter)__<br>

## 주의사항!

- `npm i vue@next`로 설치(3버전)
- `npm i vue-loader@next`로 설치(3버전)
- `npm i -D webpack-dev-server@next`로 설치(webpack-cli 버전(@4^)과 일치)!<br>
- `package.json` 옵션으로 `browserslist` 추가!<br>
- `.postcssrc.js` 생성(PostCSS 구성 옵션)!<br>
- `.babelrc.js` 생성(Babel 구성 옵션)!<br>
- `.eslintrc.js` 생성(ESLint 구성 옵션)! __(+ESLint)__<br>

## ESLint Auto fix on save for VSCode

- 모든 명령 표시(Windows: `Ctrl`+`Shift`+`P` / macOS: `Cmd`+`Shift`+`P`)
- 모든 명령 표시에서 `settings` 검색
- `Preferences: Open Settings (JSON)` 선택
- 오픈된 `settings.json`파일에서 아래 코드 추가 및 저장

```json
{
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  }
}
```


https://www.googletagmanager.com/gtm.js?   GTM-T8B5P2

https://www.googletagmanager.com/gtag/js?id=G-4391KKZ1EB

