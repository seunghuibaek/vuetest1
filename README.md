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

ppknwebsvcacc : 6~pD$R(LH>}j9+wn
ppknapisvcacc : )dQGcX<?F6F{ncy!

회원 데이터 항목 중 CI 값은 DB에 기록하지 않도록 변경이 필요합니다.

이에 CI값 전달하는 부분을 빈문자열로 치환해서 SP 호출되도록 수정되어야 합니다.

대상 SP는 아래 3개입니다. SP명세서도 첨부합니다.

USP_Add_NewMmbrProcess_002
JBN_WEB_CertifyInfoSave_phone
JBN_WEB_CertifyInfoSave_ipin


USP_GetList_BrdcChtnDclrList_002
USP_Mod_NbkkRfmProcess_004
USP_Mod_NbkkRfmHndoprProcess_003


sendNumber = Trim(oJSON.data("SNDN"))
receiveNumber = Trim(oJSON.data("RCVN"))
receiveText = Trim(oJSON.data("TXT"))
TID = Trim(oJSON.data("TID"))

/AS/monitor/nabankSms.asp

USP_GetList_BrdcChtnDclrList_002
sndMsg  partnerCode
P-00001(봉봉이_)에 대한 방송 신고가 3회 접수되었습니다.	P-00001
P-00001(222dev)에 대한 방송 신고가 3회 접수되었습니다.	P-00001
P-00001(프론트웹팀02)에 대한 방송 신고가 3회 접수되었습니다.	P-00001

/AS/monitor/nabankSms.asp

USP_Mod_NbkkRfmHndoprProcess_003

naSchCastList.asp


1. 이벤트 명 : 7월 여름휴가 이벤트 !
2. 이벤트 기간 : 2023년 7월 1일 00시 00분 ~ 2023년 7월 7일 16시 59분 (약 7일간)
3. 진행 내용 :  점수 차등에 따른 인기MC/신입MC 각각 상위 10명에게 혜택지급
4. 기타 요청사항
 - 유의사항은 퍼블리싱 작업 요청 드립니다. 
 - '유료 방송 입장료'에 대해 일반 팝콘 점수로 산정 
 - 6월 랭킹이벤트와 점수기준 같으나 럭셔리 팝콘 종류만 변경
 - 점수기준 : (일반 팝콘(30%)*30%)*40 + (럭셔리 팝콘(30%)*30%)*40 + (이벤트 팝콘(30%)*30%)*40 + (추천 수(10%)*10%)*40 + 보너스점수(골드로즈 팝콘 (30%)*30%)*40
AS/svmonitor/serverMod.asp

SC_ST : C (채팅서버)
        L (영상서버)
-- 채팅서버
192.168.1.16
[B_CHATDATA].dbo.[USP_Mod_chatServerStatus]
-- 영상서버
[B_CASTDATA].dbo.[USP_Mod_liveServerStatus]

채팅
fromNum = "0262385000"
fromMsg = "[팝콘모니터] 채팅서버["&pk&"] "& isServicetxt &" 변경됐습니다." 
Call sendSMSKT("01094597918", Replace(fromNum,"-",""), fromMsg, Left(SERVER_NAME,16))'허재원
Call sendSMSKT("01056437222", Replace(fromNum,"-",""), fromMsg, Left(SERVER_NAME,16))'고경섭
Call sendSMSKT("01090959021", Replace(fromNum,"-",""), fromMsg, Left(SERVER_NAME,16))'김민순
영상
fromNum = "0262385000"
fromMsg = "[팝콘모니터] 영상서버["&pk&"] "& isServicetxt &" 변경됐습니다." 
Call sendSMSKT("01094597918", Replace(fromNum,"-",""), fromMsg, Left(SERVER_NAME,16))'허재원
Call sendSMSKT("01056437222", Replace(fromNum,"-",""), fromMsg, Left(SERVER_NAME,16))'고경섭

ch/setup/fan/management_04_01.asp

[재현절차]
- dev서버
- 열혈팬 리스트 중 휴면회원 有

1. 마이채널 > 관리 > 팬 관리
2. 팬리스트 확인 > 팬 리스트 중 휴면회원 확인


192.168.1.28

114.31.51.70
114.31.51.71

115				\\192.168.0.115\popkontv
213				\\192.168.0.14\popkontv
71
69				\\192.168.0.4\popkontv

103    \\192.168.0.103\popkontv    액세스 거부  
114    \\114.31.50.114\popkontv    계정 잠김. 로그온 할 수 없습니다
122    \\192.168.0.122\popkontv    연결안됨
123    \\192.168.0.123\popkontv    연결안됨
124    \\192.168.0.124\popkontv    연결안됨
247    \\192.168.0.247\popkontv    액세스 거부
248    \\192.168.0.248\popkontv    액세스 거부
66    \\192.168.0.1\popkontv       네트워크 경로 찾지 못함
67    \\192.168.0.2\popkontv      네트워크 경로 찾지 못함
69    \\192.168.0.4\popkontv    액세스 거부
99    \\192.168.0.99\popkontv    액세스 거부

?bmNowDate=2023-07-01%2003:50:00&bmMaxDate=2024

PC
커밋: 878d4171d697032e332c84d0fa20f0f80bb1356d [878d417]
상위 항목: 0fdcb84db9
작성자: 백승희 <sh.back@theenm.com>
날짜: 2023년 6월 27일 화요일 오후 5:27:58
커밋한 사람: 백승희
BestMc 최종 등록_6

커밋: 29f3ca8d1a2b502bf30306a30a20df1fd04dd5b2 [29f3ca8]
상위 항목: d170187842
작성자: 백승희 <sh.back@theenm.com>
날짜: 2023년 6월 27일 화요일 오후 5:27:21
커밋한 사람: 백승희
BestMc 최종 등록_6


https://www.jetbrains.com/ko-kr/idea/download/?section=windows
https://sys1.popkontv.kr:9002/AS/member/nasignAliveCheck.asp
