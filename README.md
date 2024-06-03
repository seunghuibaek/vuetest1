["SC_IA": "N", "SC_DN": "1", "SC_PN": "1", "SC_LYN": "Y", "SC_STYP": "2", "SC_PS": "0", "SC_LN": "", "SC_PC": "P-00001"]

https://devsys.popkontv.kr:9002/AS/castData/castOnData.asp

{
  "SC_PCC": "librestilo-20240603105915",
  "SC_SI": "librestilo",
  "SC_PC": "P-00001",
  "SC_CST": "0",
  "SC_CAD": "rtmp://live-popkontv.hscdn.com/pop_cast20|librestilo_P-00001_20240603105915",
  "SC_SP": "0xBAB302587F78ABC13D93B96AF9E93695A81D0145BA9E377319856D708FBCC4F0",
  "SC_CLN": "3",
  "SC_CSQ": "",
  "SC_WTM": "0",
  "SC_CR": "w1280h720e1",
  "SC_EB": "PCP32bit"
}


["SC_STYP": "2", "SC_DN": "1", "SC_PC": "P-00001", "SC_LYN": "0", "SC_LN": "", "SC_IA": "1"]

{"SC_PCC":"librestilo-20240531092943","SC_SI":"librestilo","SC_PC":"P-00001","SC_BCT":"0","SC_PGT":"3"}


{"rst":{"rstCode" : "0","rstMsg" : "SUCCESS"}, "itemList":[{"itemCode":"", "iName":"", "Cnt":"0", "OnUse": ""}]}
{"rst":{"rstCode" : "0","rstMsg" : "SUCCESS"}, "itemList":[{"itemcode": "AC-0009","iname": "LISTUP","cnt": 1,"onuse": "N"}]}



우선_정렬_상품_수량 조회합니다
 USP_Get_PrioSortGudsQty_002

 조회 내역이 없을 경우 
 기존 사용한 아이템의 OnUse 값이 필요
 

CASE PSGUD.BrdcType WHEN 0 THEN 'LIVE 방송'  
    WHEN 1 THEN '일대일'  
    WHEN 2 THEN '일대일'  
    WHEN 3 THEN '중계'  
    WHEN 4 THEN '녹화방송'  
    WHEN 5 THEN '일대다 그룹'  
    WHEN 6 THEN '일대다 일반'  
    WHEN 7 THEN '일대다 유료방송'  
    ELSE NULL END AS BrdcType  
   , CASE WHEN IM.OnuseYn = 'Y' THEN '적용중'  
    WHEN PSGUD.MngrRlsDt IS NOT NULL THEN '적용해제'
    

PPKNBRDCCACH(11)
[B_CASTDATA].[dbo].[USP_GetList_CastOnListSrchForAPI_004]  기존 메인

[B_CASTDATA].[dbo].[USP_GetList_BrdcListMainExpsr_001]  

/as/cache/exe/livemain.asp
/as/cache/exe/castlistmakeone.asp

192.168.1.80,9190
오류 번호 : 3704
내용 : 개체가 닫혀 있으면 작업이 허용되지 않습니다.

ppknapisvcacc

, @intPgSeCd  int    --// 결제대행사_구분_코드 :: [30001 : 케이지이니시스, 30002 : 케이지모빌리언스, 30003 : 다날, 30004 : 페이레터, 30005 : 헥토파이낸셜, 30006 : 갤럭시아머니트리]  
 , @nvcPgStorIdnt nvarchar(30) --// 결제대행사_상점_아이디  
 , @vchPgDelngNo  varchar(50)  --// 결제대행사_거래_번호  
 , @nvcPgDelngStatCd nvarchar(50) --// 결제대행사_거래_상태_코드   
 , @nvcPgRspnsCd  nvarchar(50) --// 결제대행사_응답_코드  
 , @vchSvcSiteUrl varchar(2083) --// 서비스_사이트_URL  
 
/AS/coin/buyCoin.asp
/AS/item/buyItem.asp


2024-05-13 03:44:07 192.168.1.124 POST /AS/push/getPushKeyInfo.asp |101|80004005|Transaction_(Process_ID_101)_was_deadlocked_on_lock_resources_with_another_process_and_has_been_chosen_as_the_deadlock_victim._Rerun_the_transaction. 9001 - 192.168.1.41 - - 500 0 0 5572 114.141.29.126


10.20.23.221
[B_PUSH].[dbo].[USP_GetList_PushKeySndngInfo_002]


theenm123!@#
theenm123!@#

AS/push/getPushKeyInfo.asp

