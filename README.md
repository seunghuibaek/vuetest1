<!--#include virtual="/ssi/global/page_init.ssi"-->
<!--#include virtual="/ssi/function/aes_func.ssi"-->
<!--#Include Virtual="/ssi/function/domainallow.ssi"-->
<!--#Include Virtual="/ssi/function/ZonePlayerUtils.asp"-->
<!--#include virtual="/ssi/function/chatUtil.asp"-->
<%
'에러 무시 활성
'On Error Resume Next

'#### 2016.09.13
'#### SSM
'#### /castData/naCastWatchOnOff.asp

'--# 서비스 점검체크
'# IS_SERVER_SERVICE
'> true:서비스실행, false:서비스 점검
'# 수동전체 점검체크
If Not IS_SERVER_SERVICE Then
	Call resultJsonSet("E","서비스 정기점검중 입니다.")
End If
'//

'--# server value
Dim castAddress
Dim accountLevel
Dim fanLevel
Dim fanLevelName
Dim groupLevelNm
Dim fanLevelGiftCoin
Dim castFanLevel
Dim needCoin
Dim coin
Dim chatServerType
Dim castAddressArr
Dim chatAddress
Dim memberSex
Dim nickName
Dim castCastType
Dim isUpdate
Dim vTK
Dim isAdultCheck
Dim castisAdult
Dim castcategory
Dim isJoint
Dim itemlist
Dim isGifter
Dim groupLevelNm_0
Dim groupLevelNm_1
Dim groupLevelNm_2
Dim groupLevelNm_3
castAddress = ""
accountLevel = ""
fanLevel = ""
fanLevelName = ""
groupLevelNm = ""
fanLevelGiftCoin = ""
castFanLevel = 4
needCoin = ""
coin = ""
chatServerType = ""
castAddressArr = ""
chatAddress = ""
memberSex = ""
nickName = ""
castCastType = ""
isUpdate = 0
vTK = ""
isAdultCheck = 0
isJoint = 0
itemlist = ""
isGifter = 0
groupLevelNm_0 = "VIP"
groupLevelNm_1 = "다이아몬드"
groupLevelNm_2 = "골드"
groupLevelNm_3 = "실버"
Dim playerType	'0' : ExoPlayer, '1': VXGPlayer
'//

'--# Request
'# data
Dim Data, oJSON
dim key
dim aesver
Data = Trim(Request.form("data"))
key = Trim(Request.form("key"))
aesver = Trim(Request.form("v"))
Data = aesvalidate(Data, key, aesver)
Set oJSON = new aspJSON
oJSON.loadJSON(data)
'# request
Dim signId
Dim signPwd
Dim partnerCode
Dim cast_signId
Dim cast_partnerCode
Dim commandType
Dim castCode
Dim castType
Dim exePath
Dim password
Dim version
Dim androidStore
Dim isSecret
signId = Trim(oJSON.data("SC_SI"))
signPwd = Trim(oJSON.data("SC_SP"))
partnerCode = Trim(oJSON.data("SC_PC"))
cast_signId = Trim(oJSON.data("SC_CSI"))
cast_partnerCode = Trim(oJSON.data("SC_CPC"))
commandType = Trim(oJSON.data("SC_CT"))
castCode = Trim(oJSON.data("SC_PCC"))
castType = Trim(oJSON.data("SC_CTYP"))
exePath = Trim(oJSON.data("SC_EP"))
password = Trim(oJSON.data("SC_PK"))
version = Trim(oJSON.data("SC_VER"))
androidStore = Trim(oJSON.data("SC_AS"))
isSecret = Trim(oJSON.data("SC_ISCR"))
Set oJSON = nothing
'//

'--# Request Check
'# signId
If Not paramChk_signId(signId) Then
	Call resultJsonSet("1","SC_SI")
End If
'# signPwd
If Not isStringLen(signPwd,4,255) Then
	call resultJsonSet("1","SC_SP")
End If
'# partnerCode
If Not paramChk_partnerCode(partnerCode) Then
	Call resultJsonSet("1","SC_PC")
Else
	partnerCode = UCase(partnerCode)
End If
'# cast_signId
If Not paramChk_signId(cast_signId) Then
	Call resultJsonSet("1","SC_CSI")
End If
'# cast_partnerCode
If Not paramChk_partnerCode(cast_partnerCode) Then
	Call resultJsonSet("1","SC_CPC")
Else
	cast_partnerCode = UCase(cast_partnerCode)
End If
'# commandType(0:방송시청,1:방송시청종료)
If not paramChk_bit(commandType) then
	Call resultJsonSet("1","SC_CT")
Else
	commandType = CInt(commandType)
End if
'# castCode
If Not paramChk_castCode(castCode) Then
	Call resultJsonSet("1","SC_PCC")
End If
'# castType
If Not paramChk_smallInt(castType) then
	call resultJsonSet("1","SC_CTYP")
Else
	castType = CInt(castType)
End If
If castType < 0 Or castType > 8 Then
	call resultJsonSet("1","SC_CTYP")
End if
'# exePath (0:etc, 1:Android, 2:iPhone, 3:iPhone Enterprise(flex), 4:PC P/G, 5:PC WEB, 6:mobile WEB, 7:native andriod, 8:native iPhone, 9:신규PC, 12:맥 PC) 
'# exePath 추가 (15: 통합 로그인 앱스토어 기업 프로그램 IOS 앱, 16: 통합 로그인 앱스토어 IOS 앱, 17: 통합 로그인 구글플레이 안드로이드 앱, 18: 통합 로그인 원스토어 안드로이드 앱)
If Not paramChk_path(exePath) Then
	Call resultJsonSet("1", "SC_EP")
Else
	exePath = CInt(exePath)
End If
'# version
If Not IsNumeric(Replace(version,".","")) Then
	Call resultJsonSet("1","SC_VER")
End If
'#password'
if len(password) > 10 then
	call resultJsonSet("E1","비밀번호가 일치하지 않습니다.")
end if
'--# 방송자와 시청자 동일 아이디 시청 불가
If lcase(signId) = lcase(cast_signId) and partnerCode = cast_partnerCode then
	call resultJsonSet("1","시청할 수 없는 방송입니다.")
End if

'# androidStore (0:googleplay, 1:OneStore)'
if androidStore = "" then
	androidStore = 0
end if
If Not isNumKey(androidStore) Then
	Call resultJsonSet("1", "SC_AS")
Else
	androidStore = CInt(androidStore)
End If

'# isSecret(0:시크릿모드 끔,1:켬)
If not paramChk_bit(isSecret) then
	isSecret = 0	
Else
	isSecret = CInt(isSecret)
End if
'// 

'--# 파트너사 정보
Call PAGE_INIT(partnerCode)
'//
'# 파트너 점검체크
If Not IS_SERVER_SERVICE Then
	Call resultJsonSet("E","서비스 정기점검중 입니다.")
End if

'--# 회원로그인정보 확인 (true:성공, false:실패)
if Not idPwdCheck(signId, signPwd, partnerCode) Then
	call resultJsonSet("E2","IPC")
End If
'//

'--# ADO open
Dim objCmd, cmdRtnCode, cmdRs
Set objCmd = server.CreateObject("ADODB.COMMAND")
'//

'--# 방송시청 권한 설정
'# accountLevel (0:일반시청자, 1:방송자, 2:매니저, 3:운영자, 4:관리자)
with objCmd
	Call cmdPramDel(objCmd)
	cmdRtnCode = ""
	.commandText = "[B_CASTDATA].[dbo].[JBN_JSON_castWatchOn_Step1_LisenceCheck]"
	.commandType = &H0004
	.activeConnection = OLEDB_CTICAST9
	.Parameters.Append .CreateParameter("@cast_signId", adVarChar, adParamInput, 25)
	.Parameters.Append .CreateParameter("@watch_signId", adVarChar, adParamInput, 25)
	.Parameters.Append .CreateParameter("@cast_partnerCode", adVarChar, adParamInput,7)
	.Parameters.Append .CreateParameter("@watch_partnerCode", adVarChar, adParamInput,7)
	.Parameters.Append .CreateParameter("@return", adInteger, adParamOutput, 10)
	.Parameters("@cast_signId") = cast_signId
	.Parameters("@watch_signId") = signId
	.Parameters("@cast_partnerCode") = cast_partnerCode
	.Parameters("@watch_partnerCode") = partnerCode
	.Parameters("@return") = 0
	.execute()
	accountLevel = .parameters("@return")
End With
'// 

'--# 방송자/운영자 파트너별 제한
If accountLevel = 3 Or accountLevel = 4 Then
	If cast_partnerCode <> partnerCode and partnerCode <> "P-00001" then
		call resultJsonSet("E3","해당 아이디는 방송시청이 불가능 합니다.")
	End if
End if
'//
'--# 버전업데이트 심의상태 여부 (0:정상서비스상태, 1:버전업데이트심의상태)
if exePath = 7 Or exePath = 18 Or exePath = 19 then
	Select Case exePath
		Case 7
			isUpdate = IS_AOS_SIMSA
			' 심사용 버전 있을 경우 해당 버전과 일치 하지 않으면 심사중 해제
			if not isnull(NATIVE_ANDROID_VERSION_SIMSA) and NATIVE_ANDROID_VERSION_SIMSA <> "" and NATIVE_ANDROID_VERSION_SIMSA <> version then
				isUpdate = 0
			end if
		
		Case 18
			isUpdate = RnkPlusOnestorInspPrgrYn
			If Not IsNull(RnkPlusOnestorInspVer) And RnkPlusOnestorInspVer <> "" And RnkPlusOnestorInspVer <> version Then
				isUpdate = 0
			End If
		Case 19
			isUpdate = RnkPlusGlxstorInspPrgrYn
			If Not IsNull(RnkPlusGlxstorInspVer) And RnkPlusGlxstorInspVer <> "" And RnkPlusGlxstorInspVer <> version Then
				isUpdate = 0
			End If
	End Select
	'if partnerCode = "P-00001" and (version = "4.0.3" or version = "4.0.4") then
	''	isUpdate = 0
	'end if
elseif exePath = 8 then
	isUpdate = IS_IOS_SIMSA
end if
'//

