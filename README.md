/AS/castData/lbaVodList.asp

SC_PC : 파트너코드
SC_IA : 성인여부 (0 또는 1)
SC_GP : 그룹코드(정수형)
SC_CT : 카테고리(정수형)
SC_STYP : 정렬(0:랜덤, 1:최신순, 2:조회순, 3:추천순)
SC_PN : 페이지 번호
SC_PS : 노출 페이지 수


/AS/castData/lbaVodStdInfo.asp   SC_PC: 파트너코드


PPKNVODINFO
192.168.1.91
192.168.1.14

B_VOD
USP_GetList_PrtsVodStdrInfo_001		파트너사_VOD_기준_정보 조회합니다.

USP_GetList_PrtsVodList_001		파트너사_VOD_목록 조회합니다.

USP_Get_PrtsVodListDtl_001		파트너사_VOD_목록_상세 조회합니다.



118.129.153.82(게시판,관리자/AD(9)
exec USP_Get_PrtsSvcSiteInfo_002 @partnerCode = 'P-00074'
SITE_PC_URL
SITE_MOBILE_URL



/AS/recVod/naVodMain.asp [4-1] VOD 메인 방송목록
/AS/castData/cateGrpVodList.asp [5-6] VOD 카테고리 데이터 목록(신규)  요거
  [B_VOD].[dbo].[LHY_cateGrpVodList]   118.129.153.88,9190
/AS/recVod/naMcGrpList.asp [4-2] VOD-개인방송 방송자목록


API
/AS/castData/cateGrpVodList.asp [5-6] VOD 카테고리 데이터 목록(신규)  요거
  [B_VOD].[dbo].[LHY_cateGrpVodList]   118.129.153.88,9190
WEB
[B_VOD].[dbo].[LHY_WEB_VodList]   118.129.153.91,9190

USP_Get_RnkgEvntExpsrEnnc_001
USP_GetList_RnkgEvntSmmResult_001
USP_GetList_RnkgEvntImag_001
USP_GetList_RnkgEvntSmmTgtBnsCashGuds_001

RANK
EvntSeq - 이벤트_순번
Mmbri - 회원아이디
nickName
PrtsCd,- 파트너사_코드
TtlScor - 토탈점수
GnrlCashGudsScor - 일반 팝콘 점수
GnrlCashGudsTariff - 일반 팝콘 적용 요율
LxryCashGudsScor - 럭셔리 팝콘 점수
LxryCashGudsTariff - 럭셔리 팝콘 적용 요율
EvntCashGudsScor - 이벤트 팝콘 점수
EvntCashGudsTariff - 이벤트 팝콘 적용 요율
RcmnScor - 추천 점수
RE.RcmnTariff - 추전 적용 요율
BnsScor 보너스 점수
BrdcHhMinScor - 방송시간 점수 (차후 적용될지 몰라 사전 적용 현재 사용X)
BrdcHhMinTariff - 방송시간 요율 (차후 적용될지 몰라 사전 적용 현재 사용X)
pFileName,
pTitle
castStatus
castStartDateCode

JBN_WEB_CoinAccount
JBN_WEB_coinAccount_channel
JBN_WEB_CoinItemAccount 
JBN_WEB_coinItemAccount_Cancel
JBN_WEB_LCoinItemAccount
JBN_WEB_LCoinItemAccount_cancel
JBN_coinAccountLog_Insert


                                        PW                  MW              API
JBN_WEB_CoinAccount                     49                  18(SSM_GalaxiaPhone_insert(폰결제), JTW_GalaxiaBank_insert(무통장),JTW_GalaxiaCard_insert)              4(결제시 코인지급 SP. 모든 결제시)
JBN_WEB_coinAccount_channel                                                 1(SSM_partnerPoint_insert)
JBN_WEB_CoinItemAccount                 25                  17              3
JBN_WEB_coinItemAccount_Cancel
JBN_WEB_LCoinItemAccount                28                  17(JTW_GalaxiaTicket_insert,JTW_GalaxiaBank_insert,SSM_GalaxiaPhone_insert,KJH_GalaxiaTMoney_insert)              3(인앱결제(JBN_inAppPurchaseAOS_insert, JBN_inAppPurchaseIOS_insert))
JBN_WEB_LCoinItemAccount_cancel
JBN_coinAccountLog_Insert               3                   3(랜딩페이지를 통한 가입시 무료 팝콘 지급)         



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

--최종 로그인일시 를 365일로 변경
UPDATE B_MEMBER.dbo.memberPublic
SET loginDate=CONVERT(VARCHAR(10),DATEADD(DAY,-365,GETDATE()),121),
	passModiAfter = 0,
	passModiDate = CONVERT(VARCHAR(10),DATEADD(DAY,-120,GETDATE()),121)
WHERE signId = '회원아이디' AND parnterCode = '파트너사코드'

--Agent실행일과 loginDate 날짜 차이가 365일에 해당하는 회원 > 개인정보 분리 & loginAfterYear=1변경
EXEC B_MEMBER.dbo.UAP_Add_PrsninfoSprt_001
오후 04:58


테스트 계정의 logindate 를 변경해서  오늘 기준 365일 이전 
B_MEMBER.dbo.UAP_Add_PrsninfoSprt_001 를 실행하면 휴면으로 해당 아이디가 변경됩니다.
해보세요
오후 04:59


DECLARE @cnt int
DECLARE @rtn int
EXEC @rtn = usp_UpdatePrice -0.1, 'CE', @cnt OUTPUT

SELECT @cnt AS 업데이트, @rtn AS 오류

B_MEMBER.dbo.USP_GetListOAuthSvcSplr 

 SELECT TOP 1  
  M.*, ISNULL(P.pFileName, '') AS 'pFileName',ISNULL(C.SVC_SE_CD,0) as SVC_SE_CD  
 FROM [B_MEMBER].dbo.memberPublic M WITH(NOLOCK)  
  INNER JOIN memberPage P WITH(NOLOCK) ON M.signId = P.signID  AND M.partnerCode = P.partnerCode  
  Left Outer Join [OAUTH_USR] as C on M.signId=C.MMBRI  
 WHERE M.signId = 'bluewar111'
  AND M.partnercode = 'P-00001'
  AND M.isserviceclose = 0  
 ORDER BY pk_code DESC  


 JBN_WEB_memberPublicSearch


 https://devw.popkontv.com/event/202307Reward/?t=15012985

 ' 선물 팝콘 갯 수 100% 기준 14,512,985 hCnt
    ' 선물 팝콘 갯 수 초과 기준 15,204,079 oCnt 
 

 [B_BOARD].[dbo].[JBN_WEB_serviceCounsel_List] 
 118.129.153.82
 192.168.1.82

 categoryTitle



 SELECT top 100 * FROM [B_MANAGER].[dbo].[castLogSum] with(nolock)
  where signid = 'bluewar111'
  order by pk_code desc

  update [B_MANAGER].[dbo].[castLogSum] set registDateCode = '20230705095445'
  where pk_code = 7607895 and signid = 'bluewar111'

  update [B_MANAGER].[dbo].[castLogSum] set premiumGiftCoin = 5000
  where pk_code = 7607895 and signid = 'bluewar111'
  
update [B_MANAGER].[dbo].[castLogSum] set liveGiftCoin = 15000
  where pk_code = 7607895 and signid = 'bluewar111'

  update [B_MANAGER].[dbo].[castLogSum] set vodGiftCoin = 15000
  where pk_code = 7607895 and signid = 'bluewar111'


- 삭제 컬럼명: SatBankVrAcuntPwd, StlbnkVrAcunt010Pwd

- 개인정보_암호_키 컬럼명: StlbnkPrsninfoPsswrdKey, StlbnkVrAcunt010PrsninfoPsswrdKey

KJH_CheckCompanyPGInfo
https://gitlab.theenm.com/Develop1/popkondp.git


체 연동 관련 URL변경으로 인해 팝콘TV ok캐시백 연동 작업을 요청 드립니다.

https://pg.aronhub.com/docs/ocb_use.asp
연동 방법의 경우 위 URL 참고해주시기 바랍니다.

*OCB : 통신URL 변경 후 사용가능 
 - https://api.aronhub.com/api/ocb/PocbStart.asp
SID : 90588615 
연동 작업 부탁드립니다.


https://www.popkontv.com/item/ocb/return_buy_ocb.asp?USER_ID=bluewar111&USER_IP=175.196.87.168&ITEM_NAME=FULL%20VIEW%207%20DAY&ITEM_CODE=AB-0001&AMOUNT=1100&ITEM_COUNT=0&ORDER_ID=M-20230711144451667-2246C07B&SID=90588615&USERID=bluewar111&PAYPOINT=1000&EVENTPOINT=0&REPLYCODE=000000&MCTTRNO=20230711144459

개발기 서비스DB user 비번변경 관련 아래 서버 확인 부탁드립니다.
[클라이언트: 114.141.29.108]

2023-07-11 15:21:45.230 Logon Login failed for user 'ppknwebsvcacc'. 원인: 암호가 제공된 로그인의 암호와 일치하지 않습니다. [클라이언트: 114.141.29.108]

호출 API : 5.1 [검색-VOD] VOD 목록 (castData/naSchCateVodList_new.asp)
호출값 : {"SC_GP":1,"SC_IA":1,"SC_PC":"P-00001","SC_PN":1,"SC_SCTE":0,"SC_SS":"팝콘","SC_STYP":1}


 1) URL : https://api.aronhub.com/api/ocb/PocbCancel.asp
    2) 방식 : POST
    3) 파라미터 : (*) 필수 항목
        - (*) SID : 고객사코드
        - (*) TXNO : OCB 거래번호
    4) 결과(브라우저 출력)
        - 취소성공 : 000000, 취소실패 : 000000 을 제외한 값(실패 오류 코드값)
        - 