----------- Response --------------------
 URL:https://stagesys.popkontv.com:9002/AS/member/registExe.asp
 PARAMS:["SC_PC": "P-00001", "SC_SCD": "0", "SC_AID": "2526526027", "SC_PN": "01071899608", "SC_NK": "닉네임입니다", "SC_SI": "", "SC_SP": "", "SC_EP": "15", "SC_ISA": "1"] 
- Result -
 {"rst":{"rstCode" : "1","rstMsg" : "사용할 수 없는 아이디 입니다.","signId" : "","signPwd" : ""}} 
-----------------------------------------


C:\Users\THE E&M\AppData\Roaming\npm
/ssi/global/dbPwdCng.asp


/AS/push/getPushKeyInfo.asp

USP_GetList_ItemPushKeySndngInfo_002 'librestilo', 'P-00001', 3, 500


.Parameters("@cast_signId") = cast_signId
		.Parameters("@cast_partnerCode") = cast_partnerCode
		.Parameters("@insDvcType") = insDvcType
		.Parameters("@intRecordCnt") = intRecordCnt


USP_GetList_ItemPushKeySndngInfo_002
{
  "rst": {
    "rstCode": "0",
    "rstMsg": "SUCCESS"
  },
  "strRst": [
    {
      "pk_code": "96",
      "pushKey": "eOUNgFWRUYw:APA91bF9nwT_J5VwDDxB_OPExxA9MR4DtltbbCl-mpjHiCiLHHfeEAGcmxUioYFyS-iLXagCU_mhvS8CPl3ttpdGwabnaZ2R0BjcF9ri-aSyp-zoKpiJmnL1hLy4oCKtu3HjMztr_Rh5",
      "deviceType": "7",
      "signId": "wocnd7333",
      "partnerCode": "P-00001",
      "offTimeStart": "2300",
      "offTimeEnd": "0900",
      "cast_signId": "qatest1019",
      "cast_partnerCode": "P-00001"
    }
  ]
}


${apiUrl}/AS/push/getPushItemKeyInfo.asp
librestilo
P-00001
3


USP_GetList_PushKeySndngInfo_002
USP_GetList_AnvrPushKeySndngInfo_002
USP_GetList_ItemPushKeySndngInfo_002

https://docs.google.com/spreadsheets/d/1tWB4-X1ul_tis2Ut-1iFxWBY2FGfP12l6LOZcs2QQRA/edit#gid=0

PUSH 발송자 조회중 오류 발생시  에러코드 :  1150001 반환하도록 하겠습니다.

/AS/push/getPushKeyInfo.asp 
/AS/push/getAnniversaryPushKeyInfo.asp
/AS/push/getPushItemKeyInfo.asp


https://devsys.popkontv.kr:9002/AS/member/levelFanData.asp

----------- Response --------------------
 URL:https://devsys.popkontv.kr:9002/AS/member/levelFanData.asp
 PARAMS:["SC_SP": "", "SC_CSI": "popaos6", "SC_IE": "0", "SC_SI": "", "SC_PC": "P-00001", "SC_CPC": "P-00001"] 
- Result -
 {"rst":{"rstCode" : "1","rstMsg" : "SC_SI", "lvl":"1", "nowExp":"0", "lvlupExp":"0", "lvlPer":"0"}} 
-----------------------------------------

----------- Request ---------------------
 URL:https://devsys.popkontv.kr:9002/AS/member/levelFanData.asp
 PARAMS:["SC_SP": "", "SC_CSI": "popaos6", "SC_IE": "0", "SC_SI": "", "SC_PC": "P-00001", "SC_CPC": "P-00001"]
-----------------------------------------



C:\Users\{$사용자}\AppData\Local\Atlassian\SourceTree.exe_Url_4ir5kstrwxmih14qvtxzf3dqvbfexoj2\3.1.2.3027
 Composition.cache 파일을 삭제

'에러로그 파일에 기록..
Dim Fso, LogPath, Sfile
Set Fso=CreateObject("Scripting.FileSystemObject")

LogPath = Server.MapPath ("/ErrHandler/log/Err") & date & ".log"


Set Sfile = Fso.OpenTextFile(LogPath,8,true)

Sfile.WriteLine "Date : " & now()
Sfile.WriteLine "Domain : " & Request.ServerVariables("HTTP_HOST")
Sfile.WriteLine "Browser : " & Request.ServerVariables("HTTP_USER_AGENT")

If Len(CStr(objError.ASPCode)) > 0 Then
Sfile.WriteLine "IIS Error Number : " & objError.ASPCode
End If