'--# 시청신호처리
'# commandType (0:방송시청, 1:방송시청종료)
If commandType = 0 Then
	'--# 프로그램 버전체크
	Select Case exePath
	'# android
	Case 1
		If not versionCompare(version, ANDROID_VERSION) Then
			call resultJsonSet("V","프로그램 업데이트가 필요합니다. 프로그램을 새로 다운받아 설치하시기 바랍니다.")
		End If
	'# IOS
	Case 2
		If not versionCompare(version, IOS_VERSION) Then
			call resultJsonSet("V","프로그램 업데이트가 필요합니다. 프로그램을 새로 다운받아 설치하시기 바랍니다.")
		End If
	'# IOSE
	Case 3
		If not versionCompare(version, IOSE_VERSION) Then
			call resultJsonSet("V","프로그램 업데이트가 필요합니다. 프로그램을 새로 다운받아 설치하시기 바랍니다.")
		End If
	'# PC
	Case 4
		If not versionCompare(version, PC_VERSION) Then
			call resultJsonSet("V","프로그램 업데이트가 필요합니다. 프로그램을 새로 다운받아 설치하시기 바랍니다.")
		End If
	'# native Android
	Case 7
		If not versionCompare(version, NATIVE_ANDROID_VERSION) Then
			call resultJsonSet("V","프로그램 업데이트가 필요합니다. 프로그램을 새로 다운받아 설치하시기 바랍니다.")
		End If
	'# native iPhone
	Case 8
		If not versionCompare(version, NATIVE_IPHONE_VERSION) Then
			call resultJsonSet("V","프로그램 업데이트가 필요합니다. 프로그램을 새로 다운받아 설치하시기 바랍니다.")
		End If
	'# PC NEW
	Case 9
		Dim objRs, cmdTxt
		Set objRs = server.CreateObject("ADODB.RECORDSET")
		' 플레이어 정보는 P-00001로 통일
		cmdTxt = "EXEC [B_COMPANY].[dbo].[USP_Get_PrtsSvcSiteInfo_002] @partnerCode='P-00001'"
		objRs.open cmdTxt, OLEDB_CAST4, 1
		If Not objRs.eof Then	
			PC_WIN_VERSION = trim(objRs("PC_WIN_VERSION"))
		End If 
		objRs.close
		set objRs = nothing
		
		If not versionCompare(version, PC_WIN_VERSION) Then
			call resultJsonSet("V","프로그램 업데이트가 필요합니다. 프로그램을 새로 다운받아 설치하시기 바랍니다.")
		End If
	'# PC NEW
	Case 12
		If not versionCompare(version, PC_MAC_VERSION) Then
			call resultJsonSet("V","프로그램 업데이트가 필요합니다. 프로그램을 새로 다운받아 설치하시기 바랍니다.")
		End If
	'# IOSE NEW / 린크_플러스_앱스토어_기업_프로그램
	Case 15
		If not versionCompare(version, RnkPlusAppstorEntrPgmVer) Then
			call resultJsonSet("V","프로그램 업데이트가 필요합니다. 프로그램을 새로 다운받아 설치하시기 바랍니다.")
		End If
	'# native iPhone NEW / 린크_앱스토어
	Case 16
		If not versionCompare(version, RnkAppstorVer) Then
			call resultJsonSet("V","프로그램 업데이트가 필요합니다. 프로그램을 새로 다운받아 설치하시기 바랍니다.")
		End If
	'# AOS 구글플레이 NEW / 린크_구글플레이
	Case 17
		If not versionCompare(version, RnkGglplyVer) Then
			call resultJsonSet("V","프로그램 업데이트가 필요합니다. 프로그램을 새로 다운받아 설치하시기 바랍니다.")
		End If
	'# AOS 원스토어 NEW / 린크_플러스_원스토어
	Case 18
		If not versionCompare(version, RnkPlusOnestorVer) Then
			call resultJsonSet("V","프로그램 업데이트가 필요합니다. 프로그램을 새로 다운받아 설치하시기 바랍니다.")
		End If
	'# 린크_플러스_갤럭시스토어
	Case 19
		If not versionCompare(version, RnkPlusGlxstorVer) Then
			call resultJsonSet("V","프로그램 업데이트가 필요합니다. 프로그램을 새로 다운받아 설치하시기 바랍니다.")
		End If
	'# 린크_플러스_안드로이드_수동_다운로드_앱
	Case 20
		If not versionCompare(version, RnkPlusAndrdPssivDwnlAppVer) Then
			call resultJsonSet("V","프로그램 업데이트가 필요합니다. 프로그램을 새로 다운받아 설치하시기 바랍니다.")
		End If
	End Select
	'//
	
	'--# 로그인 차단확인
	'# @return (-1:성공, 0:영구정지, n:해당일정지)
	with objCmd
		Call cmdPramDel(objCmd)
		cmdRtnCode = -2				
		.commandText = "[B_MEMBER].[dbo].[JBN_JSON_signOn_Step2_BlockCheck_DDD]"
		.commandType = &H0004
		.activeConnection = nothing
		.activeConnection = OLEDB_CAST
		.Parameters.Append .CreateParameter("@signId", adVarChar, adParamInput, 25)
		.Parameters.Append .CreateParameter("@partnerCode", adVarChar, adParamInput, 7)
		.Parameters.Append .CreateParameter("@return", adInteger, adParamOutput)	
		.Parameters("@signId") = signId
		.Parameters("@partnerCode") = partnerCode
		.Parameters("@return") = cmdRtnCode
		.execute()
		cmdRtnCode = .parameters("@return")
	End With
	if err.number <> 0 then
		call resultJsonSet("1","일시적인 오류로 서비스 점검중 입니다.")
	end if		
	Select Case (cmdRtnCode)		
		Case -2
			call resultJsonSet("1","일시적인 오류로 서비스 점검중 입니다.")
		Case -1
		Case 0
			call resultJsonSet("E4","회원님은 운영정책에 위반되는 방송진행으로 영구정지 되셨습니다. 추가로 소명이 필요하신 부분이 있으시면 일대일문의를 부탁드립니다.")
		Case Else
			call resultJsonSet("E4","회원님은 운영정책에 위반되는 방송진행으로 " & cmdRtnCode & "일정지 되셨습니다. 정지기간 중 다른 계정으로 방송 시 영구정지가 될 수 있습니다.")
	End select
	'//

	'--# 방송코드 존재확인 (true:존재, false:미존재) 
	If Not castUseCheck(castCode) Then
		call resultJsonSet("E5","방송이 존재하지 않습니다.")
	End If
	with objCmd
		Call cmdPramDel(objCmd)
		cmdRtnCode = ""
		.commandText = "[B_CASTDATA].[dbo].[USP_GetList_CastInfoForAPI_003]"
		.commandType = &H0004
		.activeConnection = nothing
		.activeConnection = OLEDB_CTICAST2 
		.Parameters.Append .CreateParameter("@signId", adVarChar, adParamInput, 25)
		.Parameters.Append .CreateParameter("@partnerCode", adVarChar, adParamInput, 7)
		.Parameters("@signId") = cast_signId
		.Parameters("@partnerCode") = cast_partnerCode
		Set cmdRs = .execute()
	End With
	If cmdRs.eof Then
		call resultJsonSet("1","방송이 존재하지 않습니다.")
	Else
		chatServerType = cmdRs("chatType")
		castAddress = cmdRs("castAddress")
		castAddressArr = Split(castAddress,"|")
		'RTC 방송 시청 제한'
		if left(castAddress, 4) <> "rtmp" and not(exePath = 3 or exePath = 7 or exePath = 15 or exePath = 17 or exePath = 18) then
			'개발섭은 웹시청 허용'
			If not(SERVER_NAME = TEST_SERVER_NAME and exePath = 5) Then
				call resultJsonSet("1","이 방송은 안드로이드앱이나 아이폰 앱을 통해서만 시청가능합니다.")
			end if
		end if
		If uBound(castAddressArr) = 2 Then
			chatAddress = castAddressArr(2)			
			if exePath = 5 or exePath = 6 then
				castAddress = replace(castAddress, "rtmp", "http")
			' pip 기능 추가건. 아이폰 App은 두개 영상 URL이 다 필요하여 추가
			ElseIf exePath = 3 or exePath = 8 Or exePath = 15 or exePath = 16 then
				castAddress = replace(castAddress, "rtmp", "http")				
			end if
			castAddress = getLIVEURLcast(castAddress, signId)

			' pip 기능 추가건. rtmp://아이피로 변경
			if exePath = 3 or exePath = 8 Or exePath = 15 or exePath = 16 then
				castAddress = replace(castAddress, "http://", "rtmp://")
			end if
		End If
		castCastType = CInt(cmdRs("castType"))
		castisAdult = cmdRs("isAdult")
		castcategory = cmdRs("category")
		isJoint = cmdRs("isJoint")
		If accountLevel < 1 then '일반 시청자 송출 제한 체크
		if cmdRs("castListTarget") = "10" then
			if partnerCode <> cast_partnerCode then
				call resultJsonSet("1","본 방송은 시청하실 수 없습니다.")
				end if
			end if
		end if
	End If
	Set cmdRs = Nothing

	'--# 휴대폰인증 여부 확인(0:미인증, 1:인증)
	'// 셀럽티비 제외
	if castisAdult = true then
		with objCmd
			Call cmdPramDel(objCmd)
			cmdRtnCode = ""
			.commandText = "[B_MEMBER].[dbo].[JBN_JSON_isPhoneCheck]"
			.commandType = &H0004
			.activeConnection = nothing
			.activeConnection = OLEDB_220
			.Parameters.Append .CreateParameter("@signID", adVarChar, adParamInput, 25)
			.Parameters.Append .CreateParameter("@partnerCode", adVarChar, adParamInput,7)
			.Parameters.Append .CreateParameter("@return", adInteger, adParamOutput, 4)
			.Parameters("@signID") = signId
			.Parameters("@partnerCode") = partnerCode
			.Parameters("@return") = 0
			.execute()
			cmdRtnCode = .parameters("@return")
		End With
		If Not cmdRtnCode = 1 Then
			'call resultJsonSet("1","회원님의 휴대폰번호는 인증되지 않았습니다. 마이페이지 내정보수정에서 휴대폰번호변경(인증) 후 이용하세요.")
			call resultJsonSet("A","휴대폰 미인증 회원입니다. 웹사이트 로그인 후 마이페이지>내정보수정 하단에서 휴대폰 인증 후 이용 가능합니다")			
		End if
	end if
	'//
	
	'# 방송타입 확인
	If Not castType = castCastType Then
		call resultJsonSet("1","방송시청을 할 수 없습니다.[CT]")
	End if
	'//

	'--# 비공개방송 비밀번호 확인
	If accountLevel < 3 then
		with objCmd
			Call cmdPramDel(objCmd)
			cmdRtnCode = ""
			.commandText = "[B_CASTDATA].[dbo].[JBN_JSON_castWatchOn_Step5_PasswordCheck]"
			.commandType = &H0004
			.activeConnection = nothing
			.activeConnection = OLEDB_CAST
			.Parameters.Append .CreateParameter("@pk_castCode", adVarChar, adParamInput, 40)
			.Parameters.Append .CreateParameter("@passwordKey", adVarChar, adParamInput,10)
			.Parameters.Append .CreateParameter("@return", adInteger, adParamOutput, 10)
			.Parameters("@pk_castCode") = castCode
			.Parameters("@passwordKey") = password
			.Parameters("@return") = 0
			.execute()
			cmdRtnCode = .parameters("@return")
		End with
		If Not cmdRtnCode = 0 Then
			call resultJsonSet("E1","비밀번호가 일치하지 않습니다.")
		End If
	End if
	'// 

	'--# 멀티방송 모바일시청 불가처리
	If castType = 3 And exePath <> 4 Then
		call resultJsonSet("1","멀티방송은 PC에서만 시청이 가능합니다.")
	End If
	'//

	'--# 시청자 팬등급 설정 (0:최상위, 1:상위, 2:하위, 3:최하위, 4:없음)
	with objCmd
		Call cmdPramDel(objCmd)
		cmdRtnCode = ""
		.commandText = "[B_MEMBER].[dbo].[SSM_fanGroup_memberSelect]"
		.commandType = &H0004
		.activeConnection = nothing
		.activeConnection = OLEDB_CAST5
		.Parameters.Append .CreateParameter("@signid", adVarChar, adParamInput, 25)
		.Parameters.Append .CreateParameter("@fan_signId", adVarChar, adParamInput, 25)
		.Parameters.Append .CreateParameter("@partnerCode", adChar, adParamInput,7)
		.Parameters.Append .CreateParameter("@fan_partnerCode", adChar, adParamInput,7)
		.Parameters("@signid") = cast_signId
		.Parameters("@fan_signId") = signId
		.Parameters("@partnerCode") = cast_PartnerCode
		.Parameters("@fan_partnerCode") = partnerCode
		Set cmdRs = .execute()
	End with
	If Not cmdRs.eof Then
		fanLevel = cmdRs("fanLevel")
	Else
		fanLevel = 4
	End If
	Set cmdRs = Nothing	
	'--# 팬설정정보 검색
	with objCmd
		Call cmdPramDel(objCmd)
		.commandText = "[B_MEMBER].[dbo].[JBN_JSON_memberFanLevelSetupSearch]"
		.commandType = &H0004
		.activeConnection = OLEDB_CAST5
		.Parameters.Append .CreateParameter("@signId", adVarChar, adParamInput, 25)
		.Parameters.Append .CreateParameter("@partnerCode", adChar, adParamInput,7)
		.Parameters("@signId") = cast_signId
		.Parameters("@partnerCode") = cast_PartnerCode
		Set cmdRs = .execute()
	End With
	If not cmdRs.eof Then
		groupLevelNm_0 = cmdRs("groupLevelNm_0")
		groupLevelNm_1 = cmdRs("groupLevelNm_1")
		groupLevelNm_2 = cmdRs("groupLevelNm_2")
		groupLevelNm_3 = cmdRs("groupLevelNm_3")		
	End If
	Select Case fanLevel
	Case 0
		fanLevelName = groupLevelNm_0
	Case 1
		fanLevelName = groupLevelNm_1
	Case 2
		fanLevelName = groupLevelNm_2
	Case 3
		fanLevelName = groupLevelNm_3
	Case else
		fanLevelName = "등급없음"
	End select
	Set cmdRs = nothing
	'//
	
	'--# 소유코인 확인
	with objCmd
		Call cmdPramDel(objCmd)
		cmdRtnCode = ""
		.commandText = "[B_COIN].[dbo].[JBN_WEB_MyPage_coinMemberData]"
		.commandType = &H0004
		.activeConnection = nothing
		.activeConnection = OLEDB_CTICAST5
		.Parameters.Append .CreateParameter("@signId", adVarChar, adParamInput, 25)
		.Parameters.Append .CreateParameter("@partnerCode", adVarChar, adParamInput, 7)
		.Parameters.Append .CreateParameter("@return", adInteger, adParamOutput, 4)
		.Parameters("@signId") = signId
		.Parameters("@partnerCode") = partnerCode
		.Parameters("@return") = 0
		Set cmdRs = .execute()
	End With
	If Not cmdRs.eof Then
		coin = cmdRs("accountCoinValue")
	End If
	Set cmdRs = nothing 
	'//

	'--# 일반 시청자 처리
	If accountLevel < 1 Then
		'--# 방송시청 차단확인
		call blockCheck()
		'//
		
		'--# 팬방송 확인
		If castType = 5 Then
			'# 팬방송 등급정보
			with objCmd
				Call cmdPramDel(objCmd)
				cmdRtnCode = ""
				.commandText = "[B_CASTDATA].[dbo].[JBN_JSON_fanLevel]"
				.commandType = &H0004
				.activeConnection = nothing
				.activeConnection = OLEDB_CAST
				.Parameters.Append .CreateParameter("@signId", adVarChar, adParamInput, 25)
				.Parameters.Append .CreateParameter("@partnerCode", adChar, adParamInput,7)
				.Parameters.Append .CreateParameter("@return", adInteger, adParamOutput, 4)
				.Parameters("@signId") = cast_signId
				.Parameters("@partnerCode") = cast_partnerCode
				.Parameters("@return") = 0
				.execute()
				castFanLevel = .parameters("@return")
			End with
			'# 팬방송 시청가능 확인
			with objCmd
				Call cmdPramDel(objCmd)
				cmdRtnCode = ""
				.commandText = "[B_CASTDATA].[dbo].[JBN_JSON_castWatchOn_Step4_GroupCheck]"
				.commandType = &H0004
				.activeConnection = nothing
				.activeConnection = OLEDB_CAST5
				.Parameters.Append .CreateParameter("@cast_signId", adVarChar, adParamInput, 25)
				.Parameters.Append .CreateParameter("@watch_signId", adVarChar, adParamInput, 25)
				.Parameters.Append .CreateParameter("@cast_PartnerCode", adVarChar, adParamInput, 7)
				.Parameters.Append .CreateParameter("@watch_PartnerCode", adVarChar, adParamInput, 7)
				.Parameters.Append .CreateParameter("@fanLevel", adSmallInt, adParamInput, 2)
				.Parameters.Append .CreateParameter("@return", adInteger, adParamOutput, 10)
				.Parameters("@cast_signId") = cast_signId
				.Parameters("@watch_signId") = signId
				.Parameters("@cast_PartnerCode") = cast_PartnerCode
				.Parameters("@watch_PartnerCode") = PartnerCode
				.Parameters("@fanLevel") = castFanLevel
				.Parameters("@return") = 0
				.execute()
				'# cmdRtnCode (0:시청가능, 1:시청 불가능)
				cmdRtnCode = .parameters("@return")
			End With
			'# 팬방송 시청불가시
			If cmdRtnCode = 1 Then
				'--# 방송자 팬설정정보
				Select Case castFanLevel
				Case 0
					groupLevelNm = groupLevelNm_0
				Case 1
					groupLevelNm = groupLevelNm_1
				Case 2
					groupLevelNm = groupLevelNm_2
				Case 3
					groupLevelNm = groupLevelNm_3
				End Select
				'//
				'--# 팬방송 필요입장코인 처리
				with objCmd
					Call cmdPramDel(objCmd)
					cmdRtnCode = ""
					.commandText = "[B_CASTDATA].[dbo].[JBN_JSON_fanCastCoin]"
					.commandType = &H0004
					.activeConnection = nothing
					.activeConnection = OLEDB_CAST5
					.Parameters.Append .CreateParameter("@signId", adVarChar, adParamInput, 25)
					.Parameters.Append .CreateParameter("@partnerCode", adVarChar, adParamInput, 7)
					.Parameters.Append .CreateParameter("@watch_signId", adVarChar, adParamInput, 25)
					.Parameters.Append .CreateParameter("@watch_partnerCode", adVarChar, adParamInput, 7)
					.Parameters.Append .CreateParameter("@cast_fanLevel", adSmallInt, adParamInput, 2)
					.Parameters.Append .CreateParameter("@giftCoin", adInteger, adParamOutput, 4)
					.Parameters("@signId") = cast_signId
					.Parameters("@partnerCode") = cast_PartnerCode
					.Parameters("@watch_signId") = signId
					.Parameters("@watch_partnerCode") = PartnerCode
					.Parameters("@cast_fanLevel") = castFanLevel
					.Parameters("@giftCoin") = 0
					.execute()
					fanLevelGiftCoin = .parameters("@giftCoin")
				End With
				'//
				'--# 그룹방송 시청불가 결과처리
				If fanLevelGiftCoin <= 0 Then
					call resultJsonSet("E7","회원님의 팬등급이 방송자에 의해 하향 조정되어 시청이 불가능 합니다.")
				Else
					needCoin = fanLevelGiftCoin
						call resultJsonSet("A1","본 방송은 [" & groupLevelNm & "]팬클럽 방송이며 해당 팬클럽에 가입하려면 " & SERVICE_COIN_NAME & " [" & fanLevelGiftCoin & "]개가 필요합니다. 가입 후 시청하시겠습니까?")
				End If
				'//
			End If
		End If
		'// 팬방송 확인

		'--# 유료방송 확인
		If castType = 7 Then
			'--# 시청 코인지불 내역확인
			with objCmd
				Call cmdPramDel(objCmd)
				cmdRtnCode = ""
				.commandText = "[B_COIN].[dbo].[JBN_JSON_ticketCoinUseCheck]"
				.commandType = &H0004
				.activeConnection = nothing
				.activeConnection = OLEDB_CTICAST5
				.Parameters.Append .CreateParameter("@watch_signId", adVarChar, adParamInput, 25)
				.Parameters.Append .CreateParameter("@cast_signId", adVarChar, adParamInput, 25)
				.Parameters.Append .CreateParameter("@watch_PartnerCode", adVarChar, adParamInput,7)
				.Parameters.Append .CreateParameter("@cast_PartnerCode", adVarChar, adParamInput,7)
				.Parameters.Append .CreateParameter("@return", adInteger, adParamOutput)
				.Parameters("@watch_signId") = signId
				.Parameters("@cast_signId") = cast_signId
				.Parameters("@watch_PartnerCode") = partnerCode
				.Parameters("@cast_PartnerCode") = cast_partnerCode
				.Parameters("@return") = 0
				.execute()
				'# @return (0:내역존재, 1:내역없음)
				cmdRtnCode = .parameters("@return")
			End with
			'//

			'--# 시청 코인지불 내역없음
			If Not cmdRtnCode = 0 Then	
				'# 시청 코인금액 확인
				with objCmd
					Call cmdPramDel(objCmd)
					.commandText = "[B_CASTDATA].[dbo].[JBN_JSON_castMemberSearch_DDD]"
					.commandType = &H0004
					.activeConnection = nothing
					.activeConnection = OLEDB_CAST
					.Parameters.Append .CreateParameter("@signId", adVarChar, adParamInput, 25)
					.Parameters.Append .CreateParameter("@partnerCode", adVarChar, adParamInput, 7)
					.Parameters("@signId") = cast_signId
					.Parameters("@partnerCode") = cast_partnerCode
					Set cmdRs = .execute()
				End With
				If Not cmdRs.eof then
					needCoin = cmdRs("tiketCoin")
				Else
					call resultJsonSet("1","JJCMS")
				End If
				Set cmdRs = nothing
				'# 시청 코인금액 정보
				call resultJsonSet("A3","본 방송은 유료방송이며, 입장료 " & SERVICE_COIN_NAME & " " & needCoin & "개가 소진됩니다. 시청하시겠습니까?")
			End If
			'// 
		End if
		'//

		'--# 시청인원제한 확인
		If accountLevel < 1 Then
			with objCmd
				Call cmdPramDel(objCmd)
				cmdRtnCode = "0"
				.commandText = "[B_CASTDATA].[dbo].[JBN_JSON_castWatchOn_Step3_MaxInCheck_DDD]"
				.commandType = &H0004
				.activeConnection = nothing
				.activeConnection = OLEDB_CAST
				.Parameters.Append .CreateParameter("@pk_castCode", adVarChar, adParamInput, 40)
				.Parameters.Append .CreateParameter("@cast_signId", adVarChar, adParamInput, 25)
				.Parameters.Append .CreateParameter("@watch_signId", adVarChar, adParamInput, 25)
				.Parameters.Append .CreateParameter("@cast_partnerCode", adVarChar, adParamInput,7)
				.Parameters.Append .CreateParameter("@watch_partnerCode", adVarChar, adParamInput,7)
				.Parameters.Append .CreateParameter("@return", adInteger, adParamOutput, 10)
				.Parameters("@pk_castCode") = castCode
				.Parameters("@cast_signId") = cast_signId
				.Parameters("@watch_signId") = signId
				.Parameters("@cast_partnerCode") = cast_partnerCode
				.Parameters("@watch_partnerCode") = partnerCode
				.Parameters("@return") = 0
				.execute()
				cmdRtnCode = .parameters("@return")
			End With
			'# @return (0:시청인원 가능, 1:시청인원 불가능)
			If cmdRtnCode = 1 Then
				if exePath = 8 Or exePath = 16 then
					call resultJsonSet("A2","시청인원이 초과되어 시청이 불가능합니다. 아이템이 필요합니다.")
				else
					call resultJsonSet("A2","시청인원이 초과되어 시청이 불가능합니다. 풀방 입장 아이템을 구매하시겠습니까?")
				end if
			End If
		End If
		'// 

	End if
	'// 일반시청자 처리

	'--# 매니저 시청자 처리
	If accountLevel = 2 Then
		'--# 방송시청 차단확인
		call blockCheck()
	End if
	'//
	'AOS player 체크'
	playerType = getplayerType(exePath, androidStore)