The server principal "sadmusr" is not able to access the database "ZDBMNGR" under the current security context.

M-20230717103339810-93EC9698
M-20230717111308410-EF4E450A

댓글/답글 삭제 : /castData/cateVodCommentDel.asp [5-11]
목록 : /castData/castVodCommentList.asp [5-10]

- 답글 클릭 시 : /castData/cateVodCommentList.asp [5-10]
전달 파라미터 : {"SC_CC":"20536","SC_PC":"P-00001","SC_PN":1,"SC_RF":"46341","SC_ST":2,"SC_STYP":0}
에러 : callbackId: VOD_COMMENT_LIST / decodeResponse : 500

- 삭제 클릭 시 : /castData/cateVodCommentDel.asp [5-11]
전달 파라미터 : {"SC_CK":"46338","SC_PC":"P-00001","SC_SI":"popaos5","SC_SP":"0xF76A56933DD7E3CDE5B60B0E0FC4DFFB98DE897E1B689B765634620AC6E2357E"}
에러 : callbackId: VOD_COMMENT_DELETE / decodeResponse : 500

JBN_MANAGER_memberSignStatusCheck
JBN_MANAGER_memberSignStatusInit
JBN_memberSignStatus_Update_statusType
SSM_memberSignStatus_search
SSM_memberSignStatus_signAliveCheck

https://www.googletagmanager.com/gtm.js?   GTM-T8B5P2

https://www.googletagmanager.com/gtag/js?id=G-4391KKZ1EB

