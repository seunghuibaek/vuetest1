USP_GetList_BrdcListUprExpsr_001

USP_GetList_BrdcListMainExpsr_001






[B_MEMBER].[dbo].[USP_GetListOAuthSvcSplr]


회원 인증 서비스 목록

SVC_SE_CD	SVC_NM
1	GOOGLE
2	KAKAO
3	NAVER
4	FACEBOOK
5	APPLE


exec USP_GetList_BrdcListUprExpsr_001 'P-00015', 10, 0, 'N', 'Y'


{"SC_CLT":1,"SC_CT":0,"SC_EP":7,"SC_IA":0,"SC_IAS":1,"SC_PC":"P-00015","SC_PN":1,"SC_PS":"","SC
_SCT":"","SC_SCTE":0,"SC_STYP":2}
https://devsys.popkontv.kr:9002/AS/castData/naViewCastList.asp

{"SC_AS":0,"SC_EP":7,"SC_PC":"P-00015"}
https://devsys.popkontv.kr:9002/AS/program/naPGexe.asp


보유지 -> 나유에
https://sys1.popkontv.kr:9002/AS/recVod/mcGrpVodList.asp

{"SC_TP":"0","SC_PN":1,"SC_IAC":"1","SC_PC":"P-00001","SC_VSI":"zkfkapfzhs","SC_VPC":"P-00001"}

{
  "mcGrpVodListData": {
    "rstCode": "0",
    "pageNum": "1",
    "totalPageNum": "4",
    "totalListNum": "77",
    "rstMsg": "SUCCESS"
  },
  "mcGrpVodList": [
    {
      "vodCode": "2104787",
      "vSetDate": "20240624152314",
      "vViewCnt": "970",
      "vRecommendCnt": "4",
      "vSignId": "zkfkapfzhs",
      "vCastTitle": "\uD551\uD06C\uC0C9\uCCB4\uD06C\uAD50\uBCF5",
      "vPartnerCode": "P-00001",
      "vNickName": "\uB098\uC720\uC5D0",
      "vPfileName": "https:\/\/pic.popkontv.com\/profile_thumb\/P-00001\/z\/zk\/zkfkapfzhs_P-00001_20200809192224.png"
    },
    ................
  ]
}

USP_Add_OauthMmbrRgst_002 : 셀럽티비 리뉴얼 배포시 비사용 처리(오브젝트 명세서 확인)
USP_GetList_LvlALLAdm_002 : 파트너사_코드 매개변수 필요
LHY_WEB_vodCategory_Listrandom : 클립 기능 배포시 비사용 처리(오브젝트 명세서 확인)


Case "0"
				targetURL = "http://news.mk.co.kr/cp/popcon/mbnstar.xml"
			Case "1"
				targetURL = "http://news.mk.co.kr/cp/popcon/sports.xml"
			Case Else
				targetURL = "http://news.mk.co.kr/cp/popcon/sports.xml"

{"SC_CT":0,"SC_SCT":"","SC_SCTE":"0","SC_PN":1,"SC_STYP":"2","SC_IA":"1","SC_EP":"9","SC_PC":"P-00001","SC_CLT":"0","SC_IAS":0} 
파라미터입니다. 
naViewCastList.asp
https://bts.rink.kr/issues/12432

https://devsys.popkontv.kr:9002/AS/castData/castMemberData.asp

{
  "SC_CT": "1",
  "SC_SI": "librestilo",
  "SC_PC": "P-00001",
  "SC_SP": "0xBAB302587F78ABC13D93B96AF9E93695A81D0145BA9E377319856D708FBCC4F0",
  "SC_CAT": "아바타 테스트",
  "SC_ADT": "0",
  "SC_IPVT": "1",
  "SC_PK": "asdf",
  "SC_LMN": "426",
  "SC_CTE": "10",
  "SC_CAPT": "9",
  "SC_CTYP": "5",
  "SC_TKC": "0",
  "SC_COS": "window",
  "SC_CLT": "0",
  "SC_IJ": "0",
  "SC_ICS": "N"
}

{
  "castMemberData": {
    "rstCode": "1",
    "rstMsg": "SC_FLV",
    "signId": "librestilo",
    "castTitle": "\uC544\uBC14\uD0C0 \uD14C\uC2A4\uD2B8",
    "isAdult": "0",
    "isPrivate": "1",
    "limitNumber": "426",
    "category": "10",
    "castPath": "9",
    "castType": "5",
    "fanLevel": "",
    "groupLevelNm_0": "",
    "groupLevelNm_1": "",
    "groupLevelNm_2": "",
    "groupLevelNm_3": "",
    "castListTarget": "0",
    "maxWatchCnt": "1000",
    "isJoint": "0",
    "isCastShare": "N",
    "passwordKey": "asdf",
    "tiketCoin": "0"
  }
}


https://docs.google.com/spreadsheets/d/1K6Y1xkoDaU14U_Qmo4MNrpz4zDZjE2u2kGdGRE6jjg0/edit?gid=0#gid=0

http://118.129.153.153/funnyfig_api

ppknapisvcacc 63 2812 저장 프로시저 'B_VOD.dbo.KJM_Content_commandExecute'을(를) 찾을 수 없습니다.
ppknapisvcacc 70 2812 저장 프로시저 'B_VOD.dbo.LHY_WEB_vodCategory_Listrandom'을(를) 찾을 수 없습니다.

B_VOD.dbo.LHY_WEB_vodCategory_Listrandom
118.129.153.91,9190

declare @output int
 exec [B_CASTDATA].[dbo].[USP_Mod_BrdcOnOff_004] 'bluewar96tv-20240625134902', 'bluewar96tv', '20240625135511', 0, 'rtmp://live-popkontv.hscdn.com/pop_cast20|bluewar96tv_P-00067_20240625134902'
 , 0, '', 'P-00067', 1,       @output output, 0, '', 0, 'PCP32bit'
 select @output;

SELECT *  
  FROM [B_COMPAY].dbo.castModeSet WITH(NOLOCK)  
  WHERE partnerCode = 'P-00067'; 
  '[B_COMPAY].dbo.castModeSet'
  


[B_CASTDATA].[dbo].[USP_GetList_CastOnListSrchForAPI_004]


{
  "SC_PCC": "bluewar96tv-20240625134902",
  "SC_SI": "bluewar96tv",
  "SC_PC": "P-00067",
  "SC_CST": "0",
  "SC_CAD": "rtmp://live-popkontv.hscdn.com/pop_cast20|bluewar96tv_P-00067_20240625134902",
  "SC_SP": "0x24AC6125195C85EE33FAD944F4A8DAB186200A0C2F27576481D5C45BAC18FA39",
  "SC_CLN": "1",
  "SC_CSQ": "",
  "SC_WTM": "0",
  "SC_VITC": "AC-0009",
  "SC_CR": "w1280h720e1",
  "SC_EB": "PCP32bit"
}


{
  "castOnData": {
    "rstCode": "SP",
    "rstMsg": "방송이 차단되어 있습니다.",
    "chatServerUrl": "https:\/\/dev.popkontv.kr:1920"
  }
}


https://sys1.96tv.co.kr:9002/AS/castData/naViewCastList.asp 
{"SC_CT":0,"SC_CLT":1,"SC_IAS":0,"SC_PC":"P-00067","SC_IA":1,"SC_SCT":"","SC_SCTE":0,"SC_EP":7,"SC_PN":1,"SC_STYP":1}



안녕하세요. 
명일 개발기 배포 예정인 DB 서비스 계정 비번 공유드립니다.

ppknapisvcacc  :  GUFzgx\7=h5rD24s


ppknwebsvcacc  :  P!#gs6=E8ZSDka3)
ppknapisvcacc  :  GUFzgx\7=h5rD24s
smsuser  :  hzaJrC2(5S$pT=B


복사 완료 하시고 말씀주시면 대화 삭제 하겠습니다.


Qortmdgml!@#

**06/18
API03 (114.141.29.117)
ASP-API06 (114.141.29.120)

06/19
API04 (114.141.29.118)
ASP-API07 (114.141.29.121)**


  "SC_PCC": "librestilo-20240613092408",
  "SC_SI": "librestilo",
  "SC_PC": "P-00001",
  "SC_CST": "2",
  "SC_CAD": "",
  "SC_SP": "123456",
  "SC_CLN": "",
  "SC_SEC": "1",
  "SC_CET": "3"
}

 
 
 declare @rtn int
 exec USP_Mod_BrdcOnOff_005  'bluewar111-20240612091542', 'bluewar111'
 , '20240612091911', 0, 'rtmp://live-popkontv.hscdn.com/pop_cast20|bluewar111_P-00001_20240612091542'
 , 0, '', 'P-00001', 3, @rtn output, 0, '', 0, '720x1280', 'AC-0009'
 select @rtn

1170067

 SELECT TOP 1 castType
  FROM dbo.castMemberData with(nolock)  
  WHERE signId = 'bluewar111'  AND partnerCode = 'P-00001';  


   DECLARE @dt2Rgstdt   DATETIME2(7)
   declare @ret int
    EXEC @ret = [192.168.1.24,9190].B_ITEM.dbo.USP_Mod_PrioSortGudsUse_002  
     @vchItemCd = 'AC-0009'  
     , @vchMmbri = 'bluewar111' 
     , @chrPrtsCd = 'P-00001'  
     , @vchBrdcCd  = 'bluewar111-20240612091542'
     , @insBrdcType = 0  
     , @dt2Rgstdt = @dt2Rgstdt output;  

	 select @ret, @dt2Rgstdt

     1160019

     ----------


[B_CASTDATA].[dbo].[USP_Mod_PrioSortGudsOnairUse_001]
[192.168.1.24,9190].B_ITEM.dbo.USP_Mod_PrioSortGudsUse_002 

1160018 = 사용할 수 있는 아이템이 없습니다.  



https://devsys.popkontv.kr:9002/AS/castData/castListUpUse.asp  
{
  "SC_PCC": "librestilo-20240611164908",
  "SC_SI": "librestilo",
  "SC_PC": "P-00001",
  "SC_BCT": "0",
  "SC_PGT": "3",
  "SC_VITC": "AC-0009"
}

res : {"castOnData":{"rstCode" : "SP","rstMsg" : "상품 설정에 오류가 있습니다."}}  


----------- Response --------------------
 URL:https://devsys.popkontv.kr:9002/AS/castData/naListupItemCnt.asp
 PARAMS:["SC_SP": "0xFB03C61F91D6ABA7F47514A48B3C1072E97BFC88AB1C6393E942C1AEC8CB0B09", "SC_SI": "popaos6", "SC_PC": "P-00001"] 
- Result -
 {"rst":{"rstCode" : "0","rstMsg" : "SUCCESS"}, "itemList":[{"itemcode": "AC-0009","iname": "LISTUP","cnt": 1,"onuse": "N"}]} 
-----------------------------------------

----------- Request ---------------------
 URL:https://devsys.popkontv.kr:9002/AS/castData/naListupItemCnt.asp
 PARAMS:["SC_SP": "0xFB03C61F91D6ABA7F47514A48B3C1072E97BFC88AB1C6393E942C1AEC8CB0B09", "SC_SI": "popaos6", "SC_PC": "P-00001"]
-----------------------------------------



----------- Response --------------------
 URL:https://devsys.popkontv.kr:9002/AS/castData/castOnData.asp
 PARAMS:["SC_PC": "P-00001", "SC_CR": "720x1280", "SC_SI": "popaos6", "SC_CAD": "rtmp://live-popkontv.hscdn.com/pop_cast20|popaos6_P-00001_20240611161400", "SC_VITC": "AC-0009", "SC_WTM": "0", "SC_CLN": "3", "SC_PCC": "popaos6-20240611161400", "SC_SP": "0xFB03C61F91D6ABA7F47514A48B3C1072E97BFC88AB1C6393E942C1AEC8CB0B09", "SC_CST": "0"] 
- Result -
 {"castOnData":{"rstCode" : "SP","rstMsg" : "상품 설정에 오류가 있습니다.","chatServerUrl" : "https:\/\/dev.popkontv.kr:1920"}} 
-----------------------------------------

URL:https://devsys.popkontv.kr:9002/AS/castData/castOnData.asp
 PARAMS:["SC_PC": "P-00001", "SC_CR": "720x1280", "SC_SI": "popaos6", "SC_CAD": "rtmp://live-popkontv.hscdn.com/pop_cast20|popaos6_P-00001_20240611161400", "SC_VITC": "AC-0009", "SC_WTM": "0", "SC_CLN": "3", "SC_PCC": "popaos6-20240611161400", "SC_SP": "0xFB03C61F91D6ABA7F47514A48B3C1072E97BFC88AB1C6393E942C1AEC8CB0B09", "SC_CST": "0"]


https://devsys.popkontv.kr:9002/AS/castData/naCastMainList.asp
 {"SC_DN":1,"SC_IA":1,"SC_LN":"","SC_LYN":"Y","SC_PC":"P-00001","SC_PN":1,"SC_PS":"15","SC_STYP":2}


 
URL:https://devsys.popkontv.kr:9002/AS/castData/castOnData.asp
 PARAMS:["SC_CR": "720x1280", "SC_CST": "0", "SC_PCC": "popios2-20240604161823", "SC_WTM": "0", "SC_CLN": "1", "SC_PC": "P-00001", "SC_SP": "0x269C2FE46D21EEB1278240D09F66A8748D89348EF4B34C363D1FC06C56D00DA1", "SC_SI": "popios2", "SC_CAD": "rtmp://live-popkontv.hscdn.com/pop_cast20|popios2_P-00001_20240604161823", "SC_VITC": ""]

 
https://devsys.popkontv.kr:9002/AS/castData/castOnData.asp

https://devsys.popkontv.kr:9002/AS/castData/castListUpUse.asp {"SC_PCC":"popaos7-20240604113228","SC_SI":"popaos7","SC_PC":"P-00001","SC_BCT":"0","SC_PGT":3,"SC_VITC":"AC-0009"}

[   Declare @return int
 exec  USP_Mod_BrdcOnOff_005  'librestilo-20240603172624', 'librestilo', 
 '20240603172711', 0, 'rtmp://live-popkontv.hscdn.com/pop_cast20|librestilo_P-00001_20240603172624',
 0, '', 'P-00001', 3,@return output, 0, '', 0, 'w1280h720e1', 'AC-0009'
 select @return](https://devsys.popkontv.kr:9002/AS/castData/castOnData.asp

{
  "SC_PCC": "librestilo-20240604090009",
  "SC_SI": "librestilo",
  "SC_PC": "P-00001",
  "SC_CST": "0",
  "SC_CAD": "rtmp://live-popkontv.hscdn.com/pop_cast20|librestilo_P-00001_20240604090009",
  "SC_SP": "0xBAB302587F78ABC13D93B96AF9E93695A81D0145BA9E377319856D708FBCC4F0",
  "SC_CLN": "3",
  "SC_CSQ": "",
  "SC_WTM": "0",
  "SC_VITC": "AC-0009",
  "SC_CR": "w1280h720e1",
  "SC_EB": "PCP32bit"
})


 메시지 515, 수준 16, 상태 2, 프로시저 USP_Mod_BrdcOnOff_005, 줄 404 [배치 시작 줄 30]
테이블 'B_CASTDATA.dbo.BrdcPrioSortGudsUseStatus', 열 'GudsExprtnDt'에 NULL 값을 삽입할 수 없습니다. 열에는 NULL을 사용할 수 없습니다. INSERT이(가) 실패했습니다.



/AS/castData/castOnData.asp
/castData/castListUpUse.asp

["SC_DN": "1", "SC_PC": "P-00001", "SC_PN": "1", "SC_STYP": "2", "SC_PS": "10", "SC_LN": "", "SC_IA": "N", "SC_LYN": "Y"] 

[B_CASTDATA].[dbo].[USP_Mod_BrdcOnOff_004]

{
  "SC_PCC": "librestilo-20240603134454",
  "SC_SI": "librestilo",
  "SC_PC": "P-00001",
  "SC_CST": "0",
  "SC_CAD": "rtmp://live-popkontv.hscdn.com/pop_cast20|librestilo_P-00001_20240603134454",
  "SC_SP": "0xBAB302587F78ABC13D93B96AF9E93695A81D0145BA9E377319856D708FBCC4F0",
  "SC_CLN": "3",
  "SC_CSQ": "",
  "SC_WTM": "0",
  "SC_CR": "w1280h720e1",
  "SC_EB": "PCP32bit"
}


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