End if
'// 시청신호처리
'--# 방송시청 시작/종료 로그
'with objCmd
'	Call cmdPramDel(objCmd)
'	cmdRtnCode = ""
'	.commandText = "B_CASTDATA.JBN_JSON_castWatchLog_Insert2"
'	.commandType = &H0004
'	.activeConnection = nothing
'	.activeConnection = OLEDB_171
'	.Parameters.Append .CreateParameter("@castCode", adVarChar, adParamInput, 40)
'	.Parameters.Append .CreateParameter("@cast_signId", adVarChar, adParamInput, 25)
'	.Parameters.Append .CreateParameter("@watch_signId", adVarChar, adParamInput,25)
'	.Parameters.Append .CreateParameter("@logDateCode", adVarChar, adParamInput,14)
'	.Parameters.Append .CreateParameter("@watchType", adSmallInt, adParamInput, 2)
'	.Parameters.Append .CreateParameter("@watchPath", adSmallInt, adParamInput, 2)
'	.Parameters.Append .CreateParameter("@cast_partnerCode", adVarChar, adParamInput,7)
'	.Parameters.Append .CreateParameter("@watch_partnerCode", adVarChar, adParamInput,7)
'	.Parameters.Append .CreateParameter("@logType", adSmallInt, adParamInput, 2)
'	.Parameters.Append .CreateParameter("@V_IP", adVarChar, adParamInput, 25)
'	.Parameters("@castCode") = castCode
'	.Parameters("@cast_signId") = cast_signId
'	.Parameters("@watch_signId") = signId
'	.Parameters("@logDateCode") = getDateTimeCode()
'	.Parameters("@watchType") = castType
'	.Parameters("@watchPath") = exePath
'	.Parameters("@cast_partnerCode") = cast_partnerCode
'	.Parameters("@watch_partnerCode") = partnerCode
'	.Parameters("@logType") = commandType
'	.Parameters("@V_IP") = REMOTE_ADDR
'	.execute()
'End with	
'//