If Len(CStr(objError.Number)) > 0 Then
Sfile.WriteLine "COM Error Number : " & objError.Number & " (0x" & Hex(objError.Number) & ")"
End If

If Len(CStr(objError.Source)) > 0 Then
Sfile.WriteLine "Error Source : " & objError.Source
End If

If Len(CStr(objError.File)) > 0 Then
Sfile.WriteLine "File Name : " & objError.File
End If

If Len(CStr(objError.Line)) > 0 Then
Sfile.WriteLine "Line Number : " & objError.Line
End If

If Len(CStr(objError.Description)) > 0 Then
Sfile.WriteLine "Brief Description : " & objError.Description
End If

If Len(CStr(objError.ASPDescription)) > 0 Then
Sfile.WriteLine "Full Description : " & objError.ASPDescription
End If
Sfile.WriteLine chr(13)


Sfile.Close
Set Fso=Nothing
Set objError=Nothing


https://docs.google.com/spreadsheets/d/1mAING65kdHJS6bMPXuTaaKA1IghjZyZFwL2029_D7Nc/edit#gid=0

/AS/paper/paperSend.asp
  받는 사람 아이디를 확인해주세요

  https://theenmgw.daouoffice.com/app/todo/13419/card/214366

https://www.youtube.com/watch?v=CCpibp_Re7g

192.168.1.221
[B_PUSH].[dbo].[LJC_PUSH_pushKeyInfo_V2]
[B_PUSH].[dbo].[USP_GetList_PushKeySndngInfo_002]


API Server IP : 114.141.29.118


AS/push/getPushKeyInfo.asp |102|80004005|[DBNETLIB][ConnectionOpen_(Connect()).]SQL_Server가_없거나_액세스할_수_없습니다. 9001 - 192.168.1.41 - - 500 0 0 7 114.141.29.126
/AS/push/getPushKeyInfo.asp |102|80004005|지정되지_않은_오류입니다. 9001 - 192.168.1.41 - - 500 0 0 8 114.141.29.126
AS/push/getPushKeyInfo.asp |102|80004005|로그인_시간_제한이_만료되었습니다. 9001 - 192.168.1.34 - - 500 0 0 7 114.141.29.126
AS/push/getPushKeyInfo.asp |102|80004005|[DBNETLIB][ConnectionOpen_(Connect()).]SQL_Server가_없거나_액세스할_수_없습니다. 9001 - 192.168.1.41 - - 500 0 0 7 114.141.29.126


[B_PUSH].[dbo].[LJC_PUSH_pushKeyInfo_V2]
192.168.1.221

/AS/push/getPushKeyInfo.asp

{"statusCode":500,"body":"내부 서버 오류가 발생했기 때문에 페이지를 표시할 수 없습니다.","headers":{"cache-control":"no-cache,private","pragma":"no-cache","content-type":"text/html","expires":"Thu, 02 May 2024 01:57:26 GMT","server":"","x-aspnet-version":"","x-powered-by":"","date":"Thu, 02 May 2024 01:58:47 GMT","connection":"close","content-length":"87"},"request":{"uri":{"protocol":"http:","slashes":true,"auth":null,"host":"sys1.popkontv.kr:9001","port":"9001","hostname":"sys1.popkontv.kr","hash":null,"search":null,"query":null,"pathname":"/AS/push/getPushKeyInfo.asp","path":"/AS/push/getPushKeyInfo.asp","href":"http://sys1.popkontv.kr:9001/AS/push/getPushKeyInfo.asp"},"method":"POST","headers":{"content-type":"application/x-www-form-urlencoded","content-length":118}}}
[2024/05/02 10:58:29] 



http://news.mk.co.kr/cp/popcon/mbnstar.xml
http://news.mk.co.kr/cp/popcon/sports.xml


2209656
[Web발신]KB606401**772 입출금통지수수료  2700 원 05.02 부과예정입니다 .

CMD 
 
경로 이동 :  c:\windows\system32\inetsrv\  
 
appcmd list site > c:\sites.txt

https://docs.google.com/spreadsheets/d/1GdL9EmI5g3sm8diL2TIBIoJiKJxXq-KOttANFIbxAkY/edit#gid=2063274356


{"SC_PC":"P-00001","SC_SI":"popaos6","SC_SP":"0xFB03C61F91D6ABA7F47514A48B3C1072E97BFC88AB1C6393E942C1AEC8CB0B09"}
https://devsys.popkontv.kr:9002/AS/castData/naListupItemCnt.asp


sys1 [B_VOD].[dbo].[LHY_WEB_VodList_search]

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