'--# NODE 채팅서버 Request
'# commandType (0:방송시청, 1:방송시청종료)
'# chatServerType (A:wowza, B:node)
If commandType = 0 And chatServerType = "B" Then
	'--# 회원정보
	With objCmd
		Call cmdPramDel(objCmd)
		cmdRtnCode = 0
		.commandText = "[B_MEMBER].[dbo].[JBN_WEB_memberPublicSearch]"
		.commandType = &H0004
		.activeConnection = nothing
		.activeConnection = OLEDB_CAST
		.Parameters.Append .CreateParameter("@signId", adVarChar, adParamInput, 25)
		.Parameters.Append .CreateParameter("@partnerCode", adVarChar, adParamInput, 7)
		.Parameters.Append .CreateParameter("@return", adInteger, adParamOutput)	
		.Parameters("@signId") = signId
		.Parameters("@partnerCode") = partnerCode
		.Parameters("@return") = 0
		Set cmdRs = .execute()
	End With
	If cmdRs.eof Then
		call resultJsonSet("E8","회원정보를 확인할 수 없어 방송을 시청할 수 없습니다.")
	Else
		memberSex = cmdRs("memberSex")
		nickName = cmdRs("nickName")
		isAdultCheck = cmdRs("isAdultCheck")
		If memberSex Then
			memberSex = "1"
		else
			memberSex = "0"
		End If
		If nickName = "" Or isNull(nickName) Then
			nickName = Left(signId,8)
		End if				
		if castisAdult or cstr(castcategory) = "20" then
			if not isAdultCheck then
				call resultJsonSet("E9","19세 미만은 시청이 불가능합니다.")
			end if
		end if
	End If
	Set cmdRs = Nothing

	dim vhImagFlnm, vhImagFlnmGIF
	'--# 입장효과 설정 조회
	With objCmd
		Call cmdPramDel(objCmd)
		cmdRtnCode = 0
		.commandText = "[B_ITEM].[dbo].[USP_Get_AQItemUsgstsChck_002]"
		.commandType = &H0004
		.activeConnection = nothing
		.activeConnection = OLEDB_CTICAST5
		.Parameters.Append .CreateParameter("@signId", adVarChar, adParamInput, 25)
		.Parameters.Append .CreateParameter("@partnerCode", adVarChar, adParamInput, 7)
		.Parameters.Append .CreateParameter("@effectType", adInteger, adParamOutput)	
		.Parameters.Append .CreateParameter("@vhImagFlnm", adVarChar, adParamOutput, 255)
		.Parameters("@signId") = signId
		.Parameters("@partnerCode") = partnerCode
		.Parameters("@effectType") = 0
		.execute()
		'# @return (0:없음 , 1~:입장효과 코드)
		cmdRtnCode = .parameters("@effectType")
	End With
	If cmdRtnCode <> 0 Then
		if cmdRtnCode = 5 Then	'아바타 일경우			
			vhImagFlnm = objCmd.parameters("@vhImagFlnm")
			if vhImagFlnm <> "" then
				vhImagFlnmGIF = split(vhImagFlnm, ".")(0)+".gif"
				vhImagFlnm = "https://"& IMAGE_SERVER_URL & "/profile_thumb/"& partnerCode & "/" & Left(signId,1) & "/" & Left(signId,2) &"/"&vhImagFlnm
				vhImagFlnmGIF = "https://"& IMAGE_SERVER_URL & "/profile_thumb/"& partnerCode & "/" & Left(signId,1) & "/" & Left(signId,2) &"/"&vhImagFlnmGIF
			end if
			itemlist = ", ""items"":[{""item"":""enterevt"", ""value"":"""& cmdRtnCode &""", ""avatarURL"":"""& vhImagFlnm &""", ""avatarGIFURL"":"""& vhImagFlnmGIF &""", ""to"":""room""}]"		
		else
			itemlist = ", ""items"":[{""item"":""enterevt"", ""value"":"""& cmdRtnCode &""", ""to"":""room""}]"		
		end if
	End If
	vhImagFlnm = ""
	vhImagFlnmGIF = ""
	'--# 활성 아바타 조회
	With objCmd
		Call cmdPramDel(objCmd)
		cmdRtnCode = 0
		.commandText = "[B_BOARD].[dbo].[USP_Get_AvtrPrflImag_001]"
		.commandType = &H0004
		.activeConnection = nothing
		.activeConnection = OLEDB_CAST4
		.Parameters.Append .CreateParameter("@vchMmbri", adVarChar, adParamInput, 25, signId)
		.Parameters.Append .CreateParameter("@chrPrtsCd", adVarChar, adParamInput, 7, partnerCode)			
		Set cmdRs = .execute()
	End With
	If not cmdRs.eof Then
		vhImagFlnm = cmdRs("attachFileName")
		if vhImagFlnm <> "" then
			vhImagFlnmGIF = split(vhImagFlnm, ".")(0)+".gif"
			vhImagFlnm = "https://"& IMAGE_SERVER_URL & "/profile_thumb/"& partnerCode & "/" & Left(signId,1) & "/" & Left(signId,2) &"/"&vhImagFlnm
			vhImagFlnmGIF = "https://"& IMAGE_SERVER_URL & "/profile_thumb/"& partnerCode & "/" & Left(signId,1) & "/" & Left(signId,2) &"/"&vhImagFlnmGIF
		end if
	end if
	'--# 코인지불 내역확인
	with objCmd
		Call cmdPramDel(objCmd)
		cmdRtnCode = ""
		.commandText = "[B_COIN].[dbo].[LHY_JSON_coinUseCheck]"
		.commandType = &H0004
		.activeConnection = nothing
		.activeConnection = OLEDB_CTICAST5
		.Parameters.Append .CreateParameter("@watch_signId", adVarChar, adParamInput, 25)
		.Parameters.Append .CreateParameter("@cast_signId", adVarChar, adParamInput, 25)
		.Parameters.Append .CreateParameter("@watch_PartnerCode", adVarChar, adParamInput,7)
		.Parameters.Append .CreateParameter("@cast_PartnerCode", adVarChar, adParamInput,7)
		.Parameters.Append .CreateParameter("@return", adInteger, adParamOutput)
		.Parameters("@watch_signId") = signId
		.Parameters("@cast_signId") = cast_signId
		.Parameters("@watch_PartnerCode") = partnerCode
		.Parameters("@cast_PartnerCode") = cast_partnerCode
		.Parameters("@return") = 0
		.execute()
		'# @return (0:내역없음, 1:내역존재)
		isGifter = .parameters("@return")
	End with
	'//	
	
	'# NODE request
	If Not chatAddress = "" Then
		Dim sSvcLevel : sSvcLevel = 1
		dim SvcLevelViewYn : SvcLevelViewYn = "N"
		dim chatBubbleCd
		with objCmd
			Call cmdPramDel(objCmd)
			.commandText = "[B_MEMBER].[dbo].[USP_Get_BrdcrSvcLvlExp_002]"
			.commandType = &H0004
			.activeConnection = OLEDB_CAST
			.Parameters.Append .CreateParameter("@signId", adVarChar, adParamInput, 25, signId)
			.Parameters.Append .CreateParameter("@partnerCode", adVarChar, adParamInput, 7, partnerCode)
			.Parameters.Append .CreateParameter("@intLvlSeCd", adInteger, adParamInput, , 10002) '서비스 레벨
			Set cmdRs = .execute()
		End With
		If Not cmdRs.eof Then
			sSvcLevel = cmdRs("Lvl")
			SvcLevelViewYn = cmdRs("SvcLvlExpsrYn")
		End If
		Set cmdRs = nothing
		Dim sfanLevel : sfanLevel = 1
		with objCmd
			Call cmdPramDel(objCmd)
			.commandText = "[B_MEMBER].[dbo].[USP_GetList_FanLvlExp]"
			.commandType = &H0004
			.activeConnection = OLEDB_CAST
			.Parameters.Append .CreateParameter("@signId", adVarChar, adParamInput, 25, signId)
			.Parameters.Append .CreateParameter("@partnerCode", adVarChar, adParamInput, 7, partnerCode)
			.Parameters.Append .CreateParameter("@vchBrdcrMmbri", adVarChar, adParamInput, 25, cast_signId)
			.Parameters.Append .CreateParameter("@chrBrdcrPrtsCd", adVarChar, adParamInput, 7, cast_partnerCode)
			Set cmdRs = .execute()
		End With
		If Not cmdRs.eof Then
			sfanLevel = cmdRs("Lvl")
		End If
		Set cmdRs = nothing

		with objCmd
			Call cmdPramDel(objCmd)
			.commandText = "[B_ITEM].[dbo].[USP_Get_ASItemUsgstsChck_002]"
			.commandType = &H0004
			.activeConnection = OLEDB_CTICAST5
			.Parameters.Append .CreateParameter("@signId", adVarChar, adParamInput, 25, signId)
			.Parameters.Append .CreateParameter("@partnerCode", adVarChar, adParamInput, 7, partnerCode)
			Set cmdRs = .execute()
		End With
		If Not cmdRs.eof Then
			chatBubbleCd = cmdRs("ItemCd")
			if len(chatBubbleCd) > 4 then
				chatBubbleCd = right(chatBubbleCd, 4)
				if isnumeric(chatBubbleCd) then
					chatBubbleCd = cint(chatBubbleCd)
				end if
			end if
		End If
		Set cmdRs = nothing	

		dim oChatUtil
		set oChatUtil = new chatUtil
		oChatUtil.init()
		call oChatUtil.castWatchOnOff(chatAddress, castCode, signId, nickName, memberSex, exePath, partnerCode, accountLevel, fanLevel, itemlist, isGifter, sSvcLevel, sfanLevel, SvcLevelViewYn, chatBubbleCd, isSecret, vhImagFlnm, vhImagFlnmGIF)
		oChatUtil.destroy()
		if oChatUtil.status <> "0" then
			call resultJsonSet("1", oChatUtil.statusMsg)
		end if
	End if
End if
'//

'--# ADO close
Set objCmd = nothing
'//

'--# Success
call resultJsonSet("0","SUCEESS")
'//

'--# [FUNCTION]
Sub resultJsonSet(rstCode, rstMsg)
	response.clear()
	If Not rstCode = "0" Then
		castAddress = ""
	End if
	dim errorCode
	errorCode = ""
	if len(rstCode) > 1 and left(rstCode, 1) = "E" then
		errorCode = rstCode
		rstCode = "1"
	end if
	dim strRst 
	strRST = "{" & _
		"""rst"":{""rstCode"" : """ & rstCode & """,""error"" : """ & errorCode & """,""rstMsg"" : """ & jsEncode(rstMsg) & """}," & _
		"""castWatch"":{""accountLevel"":""" & accountLevel & """, ""fanLevel"":""" & fanLevel & """, ""fanLevelName"":""" & jsEncode(fanLevelName) & """, ""needCoin"":""" & needCoin & """, ""coin"":""" & coin & """, ""castAddress"":""" & jsEncode(castAddress) & """, ""isUpdate"":""" & isUpdate & """, ""vTK"":""" & vTK & """, ""isJoint"":""" & isJoint & """,""playerType"":""" & playerType & """,""category"":""" & castcategory & """}" & _
	"}"

	Response.Write(aesresult(strRST, aesver))
	response.End()
End Sub

function blockCheck()
	'--# 방송시청 차단확인
		with objCmd
			Call cmdPramDel(objCmd)
			cmdRtnCode = ""
			.commandText = "[B_CASTDATA].[dbo].[JBN_JSON_castWatchOn_Step2_BlockCheck]"
			.commandType = &H0004
			.activeConnection = nothing
			.activeConnection = OLEDB_13
			.Parameters.Append .CreateParameter("@cast_signId", adVarChar, adParamInput, 25)
			.Parameters.Append .CreateParameter("@watch_signId", adVarChar, adParamInput, 25)
			.Parameters.Append .CreateParameter("@cast_partnerCode", adVarChar, adParamInput,7)
			.Parameters.Append .CreateParameter("@watch_partnerCode", adVarChar, adParamInput,7)
			.Parameters.Append .CreateParameter("@return", adInteger, adParamOutput, 10)
			.Parameters("@cast_signId") = cast_signId
			.Parameters("@watch_signId") = signId
			.Parameters("@cast_partnerCode") = cast_partnerCode
			.Parameters("@watch_partnerCode") = partnerCode
			.Parameters("@return") = 0
			.execute()
			'# @return (0:차단없음, 1:시청차단, 2:서비스차단, 3:방송자 차단)
			cmdRtnCode = .parameters("@return")
		End With
		If Not cmdRtnCode = 0 then
			Select Case cmdRtnCode
			Case 1
				call resultJsonSet("E6","해당 아이디는 방송시청 서비스가 정지되어 시청이 불가능 합니다.")
			Case 2
				call resultJsonSet("E6","해당 아이디는 서비스가 정지되어 시청이 불가능 합니다.")
			Case 3
				call resultJsonSet("E6","해당 아이디는 방송자에 의해 차단되어 시청이 불가능 합니다.")
			Case Else
				call resultJsonSet("E6","해당 아이디는 방송시청이 불가능 합니다.")
			End Select
		End If
end function		
'// [FUNCTION]
%>




https://devsys.popkontv.kr:9002/AS/member/registNickCheck.asp
 {"SC_NK":"프리미엄닉넴넴"}
 NicknameValidationResModel(rst=ResultModel(rstCode=0, rstMsg=사용 가능한 닉네임 입니다., pageNum=0, totalPageNum=0, totalListNum=0))





https://down.popcast.co.kr/beta/popkonTV_2.0_plus_v9.31.001.apk
https://down.popcast.co.kr/beta/popkonTV_2.0_plus.apk
https://down.popcast.co.kr/beta/rink.apk

Cert Test CertSignUpFragment CertifyComplete gender male, socialno 19840131, pnum : 01045119328, di : MC0GCCqGSIb3DQIJAyEApCmBKiv5Hauu3GUqO22EFN4kt+Zw9gBWf+F6LJbXTlY=, ci : awLIPFk8ac9GcErBmtur1c7L278WJSjG9McxmdraXoaOtz6XYwtd9kU34I4A7xoGY+jt/2In/INClH2JukUFlw==, name 오지훈
 

https://devsys.popkontv.kr:9002/AS/member/findidpwd.asp
{"SC_DI":"MC0GCCqGSIb3DQIJAyEApCmBKiv5Hauu3GUqO22EFN4kt+Zw9gBWf+F6LJbXTlY=","SC_ID":"19840131","SC_MN":"오지훈","SC_PC":"P-00001","SC_RC":"id","SC_SE":1}
FindIdPwResModel(rst=ResultModel(rstCode=0, rstMsg=조회가 완료 되었습니다., signId=, snscode=0, snsname=))

https://devsys.popkontv.kr:9002/AS/member/registMember.asp
{"SC_AEM":"","SC_AID":"189993731","SC_ANK":"","SC_EM":"","SC_EP":7,"SC_ISA":1,"SC_NK":"popaos99","SC_PC":"P-00001","SC_PID":"utm_source=google-play&utm_medium=organic","SC_PN":"01045119328","SC_SCD":3,"SC_SI":"","SC_SP":""}
SignUpResModel(rst=ResultModel(rstCode=0, rstMsg=회원가입이 정상적으로 처리되었습니다., signId=n2270094829703240226, signPwd=0x448AB02B742F1751AF57ED2541A6683D76510519387658921FB511305EAB5C03))

https://devsys.popkontv.kr:9002/AS/member/nameCertChk.asp
{"SC_CI":"awLIPFk8ac9GcErBmtur1c7L278WJSjG9McxmdraXoaOtz6XYwtd9kU34I4A7xoGY+jt/2In/INClH2JukUFlw==","SC_DI":"MC0GCCqGSIb3DQIJAyEApCmBKiv5Hauu3GUqO22EFN4kt+Zw9gBWf+F6LJbXTlY=","SC_ID":"19840131","SC_MN":"오지훈","SC_PC":"P-00001","SC_PN":"01045119328","SC_SE":1,"SC_SI":""}
CertResModel(rst=ResultModel(rstCode=0, rstMsg=회원가입이 정상적으로 처리되었습니다., bonusCoinCount=0))

--------------------------------------------------------------------------

https://devsys.popkontv.kr:9002/AS/member/findidpwd.asp

{"SC_DI":"MC0GCCqGSIb3DQIJAyEApCmBKiv5Hauu3GUqO22EFN4kt+Zw9gBWf+F6LJbXTlY=","SC_ID":"19840131","SC_MN":"오지훈","SC_PC":"P-00001","SC_RC":"id","SC_SE":1}
FindIdPwResModel(rst=ResultModel(rstCode=0, rstMsg=조회가 완료 되었습니다., signId=, snscode=0, snsname=))


https://devsys.popkontv.kr:9002/AS/member/findidpwd.asp

{"SC_DI":"MC0GCCqGSIb3DQIJAyEApCmBKiv5Hauu3GUqO22EFN4kt+Zw9gBWf+F6LJbXTlY=","SC_ID":"19840131","SC_MN":"오지훈","SC_PC":"P-00001","SC_RC":"id","SC_SE":1}
FindIdPwResModel(rst=ResultModel(rstCode=0, rstMsg=조회가 완료 되었습니다., signId=, snscode=0, snsname=))


https://devsys.popkontv.kr:9002/AS/member/findidpwd.asp
{"SC_DI":"MC0GCCqGSIb3DQIJAyEApCmBKiv5Hauu3GUqO22EFN4kt+Zw9gBWf+F6LJbXTlY=","SC_ID":"19840131","SC_MN":"오지훈","SC_PC":"P-00001","SC_RC":0,"SC_SE":1}

개체 'syssessions', 데이터베이스 'msdb', 스키마 'dbo'에 대한 SELECT 권한이 거부되었습니다.

192.168.1.28
[B_CASTDATA].[dbo].[USP_Mod_BrdcOnOff_004]

https://devsys.popkontv.kr:9002/AS/castData/castOnData.asp
{
  "SC_PCC": "librestilo-20240222145943",
  "SC_SI": "librestilo",
  "SC_PC": "P-00001",
  "SC_CST": "2",
  "SC_CET": "2",
  "SC_SP": "0xBAB302587F78ABC13D93B96AF9E93695A81D0145BA9E377319856D708FBCC4F0",
  "SC_CLN": "1",
  "SC_CSQ": "",
  "SC_WTM": "0",
  "SC_CR": "w1280h720e1",
  "SC_EB": "PCP32bit"
}



192.168.1.28

https://devsys.popkontv.kr:9002/AS/castData/castMemberData.asp

{"SC_ADT":0,"SC_CAPT":7,"SC_CAT":"","SC_CLT":10,"SC_COS":"android","SC_CT":0,"SC_CTE":0,"SC_CTYP":0,"SC_FLV":0,"SC_ICS":"","SC_IPVT":0,"SC_LMN":0,"SC_PC":"P-00001","SC_PK":"","SC_SI":"popaos7","SC_SP":"0x9144AF24F1ADD5E63AB8CB02F2175A13F5B5D00A9E4F800DCE6C054129691D0D","SC_TKC":0}



변경전
{
"rst":{
"rstCode":"0",
"error":"",
"rstMsg":"SUCEESS"
},
"castWatch":{
"accountLevel":"0",
"fanLevel":"4",
"fanLevelName":"등급없음",
"needCoin":"",
"coin":"0",
"castAddress":"http://101.202.25.58/pop_cast20?%24PD4%2FOjw4OjoLICQc8enn6evn6ejt6Ojp7urtCRglHhzx6OfnBPEEB%2FEL6ukct0k%3D%24|bluewar131_P-00001_20240216111629|https://dev.popkontv.kr:1920",
"isUpdate":"0",
"vTK":"",
"isJoint":"False",
"playerType":"1",
"category":"10"
}
}


변경 후
{
"rst":{
"rstCode":"0",
"error":"",
"rstMsg":"SUCEESS"
},
"castWatch":{
"accountLevel":"0",
"fanLevel":"4",
"fanLevelName":"등급없음",
"needCoin":"",
"coin":"0",
"castAddress":"http://27.102.104.66/pop_cast20?%24OIugpJxxaWdpa2dpaG1oaGlvbG6JmKWenHFoZ2eEcYSHcZl8fX43Qg%3D%3D%24|bluewar131_P-00001_20240216111629|https://dev.popkontv.kr:1920",
"isUpdate":"0",
"vTK":"",
"isJoint":"False",
"playerType":"1",
"category":"10",
"castAddressApp":"rtmp://live-popkontv.hscdn.com/pop_cast20?%24OIugpJxxaWdpa2dpaG1oaGlvbG6JmKWenHFoZ2eEcYSHcX2upo03Qg%3D%3D%24|bluewar131_P-00001_20240216111629|https://dev.popkontv.kr:1920"
}
}


https://devsys.popkontv.kr:9002/AS/castData/castMemberData.asp

{
  "SC_CT": "1",
  "SC_SI": "librestilo",
  "SC_PC": "P-00001",
  "SC_SP": "0xBAB302587F78ABC13D93B96AF9E93695A81D0145BA9E377319856D708FBCC4F0",
  "SC_CAT": "aabb24",
  "SC_ADT": "1",
  "SC_IPVT": "1",
  "SC_PK": "1123",
  "SC_LMN": "410",
  "SC_CTE": "20",
  "SC_CAPT": "9",
  "SC_CTYP": "0",
  "SC_TKC": "0",
  "SC_COS": "window",
  "SC_CLT": "0",
  "SC_IJ": "0",
  "SC_ICS": "N"
}







Mobile
ENC=S&
VOD=rtmp%3A%2F%2Flive%2Dpopkontv%2Ehscdn%2Ecom%2Fpop%5Fcast20%2Fbluewar131%5FP%2D00001%5F20240215144102&
SITE=popcontv&
ID=01024297580&
IP=%3A%3A1&
NIC=&
WMSPUBPOINT=&
PLAYER=ZWOWZA

PC
ENC=S&
VOD=rtmp%3A%2F%2Flive%2Dpopkontv%2Ehscdn%2Ecom%2Fpop%5Fcast20%2Fbluewar131%5FP%2D00001%5F20240215144102&
SITE=popcontv&
ID=01024297580&
IP=%3A%3A1&
NIC=&
WMSPUBPOINT=&
PLAYER=ZWOWZA







http://theenm-guard.hscdn.com/ZWMS/ZWMSTicketPublisher/ZWMSTicketPublisherServer2.asp?ENC=S&VOD=rtmp%3A%2F%2Flive%2Dpopkontv%2Ehscdn%2Ecom%2Fpop%5Fcast20%2Fbluewar131%5FP%2D00001%5F20240

http://theenm-guard.hscdn.com/ZWMS/ZWMSTicketPublisher/ZWMSTicketPublisherServer2.asp


{"rst":{"rstCode" : "0","error" : "","rstMsg" : "SUCEESS"},"castWatch":{"accountLevel":"0", "fanLevel":"0", "fanLevelName":"VIP", "needCoin":"", "coin":"841769", "castAddress":"http:\/\/180.182.63.30\/pop_cast20?%24NYidoZluZmRmaGRmZWhlamltZmaGlaKbmW5lZGSBboGEbnWBnpU0Qg%3D%3D%24|popaos7_P-00001_20240214161424|https:\/\/dev.popkontv.kr:1920", "isUpdate":"0", "vTK":"", "isJoint":"False","playerType":"1","category":"12", "castAddressApp":"http:\/\/180.182.63.30\/pop_cast20?%24NYidoZluZmRmaGRmZWhlamltZmaGlaKbmW5lZGSBboGEbnqHaKs0Qg%3D%3D%24|popaos7_P-00001_20240214161424|https:\/\/dev.popkontv.kr:1920"}}


 PARAMS:["SC_PCC": "dlsp0415-20240214132229", "SC_CTYP": "0", "SC_VER": "7.0.001", "SC_SP": "0xD42840C99AB97D86DFCB48332A48C48B6D6826D2DA1BB9D2A660C6709477BFD2", "SC_SK": "8FC47B0D-FA2F-44A4-882F-9F3287D4417E", "SC_CT": "0", "SC_PC": "P-00001", "SC_EP": "3", "SC_SI": "popios2", "SC_CPC": "P-00117", "SC_CSI": "dlsp0415"] 
- Result -
 {"rst":{"rstCode" : "0","error" : "","rstMsg" : "SUCEESS"},"castWatch":{"accountLevel":"0", "fanLevel":"4", "fanLevelName":"\uB4F1\uAE09\uC5C6\uC74C", "needCoin":"", "coin":"0", "castAddress":"rtmp:\/\/live.popkontv.hscdn.com\/pop_cast25?%24PTg2MSY7PzcMBAIEBgIEAwYDCAUDBgQkM0A5NwwDAgIfDB8iDDwTPifSRQ%3D%3D%24|dlsp0415_P-00117_20240214132229|https:\/\/gw.popkontv.kr:1920", "isUpdate":"0", "vTK":"", "isJoint":"False","playerType":"1","category":"10"}} 



 URL:https://sys1.popkontv.kr:9002/AS/castData/naCastWatchOnOff.asp

 PARAMS:["SC_CPC": "P-00117", "SC_SP": "0xD42840C99AB97D86DFCB48332A48C48B6D6826D2DA1BB9D2A660C6709477BFD2", "SC_SI": "popios2", "SC_PCC": "dlsp0415-20240214132229", "SC_SK": "6B56A58F-F136-4B26-90CE-9852B39D6B1C", "SC_PC": "P-00001", "SC_EP": "6", "SC_CTYP": "0", "SC_CT": "0", "SC_CSI": "dlsp0415", "SC_VER": "7.0.001"] 
- Result -
 {"rst":{"rstCode" : "0","error" : "","rstMsg" : "SUCEESS"},"castWatch":{"accountLevel":"0", "fanLevel":"4", "fanLevelName":"\uB4F1\uAE09\uC5C6\uC74C", "needCoin":"", "coin":"0", "castAddress":"http:\/\/27.102.104.66\/pop_cast25?%24PT44Ojs0m7C0rIF5d3l7d3l4e3h9en15eZmota6sgXh3d5SBlJeBvLmvjEdH%24|dlsp0415_P-00117_20240214132229|https:\/\/gw.popkontv.kr:1920", "isUpdate":"0", "vTK":"", "isJoint":"False","playerType":"1","category":"10"}}




--------------------------------------------------


["SC_SI":"k6085092010880240214","SC_SC":"2","SC_SK":"1356426907"
](https://stagesys.popkontv.com:9002/AS/webPage/callWeb.asp?data=0FLtJZ23U2bD1eCkGPSPJeQInHBktV6x2njW4vhpeYeMCwpaF8GR2oK5%2BIEfoQni6R4%2BqL2/3oGCGe9RfBCY1jV22qhvTUoo2SDyAvP9r%2BpFfCpAbLrHQbtH5wAFD3NYcN2uzmwcPDWpXQAy8DzXlt5b7ETVDTEVAFsm4ayKPWaYfulTeEATBXlzuLGh%2BV46&key=498&v=2)

k6085092010880240214

JBN_memberSignLog_Insert

JBN_memberSignLog_Insert 

B_LOG.dbo.JBN_memberSignLog_Insert
/AS/member/naSignOn.asp    회원 로그인
/AS/member/naSignOnCast.asp   회원 로그인(방송용)
/AS/member/signOnSNS.asp    회원 로그인(SNS)
/AS/member/signOnWeb.asp   웹에서의 응용프로그램 실행시 로그인 (자동 로그인) (플렉스)



https://sys1.popkontv.kr:9002/AS/castData/castOnData.asp,

이시욱
 res : {"castOnData":{"rstCode" : "0","rstMsg" : "SUCCESS","chatServerUrl" : ""}}


https://sys1.popkontv.kr:9002/AS/castData/castSetWaitTime.asp, strQuery : data=601UQM3MijjuzGjfnPd9DDe2fjfJi/1IA7xa9NmG1xCSrr3dLicTl2OL%2BbKLtSrmoSLU71vYe%2BL4pGdQwaeYyrTujAzwwgzO8MLzqxw0Zt%2B18aXUeqqXo5fRWbF9X3g6cJxn3b8415ab1kcwL0mMCfRAybglE0UGrPBXkQBvUdippjmmnodl9K1xGXcwCh7p&key=918&v=2  


https://sys1.popkontv.kr:9002/AS/castData/castSetWaitTime.asp,
 res : {"rst" : {"rstCode" : "1","rstMsg" : "error"}}



https://devsys.popkontv.kr:9002/AS/castData/castOnData.asp
요청값 : {"SC_CAD":"rtmp://live-popkontv.hscdn.com/pop_cast20|popaos7_P-00001_20240206133200","SC_CET":0,"SC_CLN":1,"SC_CR":"720x1280","SC_CSQ":"","SC_CST":0,"SC_PC":"P-00001","SC_PCC":"popaos7-20240206133200","SC_SI":"popaos7","SC_SP":"0x9144AF24F1ADD5E63AB8CB02F2175A13F5B5D00A9E4F800DCE6C054129691D0D","SC_WTM":0}

Function DateTime2Str( argDateTime, argFormat )
        DateTime2Str = argFormat
        DateTime2Str = Replace( DateTime2Str, "yyyy", Year( argDateTime ) )
        DateTime2Str = Replace( DateTime2Str, "yy", Right( Year( argDateTime ), 2 ) )
        DateTime2Str = Replace( DateTime2Str, "mm", Right("0"&Month( argDateTime ),2) )
        DateTime2Str = Replace( DateTime2Str, "dd", Right("0"&Day( argDateTime ),2) )
        DateTime2Str = Replace( DateTime2Str, "hh24", Right("0"&Hour( argDateTime ),2) )
        DateTime2Str = Replace( DateTime2Str, "mi", Right("0"&Minute( argDateTime ),2) )
        DateTime2Str = Replace( DateTime2Str, "ss", Right("0"&Second( argDateTime ),2) )
    End Function
nd = DateTime2Str( Now(), "yyyy-mm-dd hh24:mi:ss" )
    
{"data":"mICrU7IEJBfr0j4yQF4fYv/bG+bQXiHYr4Zp5z4whHjOQSep7Us4DhAxn6mprvWl7tdkE3riHz6dvyvtQAi+hcvpt0ROtQZVt+jBrk5Gwd0=","key":445, "v":2}



HYSERVERMASTER / 201928j94qJQ==^@%&

[https://sys1.popkontv.kr:9002/AS/webPage/callWeb.asp?data=zXAHo%2Fp5SyzseitB1vVwpmzSXWgU6LeH0eSI1FzMoFzRyZ%2B78kIibKSCy3akyN3nrpmQGzYYUGwz%0A1s1HhsL2kkxTTeB1xFWY7HPxKF7GloUyVQyqtqo3fCXzr5B%2BzyZER96LSb8t%2BLzmSIWxF58Qp%2Fiq%0AiJa1IkbSpbMnyKs%2Bl8RzfzpwGpEqv846J4XEmqQIgs4K%2FMYtH9vdP%2BPwK5AzUtol3j745pLDhsxV%0AgpChP9Rbi%2B4Sx6UblarcPg6uyIEARg%2Fo6sI3cVD2KF%2F3bExSC7SudPFqXsYkDKFU%2Fmpy4lNtC8c%2B%0AsOFonT3VJZ2wOS3jCCG5x6RTytaGX%2BtPn24HuylcOtXPovmibdhaWsteVGqBHLOB3T7T9mLuOijh%0AiLkn%0A&key=724&v=2](https://sys1.popkontv.kr:9002/AS/webPage/callWeb.asp?data=WVPyevzLjKPYbGsjilRedTtJe98WMf1FQIQPSk65SgWtu6hDZDp5XADrGT708BpKY71U4my4HGoX)

dbo.JBN_WEB_serviceCounsel_List

118.129.153.82
[B_BOARD].[dbo].USP_Get_PunshMmbrObjctnRqstDtl_001



192.168.1.82


[B_BOARD].[dbo].[USP_Get_PunshMmbrObjctnRqstDtl_001]

exec USP_Add_PunshMmbrObjctnRqst_001 'zsws1464', 'P-00001', 24103, 24202, '제목입니다3','내용입니다3'

exec USP_Add_PunshMmbrObjctnRqst_001 'polipark', 'P-00001', 24103, 24202, '제목입니다3','내용입니다3'

PPKNBRD 192.168.1.82
[B_BOARD].[dbo].[USP_Add_PunshMmbrObjctnRqst_001]
select * from PunshMmbrObjctnRqst with(nolock) order by 1 desc



2flaywd87Eo7OD8I/E9JkTrsaww/3SvxUhrFAetqXyCTD7PJDTxV1aQ/OzrHL1z9W5BJNUFjQUK9Syu2dle4QXN7l0QHyFK8mVVssJb2sDUGDQyZjNXiY+bKSozRkMsHPmwF8pbFuY62rP1StP9IkrdLI9J7vSYJEMEij+StX4BSnJQ300PWZcj1THS9WsHAE7wVxC1dWvhZLDdj5aZUrclq9WL//qPnu6Tkq5KxyOx3N7svNkqEBChtPcq6+I3IosbPkg+RkhOMSyTwvWXeyxUPyEPPdrW/HlIMfDuxSHHMt2GgKGZQzzD5jzkESTRgVGYe09T8oF6G9LLO3avSBmV+9ZyDa8Wnxs0tTOVTBIXPxW1m1ULqqa1zNBlGIvfS


/AS/webPage/callWeb.asp data=3eVzRdIB8JJtx3ccHyH22lBvzXjHHlbwovXsv5o3C%2BmIcbCHZoeVzp%2BQp46D9R4r3/7g1byeC58BOGRNfwCUcx29t3SUY%2B4ZgofCYqNMyOW0omBiCf7iTDWoO1FNqB6YSaAonApgkl1sCLpwsNrvR71FCle1X1GQn6KPSi9hTepzeasqbGGrvRvwBbIyO6C/E/YlP4nuoC8JwpDueXiE6Q==&key=680&v=2

팝콘
연예
http://news.mk.co.kr/cp/popcon/mbnstar.xml
스포츠
http://news.mk.co.kr/cp/popcon/sports.xml

셀럽
엔터
http://www.theceluv.com/popcon/enter.xml
연예
http://www.theceluv.com/popcon/star.xml


https://devsys.popkontv.kr:9002/AS/castData/naCastWatchOnOff.asp 

{"SC_AS":1,"SC_CPC":"P-00001","SC_CSI":"popaos7","SC_CT":0,"SC_CTYP":0,"SC_EP":7,"SC_ISCR":0,"SC_PC":"P-00001","SC_PCC":"popaos7-20231221165555","SC_PK":"","SC_SI":"popaos1","SC_SP":"0xFF794AFC2C094ADD967B34E4E062D1D3419B8EB2301C6596B7B90A83D1A85709","SC_VER":"7.1.01"}
CastWatchResModel(rst=ResultModel(rstCode=1, rstMsg=종료되거나 존재하지 않는 방송입니다., pageNum=0, totalPageNum=0, totalListNum=0), castWatch=CastWatch(accountLevel=0, fanLevel=0, fanLevelName=VIP, needCoin=0, coin=841769, castAddress=, isUpdate=0, castPath=0, vTK=, isJoint=False, category=12))



아이템 구매 성공시 
CoinName - 골드로즈, 향수, 구두, 고급핸드백, 골드바, ...
CoinValue - 300, 500, 700, 1000, 1500, ...
CoinName + CoinValue + 개를 구매하셨습니다.

코인 구매
SERVICE_COIN_NAME - 팝콘
itemCount - 300, 500, 700, 1000, 1500, ...
SERVICE_COIN_NAME + itemCount + 개를 구매하셨습니다.

점검 이후 14일 부터 불특정 사용자로부터 naAdultMain.asp 에서 500에러가 250건 이상 발생하고 있습니다.
2023-12-19 10:16:51 114.141.28.45 POST /AS/castData/naAdultMain.asp - 9002 - 223.32.190.185

bluewar111-20231017112040

v=2&data=rqx8xYSBb0JB68ok%2Bm1xdnOVwQwAXtfBCShOi0lDcJzx5IPc/L3uHdj8hItViYW2eO1DUH%2BI6XHPZ2M0frUJPZOsayiGIkyKc4oLzgmJnL6zWqzAdkWDg34L1a57WwUNQUXfrH3GdPRJWp3j0n3V%2BfE%2BIDBahy9cV0MarV8c3ldNHShWGsdXgJq1z0j0Uxst4fibjh6Nq34o8t8oAeRUTkEBdWLdOHrVvEft9vqWlXuUfmN9TXnJgqhcmXZ%2BGxsbQMTmahAyAymizi75S0eBCjso5ig/XS6v7AZDWINFwGo=&key=276

https://sys1.popkontv.kr:9002/AS/recVod/naMcVodWatchOnOff.asp
devtest9
0xC6542BB82142F8480DE5D11B29958F1F1C6A0F70CD22749C6A1C8E268F42BA93
P-00001
topsinger1
P-00001
0
2810913
1.12.3.0

https://sys1.popkontv.kr:9002/AS/recVod/naMcVodWatchOnOff.asp


{"rst":{"rstCode" : "0","rstMsg" : "SUCEESS"},
"vodWatch":{"needCoin":"", "vodPath":"https:\/\/media2.popkontv.hscdn.com\/CAST_VOD\/P-00001\/t\/to\/",
"playerType":"1", "vIsAdultSet":"0"}}


{"data":"8MuGTArlAx937Qia5zE/oClG9jYDEZQRfbWXOWA8FpRyz7xpfcoE08TFEayvPO5h","key":528, "v":1}



PVtransDt <!-- 가상계좌입금마감일 : 가상계좌에서만 사용합니다 예)20120101235959  -->

https://sys1.popkontv.kr:9002/helper/transKey.asp?SI=devtest9&PC=P-00001

https://www.popkontv.com/live/view?castId=lol555&partnerCode=P-00001

https://sys1.popkontv.kr:9002/json/helperinfo.asp?key=c1d6HbyX9Wwqusp238rsqA%3D%3D

https://gw.settlebank.co.kr/Lgcy/card/BillkeyAction.do

postJSONData = "PVersion=0001&PCommand=REQPAY" & _
            "&PMid=" & payment.PGID & _
            "&POid=" & order_no & _
            "&PAmt=" & accountAmount & _
            "&PBillkey=" & bill_key & _
            "&PGoods=" & product_name & _
            "&PUname=" & signId & _
            "&PUserid=" & signId & _
            "&PNoti="

192.168.1.24 결제/코인

  [B_ACCOUNT].[dbo].[LJC_autoAccount_request_list]
  

＜＞

https://sys1.popkontv.kr:9002/AS/webPage/callWeb.asp?data=Wi0nrAvOpkO/Ol9Y8R%2BxHSjfTQ%2BNr3yVg0jjDbJTl9FpAS%2BcRTc0erMqJ3RdXR7rkbxR2kov1AjCvBHB%2BFBn/t0o44T4FRy5bWjG6BmgFgichXmwSZT%2BmKfMvnZCVV5dL5jD3zAS7oH3kLsj00A1jw==&key=367&v=2

k2734091600707221225
kaira0000

201928j94qJQ==^@%&

192.168.1.24
B_ACCOUNT.dbo.autoAccount

결제 정보 기록
                핸드폰
                [B_ACCOUNT].[dbo].[YHS_Phone_Payment_Info_Insert]
                신용카드
                [B_ACCOUNT].[dbo].[YHS_Credit_Payment_Info_InsertLvl]
                
코인 지급
                [B_COIN].[dbo].[YHS_WEB_CoinAccount]
자동 충전 로그 기록
                [B_ACCOUNT].[dbo].[LJC_autoAccount_Log_insert]
                
[B_ACCOUNT].[dbo].[LJC_autoAccount_request_list]
popkontv.com/coin/settleBank/AutoPay.asp


https://theenmgw.daouoffice.com/app/board/13286/post/365266/?

[000002] [2023/11/24 11:09:21][INFR] : [CWebQuery::GetCallWebSite][CALL WEB] sURL : https://sys1.ajaetv.com:9002/AS/webPage/callWeb.asp?data=13eIw3f1/Uf/G8KpwzurNUwUnG5UuRhhcMBwfk3Cwp%2BJjjvqoAKP%2BiLLfgyJVMh1wiGe4ER6WgPVFoccPYpWE8lloyOPn98eNEeGraCRWgGqZarKof4fgBquteqIIy5IoZmoN2DXNwrFzLCGfaGL5hFeRRswCb5/mwxafRObuSzH%2BVYXo5MevtsjrpNjZqkYjR%2BfqoBHpO70hpiNHw5haw==&key=321&v=2, param : {"SC_SI":"bluewarajaetv","SC_SP":"0xB569E33BDD8F950C8D0511EFD47166B75C78D27E04A00ACCABDAA96945A46B52","SC_PC":"P-00095","SC_RPAT":"9","SC_WCP":"10"}  


118.129.153.93 DEV
[B_MEMBER].[dbo].[JBN_WEB_memberPublicSearch]
partnercode = 'P-00001'
signID = 'qas53'
pFileName
defaultProfile




https://thumb.popcast.co.kr/POPCAST_THUMB/sys_Thumb/P-00001/defaultProfile.png


http://bts.popkontv.kr/issues/10891

파일명이 데이터로 넘어온 경우
파일명 중에 defaultProfile 포함된
0:etc, 1:Android, 2:iPhone, 3:iPhone Enterprise(flex), 4:PC P/G, 5:PC WEB, 6:mobile WEB, 7:native andriod, 8:native iPhone, 9:신규PC, 12:맥 PC, 13:IOS VOD, 14:AOS VOD, 15: iPhone Enterprise New, 16: native iPhone New, 17: android store, 18: android one store, 19: 린크플러스 갤럭시스토어, 20: 린크플러스 안드로이드 수동 다운로드 앱


USP_Get_PrtsSvcSiteInfo_002

select top 10 SITE_PC_URL, SITE_MOBILE_URL from partnerSiteData  with(nolock) 
where SITE_PARTNER_CODE IN ('P-00095','P-00108', 'P-00023','P-00097','P-00074')
order by 1 desc





Error starting ApplicationContext. To display the conditions report re-run your application with 'debug' enabled.
2023-11-16T09:09:24,533 ERROR [restartedMain] o.s.b.SpringApplication: Application run failed
org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'redisCacheConfig.StandaloneRedisConfig': Injection of autowired dependencies failed; nested exception is java.lang.IllegalArgumentException: Could not resolve placeholder 'spring.profiles.active' in value "${spring.profiles.active}"



118.129.153.93,9190 개발서버 - 방송/회원
192.168.1.93,9190
[B_MEMBER].[dbo].[SSM_memberSignStatus_signAliveCheck]


https://gw.popkontv.kr/api/joinRoom : {"ccode":"pms3720-20231112231110", "signId":"zxcvbnm0103", "nickName":"\uD06C\uB77C\uC6B4", "memberSex":"1", "signPath":"7", "partnerCode":"P-00138", "accountLevel":"0", "fanLevel":"4", "bmkcnt":"", "fanList":[], "isGifter":"0", "sFanLevel":"1", "sSvcLevel":"4", "SvcLevelViewYn":"N", "chatBubbleCd":"", "isSecret":"0", "avatarURL":"", "avatarGIFURL":""} Err**
**

https://gw.popkontv.kr/api/joinRoom : {"ccode":"dhj100-20231112220504", "signId":"ciki0997", "nickName":"ACE\u2665", "memberSex":"1", "signPath":"7", "partnerCode":"P-00001", "accountLevel":"0", "fanLevel":"4", "bmkcnt":"", "fanList":[], "isGifter":"0", "sFanLevel":"1", "sSvcLevel":"22", "SvcLevelViewYn":"N", "chatBubbleCd":"", "isSecret":"0", "avatarURL":"", "avatarGIFURL":""} Err

https://gw.popkontv.kr/api/joinRoom : {"ccode":"sjsj9090-20231112200458", "signId":"ebate79", "nickName":"\uC801\uC0C9\uC218\uBC30\uC790", "memberSex":"0", "signPath":"8", "partnerCode":"P-00108", "accountLevel":"0", "fanLevel":"0", "bmkcnt":"", "fanList":[], "isGifter":"1", "sFanLevel":"8", "sSvcLevel":"23", "SvcLevelViewYn":"Y", "chatBubbleCd":"", "isSecret":"0", "avatarURL":"", "avatarGIFURL":""} Err


http://bts.popkontv.kr/issues/11132

settings_enm.xml
https://docs.google.com/document/d/17BEn9OKQtrxbaoEPWVwC6odAPP5WmzlnLzExWGBVHfw/edit
⠀<settings xmlns="http://maven.apache.org/settings/1.0.0" 
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">

  <proxies>    
  </proxies>
  <servers>	
    <server>
      <id>enm_repo</id>
      <username>admin</username>
      <password>enmadmin123#@!</password>
    </server>  
    <server>
      <id>enm_public</id>
      <username>enm_public</username>
      <password>enm_public123!@#</password>
    </server>     
  </servers>  
  <mirrors>
    <mirror>
      <id>enm_repo</id>
      <mirrorOf>*</mirrorOf>
      <url>http://114.141.29.145:15200/repository/maven-public/</url>
    </mirror>  
    <mirror>
      <id>enm_public</id>
      <mirrorOf>*</mirrorOf>
      <url>http://114.141.29.145:15200/repository/maven-public/</url>
    </mirror>   
  </mirrors>  
  <profiles>
  </profiles>
</settings>



jinjinURL:https://m.popkontv.com/Popkon/Proc/buyBankProc.asp
jinjinURL:https://pg.settlebank.co.kr/bank/MbNewBankAction.do
jinjinURL:https://pg.settlebank.co.kr/bank/page/optionEdit.do
jinjinURL:about:blank
jinjinURL:https://www.bankpay.or.kr:7443/MobilePayMO.do
jinjinURL:https://www.bankpay.or.kr:7443/MobilePayMO.do#
jinjinURL:https://bankpaypg.page.link/?link=https://eftpay.bankpay.or.kr?callbackfunc%3Dhttp%3A%2F%2Fmobile.bankpay.or.kr%2FRequestBankpay.do%26approve_no%3D20000253%26serial_no%3D0001145%26amount%3D2200%26hd_ep_type%3DSECUCERT%26firm_name%3D%ED%8C%9D%EC%BD%98%ED%8B%B0%EB%B9%84%26receipt_yn%3DN%26user_key%3D%26title%3D%26service_order%3DSE%26sbp_service_use%3DY%26sbp_tab_first%3DY%26fixed_bank_code%3D%26callbackparam1%3D873512%26returnURL%3D%26method%3DPOST%26container_deposit%3D%26&apn=com.kftc.bankpay.android&isi=398456030&ibi=kr.or.kftc.bankpaypg&ius=kftc-bankpay&efr=1
jinjinURL:https://pg.settlebank.co.kr/bank/page/receive.do
jinjinURL:https://pg.settlebank.co.kr/bank/page/complete.do
jinjinURL:https://m.popkontv.com/popkon/settleBank/GetPayParamResult.asp
jinjinURL:https://m.popkontv.com/popkon/popkon_buy.asp

118.129.153.90 개발서버 아이피

B_ACCOUNT.dob.USP_GetList_NbkkRfmInqrForBckofcSys_003


Sever Url : http://theenm-guard.hscdn.com/ZWMS/ZWMSTicketPublisher/ZWMSTicketPublisherServer2.asp
Data : ENC=S&VOD=rtmp%3A%2F%2Flive%2Dpopkontv%2Ehscdn%2Ecom%2Fpop%5Fcast20%2Fpopaos8%5FP%2D00001%5F20231031090730&SITE=popcontv&ID=bluewar111&IP=211%2E234%2E181%2E9&NIC=&WMSPUBPOINT=&PLAYER=ZWOWZA
Result : rtmp://live-popkontv.hscdn.com/pop_cast20/popaos8_P-00001_20231031090730?%24PDIz7wQIANXNy83OzMvOzMzR0NPMze38CQIA1czLy%2BjV6OvVzeQTAJtE%24


http://theenm-guard.hscdn.com/ZWMS/ZWMSTicketPublisher/ZWMSTicketPublisherServer2.asp

B_MEMBER.dbo.SSM_HYM_memberPage_partnerDefaultData_DD  -> B_MEMBER.dbo.SSM_HYM_memberPage_partnerDefaultData

/api/holidayInfo.asp


USP_Add_HldyExcng_By_OpenAPI




* End Point : http://apis.data.go.kr/B090041/openapi/service/SpcdeInfoService
    * 오퍼레이션 명 : getRestDeInfo
    * 서비스 인증키(Encoding) : xkJ%2FsNO5OIR7lueDX834DnuvsqFzdsaQ8FaiU9zhIsDV8KTgxKBWzXE6uKJyrhsEIceRwt%2BjCp%2Bkt1xnop27Gw%3D%3D
    * 서비스 인증키(Decoding) : xkJ/sNO5OIR7lueDX834DnuvsqFzdsaQ8FaiU9zhIsDV8KTgxKBWzXE6uKJyrhsEIceRwt+jCp+kt1xnop27Gw==
    * 요청 파라미터 
        - solYear : 년도 yyyy 4자리 숫자
        - pageNo : 페이징 번호
    * API 호출 샘플 URL
        - 2023년 공휴일 1페이지 : https://apis.data.go.kr/B090041/openapi/service/SpcdeInfoService/getRestDeInfo?serviceKey=xkJ%2FsNO5OIR7lueDX834DnuvsqFzdsaQ8FaiU9zhIsDV8KTgxKBWzXE6uKJyrhsEIceRwt%2BjCp%2Bkt1xnop27Gw%3D%3D&solYear=2023&pageNo=1
        - 2023년 공휴일 2페이지 : https://apis.data.go.kr/B090041/openapi/service/SpcdeInfoService/getRestDeInfo?serviceKey=xkJ%2FsNO5OIR7lueDX834DnuvsqFzdsaQ8FaiU9zhIsDV8KTgxKBWzXE6uKJyrhsEIceRwt%2BjCp%2Bkt1xnop27Gw%3D%3D&solYear=2023&pageNo=2

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

