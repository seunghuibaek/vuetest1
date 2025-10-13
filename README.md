
<code class="language-shell hljs" lang="shell" data-highlighted="yes"><span class="hljs-meta prompt_"># </span><span class="language-bash">Via scoop</span>
scoop install k9s
<span class="hljs-meta prompt_">
# </span><span class="language-bash">Via chocolatey</span>
choco install k9s
</code>


<code class="language-shell hljs" lang="shell" data-highlighted="yes"><span class="hljs-meta prompt_"># </span><span class="language-bash">Via LinuxBrew</span>
brew install derailed/k9s/k9s
<span class="hljs-meta prompt_">
# </span><span class="language-bash">Via PacMan</span>
pacman -S k9s
</code>


ip 정보
175.196.87.168
255.255.255.0
175.196.87.254

168.126.63.1
8.8.8.8

docuone ip : 172.17.12.6
BNG7W-CCTQ9-HP93Q-TJWT7-G6PKM

reg query “HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SoftwareProtectionPlatform” /v BackupProductKeyDefault


보안 부팅 켜짐으로 설정

컴퓨터에서 Chrome을 엽니다.
오른쪽 상단에서 더보기 더보기 다음 설정을 선택합니다.
개인 정보 보호 및 보안  다음 사이트 설정 다음 추가 콘텐츠 설정을 선택합니다.
기기 내 사이트 데이터를 선택합니다.
사이트에서 기기에 데이터를 저장하도록 허용을 사용 설정합니다.


https://support.google.com/chrome/answer/9175737?hl=ko-us

보안 부팅이 '꺼짐'으로 표시되는 경우, BIOS/UEFI 설정에서 직접 활성화해야 합니다. 이 과정은 PC 제조사나 마더보드 모델에 따라 다르므로, 각 제조사의 지침을 따르는 것이 중요합니다.

BIOS/UEFI 진입: PC를 재부팅하고 부팅 로고가 나타날 때 Delete 또는 F2 키를 반복해서 누릅니다. 🔑 (일부 제조사는 F10, F12, Esc 키를 사용하기도 합니다.)

'Secure Boot' 메뉴 찾기: BIOS/UEFI 설정 메뉴에서 'Boot', 'Security', 또는 **'Authentication'**과 같은 탭을 찾아 들어갑니다.

옵션 변경: 'Secure Boot' 옵션을 Enabled 또는 **On**으로 변경합니다.

UEFI 모드 설정: 만약 '보안 부팅 상태'를 변경할 수 없다면, 'BIOS 모드' 또는 **'OS Type'**을 'UEFI' 또는 **'Windows UEFI mode'**로 변경해야 할 수 있습니다.

변경 사항 저장 및 재시작: F10 키를 눌러 변경 사항을 저장하고 PC를 다시 시작합니다.


Beelink SER6 Pro

175.196.87.168
255.255.255.0
175.196.87.254

168.126.63.1
8.8.8.8

https://www.pqi.kr/application/lecturelist
' ######################################################################
    '   매개변수(Array) 생성
    ' ######################################################################
    Public Function makeParam(ByVal pName, ByVal pType, ByVal pDirection, ByVal pSize, ByVal pValue)
        If VarType(pSize) = 10 Then ' VarType 10 : adError
            Select Case pType
                Case adChar, adVarChar, adLongVarChar, adWChar, adVarWChar, adLongVarWChar
                    pSize = getCharSize(pValue)
            End Select
        End If

        makeParam = Array(pName, pType, pDirection, pSize, pValue)
    End Function
	
arrParams = Array(_
                        Db.makeParam("@pageSize", adInteger, adParamInput, 4, 4), _
                        Db.makeParam("@pageNo", adInteger, adParamInput, 4, 1), _
                        Db.makeParam("@grp", adUnsignedTinyInt, adParamInput, 4, 1), _
                        Db.makeParam("@notice", adWChar, adParamInput, 1, "Y"), _
                        Db.makeParam("@isView", adWChar, adParamInput, 1, ""), _
                        Db.makeParam("@skey", adVarWChar, adParamInput, 20, ""), _
                        Db.makeParam("@sword", adVarWChar, adParamInput, 30, ""), _
                        Db.makeParam("@totalCnt",  adInteger, adParamOutput, 4, 0)_
                    )
                    Set RsNotice = Db.execRs("SP_BOARD_LIST", DB_CMDTYPE_SP, arrParams, Nothing)
                    If Not RsNotice.bof And Not RsNotice.eof Then
                        Do Until RsNotice.Eof
						
Public Function execRs(ByVal sql, ByVal cmdType, ByRef arrParams, ByRef Db)
        Dim f
        Dim Cmd, Rs

        Call addDebug(sql)

        Call connect(Db)

        Set Cmd = Server.CreateObject("ADODB.Command")
        Set Rs = Server.CreateObject("ADODB.RecordSet")

        Cmd.ActiveConnection = Db
        Cmd.CommandText = sql
        Cmd.CommandType = cmdType
        Set Cmd = collectParams(Cmd, arrParams)

        Rs.CursorLocation = adUseClient
        Rs.Open Cmd, ,adOpenStatic, adLockReadOnly

        If cmdType = adCmdStoredProc Then
            For f = 0 To Cmd.Parameters.Count - 1
                If Cmd.Parameters(f).Direction = adParamOutput Or Cmd.Parameters(f).Direction = adParamInputOutput Or Cmd.Parameters(f).Direction = adParamReturnValue Then
                    If IsArray(arrParams) Then
                        arrParams(f)(4) = Cmd.Parameters(f).Value
                    Else
                        Exit For
                    End If
                End If
            Next
        End If

        Set Cmd.ActiveConnection = Nothing
        Set Cmd = Nothing

        If Rs.State = adStateClosed Then Set Rs.Source = Nothing
        Set Rs.ActiveConnection = Nothing

        Set execRs = Rs
        Set Rs = Nothing
    End Function

<%
' 공통: 커넥션 열고 ARITHABORT ON 보장
Function OpenSqlConn(connStr)
  Dim cn
  Set cn = Server.CreateObject("ADODB.Connection")
  cn.Open connStr
  ' 세션 옵션은 커넥션에 유지됨. 풀링 대비해서 항상 명시
  cn.Execute "SET ARITHABORT ON"
  Set OpenSqlConn = cn
End Function

' 예: 서로 다른 DB 두 개에 접속
Dim cs1, cs2
cs1 = "Provider=MSOLEDBSQL;Server=SRV1;Database=DB1;UID=xxx;PWD=yyy;"
cs2 = "Provider=MSOLEDBSQL;Server=SRV2;Database=DB2;UID=aaa;PWD=bbb;"

Dim cn1, cn2
Set cn1 = OpenSqlConn(cs1)
Set cn2 = OpenSqlConn(cs2)

' 재사용 가능한 SP 호출 헬퍼(매번 같은 방식으로 호출 가능)
Function ExecSp(cn, spName, paramsArray)
  Dim cmd, i
  Set cmd = Server.CreateObject("ADODB.Command")
  Set cmd.ActiveConnection = cn
  cmd.CommandType = 4 ' adCmdStoredProc
  cmd.CommandText = spName

  ' 파라미터가 필요하면 paramsArray = Array(Array(name, type, dir, size, value), ...)
  If IsArray(paramsArray) Then
    For i = 0 To UBound(paramsArray)
      Dim p
      p = paramsArray(i)
      cmd.Parameters.Append cmd.CreateParameter(p(0), p(1), p(2), p(3), p(4))
    Next
  End If

  Set ExecSp = cmd.Execute
End Function

' 사용 예시 1: DB1의 SP 실행
' ADO 상수: adVarChar=200, adParamInput=1 등은 상수 선언부 있으면 사용
Const adVarChar = 200, adInteger = 3, adParamInput = 1
Call ExecSp(cn1, "dbo.usp_DoSomethingInDB1", Array( _
  Array("@UserId", adInteger, adParamInput, 0, 123) _
))

' 사용 예시 2: DB2의 SP 실행
Call ExecSp(cn2, "dbo.usp_DoAnotherThingInDB2", Array( _
  Array("@Code", adVarChar, adParamInput, 20, "ABC") _
))

' 마무리
cn1.Close : Set cn1 = Nothing
cn2.Close : Set cn2 = Nothing
%>

-------


If Rs.State = adStateClosed Then Set Rs.Source = Nothing
        Set Rs.ActiveConnection = Nothing
		
'********************************************************************************
'* RecordSet 개체 소멸
'********************************************************************************
Function rsClose()
	If isObject(rs) Then
		Set rs = Nothing
	End If
	rs = Null
End Function

If VarType(db) = vbString Then
		If db.state Then
		   db.Close
		End If
		Set db = Nothing
	End If

	db = Null

OLEDB_CTICAST8.Execute "SET ANSI_WARNINGS ON; SET ARITHABORT ON;"

ExecuteNonQuery

With objCmd
    Call cmdPramDel(objCmd)
    cmdRtnCode = ""
    .CommandText = "[B_CASTDATA].[dbo].[JBN_JSON_castRecordFile_Delete]"
    .CommandType = &H0004  ' adCmdStoredProc
    .ActiveConnection = OLEDB_CTICAST8
    .Parameters.Append .CreateParameter("@pk_code", adBigInt, adParamInput, 0)
    .Parameters("@pk_code") = CLng(pk_code)
    .Execute , , adExecuteNoRecords
    .ActiveConnection = Nothing
End With


conn.Execute "SET ANSI_WARNINGS ON; SET ARITHABORT ON;";
' 확인
Set rs = conn.Execute("SELECT SESSIONPROPERTY('ARITHABORT') AS v")
Response.Write "ARITHABORT=" & rs("v") ' 1 이면 ON

Dim objCmd, cmdRs
Dim objCon, cmdTxt, objRs
Set objCmd = server.createObject("ADODB.COMMAND")
Set objCon = server.createObject("ADODB.CONNECTION")
Set objRs = server.createObject("ADODB.RECORDSET")


Set rs = conn.Execute("SELECT CASE WHEN SESSIONPROPERTY('ARITHABORT') = 1 THEN 'ON' ELSE 'OFF' END AS arithabort")
Response.Write "ARITHABORT = " & rs("arithabort")

Set rs = conn.Execute("
  SELECT 
    @@OPTIONS AS options_mask,
    CASE WHEN (@@OPTIONS & 64) = 64 THEN 'ON' ELSE 'OFF' END AS arithabort
")
Response.Write "ARITHABORT = " & rs("arithabort") & " (mask=" & rs("options_mask") & ")"

Set rs = conn.Execute("
  SELECT 
    @@SPID AS spid,
    set_options,
    CASE WHEN (set_options & 64) = 64 THEN 'ON' ELSE 'OFF' END AS arithabort
  FROM sys.dm_exec_sessions
  WHERE session_id = @@SPID
")
Response.Write "SPID=" & rs("spid") & " / ARITHABORT=" & rs("arithabort")
------------
SQLOLEDB 대신 MSOLEDBSQL

strSQL = "SELECT @@VERSION AS SQLVersion"
  Set rs = conn.Execute(strSQL)
  
<connectionStrings>
  <add name="MyDB"
       connectionString="Data Source=서버명;Initial Catalog=DB명;Integrated Security=True;ArithAbort=True;" 
       providerName="System.Data.SqlClient" />
</connectionStrings>


Set conn = Server.CreateObject("ADODB.Connection")

' SQLOLEDB.1 사용
conn.Open "Provider=SQLOLEDB.1;Data Source=서버명;Initial Catalog=DB명;User ID=계정;Password=암호;"

' 세션 옵션 강제
conn.Execute "SET ARITHABORT ON"
-------------


Set rs = conn.Execute("DBCC USEROPTIONS")
Do Until rs.EOF
  Response.Write rs(0) & " = " & rs(1) & "<br>"
  rs.MoveNext
Loop
rs.Close
Set rs = Nothing

Set conn = Server.CreateObject("ADODB.Connection")

' SQLOLEDB.1 사용
conn.Open "Provider=SQLOLEDB.1;Data Source=서버명;Initial Catalog=DB명;User ID=계정;Password=암호;"

' 세션 옵션 강제
conn.Execute "SET ARITHABORT ON"
---------------------

ARITHABORT 옵션이 OFF 설정된 클라이언트 연결의 경우, 최적의 실행계획을 부여 받지 못하여 쿼리 실행 시간이 현저히 지연될 수 있습니다.

DBMS 연결 시, ARITHABORT = ON 설정 확인 요청 드립니다.

연결 설정 변경은 반드시 정기점검 시 진행 바랍니다.

SELECT TOP 100
       [Object_Name] = object_name(st.objectid),
       creation_time,
       last_execution_time,
       total_cpu_time = total_worker_time / 1000,
       avg_cpu_time = (total_worker_time / execution_count) / 1000,
       min_cpu_time = min_worker_time / 1000,
       max_cpu_time = max_worker_time / 1000,
       last_cpu_time = last_worker_time / 1000,
       total_time_elapsed = total_elapsed_time / 1000 ,
       avg_time_elapsed = (total_elapsed_time / execution_count) / 1000,
       min_time_elapsed = min_elapsed_time / 1000,
       max_time_elapsed = max_elapsed_time / 1000,
       avg_physical_reads = total_physical_reads / execution_count,
       avg_logical_reads = total_logical_reads / execution_count,
       execution_count,
       SUBSTRING(st.text, (qs.statement_start_offset/2) + 1,
             (
                   (
                         CASE statement_end_offset
                               WHEN -1 THEN DATALENGTH(st.text)
                               ELSE qs.statement_end_offset
                         END
                         - qs.statement_start_offset
                   ) /2
             ) + 1
       ) as statement_text
  FROM sys.dm_exec_query_stats qs
 CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) st
 WHERE Object_Name(st.objectid) IS NOT NULL
   AND st.dbid = DB_ID()
 ORDER BY db_name(st.dbid), total_worker_time / execution_count DESC
---------------------
SELECT 
    TOP 1000
    (qs.total_elapsed_time / qs.execution_count) as each_elapsed_time,
    st.text as query
FROM 
    sys.dm_exec_query_stats as qs WITH(NOLOCK)
CROSS APPLY
    sys.dm_exec_sql_text(qs.sql_handle) as st
WHERE
    (qs.total_elapsed_time / qs.execution_count) > 1000000
ORDER BY
    each_elapsed_time
;
------------

 


호출해야 하는 SP는
JBN_JSON_castRecordFile_Delete 이고
DelVodAdm.asp 로 생성해주시면 될 것 같습니다
오후 01:21

황대형
사용자가 삭제한 대화입니다.
오후 01:22

황대형
DelVodAdm.asp 로 생성해주시면 될 것 같습니다 > 뒤에 Adm 으로만 붙여주시면 될 것 같습니다

https://service.whatap.io/account/login
http://114.141.28.23:3000/d/edyqhs82gmvb4c/sys1?orgId=1&refresh=10s


{
  "statusCd": "E5000",
  "statusMsg": "\n### Error querying database.  Cause: com.microsoft.sqlserver.jdbc.SQLServerException: 테이블 'B_BOARD.dbo.serviceCounsel', 열 'nTitle'에 NULL 값을 삽입할 수 없습니다. 열에는 NULL을 사용할 수 없습니다. INSERT이(가) 실패했습니다.\n### The error may exist in URL [jar:file:/app/next-app-popkon.jar!/BOOT-INF/classes!/mapper/basement/oledb9_db.xml]\n### The error may involve com.enm.api.rest.basement.mapper.OLEDB9Mapper.JBN_WEB_serviceCounsel_Insert-Inline\n### The error occurred while setting parameters\n### SQL: {             call [B_BOARD].[dbo].[JBN_WEB_serviceCounsel_Insert] (                 ?,                 ?,                 ?,                 ?,                 ?,                 ?,                 ?,                 ?,                 ?             )         }\n### Cause: com.microsoft.sqlserver.jdbc.SQLServerException: 테이블 'B_BOARD.dbo.serviceCounsel', 열 'nTitle'에 NULL 값을 삽입할 수 없습니다. 열에는 NULL을 사용할 수 없습니다. INSERT이(가) 실패했습니다.\n; 테이블 'B_BOARD.dbo.serviceCounsel', 열 'nTitle'에 NULL 값을 삽입할 수 없습니다. 열에는 NULL을 사용할 수 없습니다. INSERT이(가) 실패했습니다.; nested exception is com.microsoft.sqlserver.jdbc.SQLServerException: 테이블 'B_BOARD.dbo.serviceCounsel', 열 'nTitle'에 NULL 값을 삽입할 수 없습니다. 열에는 NULL을 사용할 수 없습니다. INSERT이(가) 실패했습니다.",
  "data": null
}


curl -i 'https://pay.example.com/api/pay' \
  -H 'User-Agent: Mozilla/5.0 (iPhone; CPU iPhone OS 16_6 like Mac OS X)...' \
  -H 'Content-Type: application/json' \
  -d '{"amount":1000,"returnUrl":"https://example.com/결제완료"}'
---------------------------


도메인과 ssl 이슈로 pwa 기능 불가능하여 
다른 호스팅 서비스 이용해서 구현했습니다.

https://bluewar.ivyro.net/
bluewar111@nate.com / as1234

PC 설치 : 주소줄에서 우측 모니터 모양 클릭
Andorid 설치 : Chrome 브라우저에서 사이트 접속 > 주소 표시줄 오른쪽의 점 세개 모양(더보기 메뉴) 클릭 > 홈 화면에 추가 선택
IOS 설치 : safari 브라우저에서 사이트 접속 > 하단의 화살표 모양(공유 버튼) 클릭 > 홈 화면에 추가 선택




https://dev.popkontv.kr/api/makeRoom : {"ccode":"popaos6-20250804095121", "signId":"popaos6", "nickName":"TEST6", "memberSex":"1", "signPath":"7", "partnerCode":"P-00001", "accountLevel":"1", "fanLevel":"", "bmkcnt":"0", "fanList":[{ "fanRank" : "0", "fanNickName" : "\uB098\uB2945\uBC88\uC774\uC5D0\uC694", "fanSignId" : "popaos5", "fanLevel" : "0", "fanSex" : "1", "fanPrintId" : "popa***", "sFanLevel" : "1", "sSvcLevel" : "1", "partnerCode" : "P-00001"},{ "fanRank" : "1", "fanNickName" : "\uBAA8\uBC14\uC77C\uD300\uBAA8\uBC14\uC77C\uD300", "fanSignId" : "popaos2", "fanLevel" : "0", "fanSex" : "1", "fanPrintId" : "popa***", "sFanLevel" : "1", "sSvcLevel" : "1", "partnerCode" : "P-00001"},{ "fanRank" : "2", "fanNickName" : "\uC0AC\uC6A9\uAE08\uC9C0\uB2C9\uB124\uC784", "fanSignId" : "yukimajuri", "fanLevel" : "0", "fanSex" : "0", "fanPrintId" : "yukim*****", "sFanLevel" : "1", "sSvcLevel" : "1", "partnerCode" : "P-00001"},{ "fanRank" : "3", "fanNickName" : "TEST_4", "fanSignId" : "popios4", "fanLevel" : "0", "fanSex" : "1", "fanPrintId" : "popi***", "sFanLevel" : "1", "sSvcLevel" : "1", "partnerCode" : "P-00001"},{ "fanRank" : "4", "fanNickName" : "\uD504\uB9AC\uBBF8\uC5C4\uB2C9\uB124\uC784\uC784", "fanSignId" : "popaos1", "fanLevel" : "0", "fanSex" : "1", "fanPrintId" : "popa***", "sFanLevel" : "1", "sSvcLevel" : "1", "partnerCode" : "P-00001"},{ "fanRank" : "5", "fanNickName" : "\uC77C\uC774\uC0BC\uC0AC\uC624\uC721\uCE60\uD314", "fanSignId" : "popios2", "fanLevel" : "0", "fanSex" : "1", "fanPrintId" : "popi***", "sFanLevel" : "1", "sSvcLevel" : "1", "partnerCode" : "P-00001"},{ "fanRank" : "6", "fanNickName" : "AOS\uD14C\uC2A4\uD2B87\uBC88", "fanSignId" : "popaos7", "fanLevel" : "0", "fanSex" : "1", "fanPrintId" : "popa***", "sFanLevel" : "1", "sSvcLevel" : "1", "partnerCode" : "P-00001"},{ "fanRank" : "7", "fanNickName" : "hrryu", "fanSignId" : "hrryu9619", "fanLevel" : "0", "fanSex" : "0", "fanPrintId" : "hrry*****", "sFanLevel" : "1", "sSvcLevel" : "1", "partnerCode" : "P-00001"},{ "fanRank" : "8", "fanNickName" : "<br\/>", "fanSignId" : "frontweb01", "fanLevel" : "0", "fanSex" : "1", "fanPrintId" : "front*****", "sFanLevel" : "1", "sSvcLevel" : "1", "partnerCode" : "P-00001"},{ "fanRank" : "9", "fanNickName" : "CL_TEST1", "fanSignId" : "celaos1", "fanLevel" : "2", "fanSex" : "1", "fanPrintId" : "cela***", "sFanLevel" : "1", "sSvcLevel" : "1", "partnerCode" : "P-00117"}], "groupLevelNmList" : [{"0" : "VIP"},{"1" : "\uB2E4\uC774\uC544\uBAAC\uB4DC"},{"2" : "\uACE8\uB4DC"},{"3" : "\uC2E4\uBC84"}],"sCastLevel":"22", "sSvcLevel":"23", "waitTimeMin":"0", "SvcLevelViewYn":"Y", "chatBubbleCd":"", "exeBit":"","isAdult":"False", "passWordKey":"zxcv", "castResolution":"360x640"} Err


xml err : -2147012867 : 서버에 연결할 수 없습니다.


[
2025-07-31 17:02:22.780 30594-30806 okhttp.OkHttpClient     com.social.media.broadcast.aospop.e  I  --> POST https://devsys.popkontv.kr:9002/AS/castData/castWaitData.asp
2025-07-31 17:02:29.968 30594-30806 okhttp.OkHttpClient     com.social.media.broadcast.aospop.e  I  <-- 200 https://devsys.popkontv.kr:9002/AS/castData/castWaitData.asp (7187ms)

http://175.196.87.168:82/

 .pwa-install-app](https://devsys.popkontv.kr:9002/AS/castData/castOnData.asp
{
  "SC_CAD": "rtmp://live-popkontv.hscdn.com/pop_cast20|popaos6_P-00001_20250804095121",
  "SC_CET": 0,
  "SC_CLN": 1,
  "SC_CR": "360x640",
  "SC_CSQ": "",
  "SC_CST": 0,
  "SC_PC": "P-00001",
  "SC_PCC": "popaos6-20250804095121",
  "SC_SI": "popaos6",
  "SC_SP": "0xFB03C61F91D6ABA7F47514A48B3C1072E97BFC88AB1C6393E942C1AEC8CB0B09",
  "SC_VITC": "",
  "SC_WTM": 0
}


{
  "castOnData": {
    "rstCode": "1",
    "rstMsg": "일시적인 장애가 발생했습니다. 잠시후 다시 시도 해주세요.",
    "chatServerUrl": "https://dev.popkontv.kr:1920"
  }
}

)
 -------
https://bluewar.ivyro.net/
bluewar111@nate.com / as1234

PC 설치 : 주소줄에서 우측 모니터 모양 클릭
Andorid : Chrome 브라우저에서 사이트 접속 > 주소 표시줄 오른쪽의 점 세개 모양(더보기 메뉴) 클릭 > 홈 화면에 추가 선택
IOS : safari 브라우저에서 사이트 접속 > 하단의 화살표 모양(공유 버튼) 클릭 > 홈 화면에 추가 선택



https://devsys.popkontv.kr:9002/dev/

redis-cli monitor


175.196.87.168
bluewar / as1234


https://rhymix.org/free/1834251


Expression [#] @1: EL1044E: Unexpectedly ran out of input

"statusMsg": "Cache 'getBrdcrsvclvlCache' does not allow 'null' values. Avoid storing null via '@Cacheable(unless=\"#result == null\")' or configure RedisCache to allow 'null' via RedisCacheConfiguration.",

@Cacheable(value = "getBrdcrsvclvlCache", key = "#yourKey", unless = "#result == null")
public YourReturnType yourMethod(String yourKey) {
    // your logic
}


USP_GetList_CastOnListSrchForAPI_005

MMBRI :n8358061328313230127
SVC_SE_CD : 3
OAUTH_USRI : 207663525
isServiceClose : 0
LoginAfterYear : 0

Ss쏘공주


k5247170844903230127

비밀번호 조회 : [B_MEMBER].[dbo].[USP_Get_OauthMmbrYnChck_002]
@inySvcSeCd : 3
@vchOauthUsri : 2010572411
@vchPartnerCode : P-00001

로그인 sp : [B_MEMBER].[dbo].[USP_Mod_MmbrLoginProcessEncpt_002]
signId = 'n9130115249020231114' AND partnerCode = 'P-00001'

URL:https://stagesys.popkontv.com:9002/AS/member/naSignOn.asp
 PARAMS:["SC_SP": "0x4012171FA6B1699E9DB91E9E0373F8D2A0AA17BFD00E75B8D27A0056AF11B026", "SC_SK": "0B8DB7E0-052C-4687-B174-FA2C2992988A", "SC_SI": "n9130115249020231114", "SC_PC": "P-00001", "SC_EP": "3"] 
- Result -
 {"rst":{"rstCode" : "1","rstMsg" : "로그인이 실패하였습니다.[SSP]"},"signOn" : {"memberSex" : "","isAdult" : "","nickName" : "","memberType" : "","pFileName" : "","accountLevel" : "","pwdCode" : "0x4012171FA6B1699E9DB91E9E0373F8D2A0AA17BFD00E75B8D27A0056AF11B026","isNameCheck" : "0","levelUp" : "0","svcLvl" : ""},"memberBlockCheck" : {"isBlock" : "0","isLoginBlock" : "0","blockRegDate" : "","blockDate" : "","blockMemo" : ""}} 
-----------------------------------------


com.enm.api.rest.sys.level.controller.LevelSysController.getMcLevel(LevelSysController.java:108), com.enm.api.common.filter.CommonFilter.doFilter(CommonFilter.java:34), :Cannot deserialize; nested exception is org.springframework.core.serializer.support.SerializationFailedException: Failed to deserialize payload. Is the byte array a result of corresponding serialization for DefaultDeserializer?; nested exception is java.io.InvalidClassException: com.enm.api.rest.basement.member.model.dto.MemberLevelDto; incompatible types for field lvlPer
^[[30m2025-07-10 09:15:22^[[m ^[[32m[INFO ]^[[m ^[[1;33mEnmHandleInterceptor.logHandle(260)^[[m:
[{/v1/level/cast} RES] :
{
  "statusCd" : "E5000",
  "statusMsg" : "Cannot deserialize; nested exception is org.springframework.core.serializer.support.SerializationFailedException: Failed to deserialize payload. Is the byte array a result of corresponding serialization for DefaultDeserializer?; nested exception is java.io.InvalidClassException: com.enm.api.rest.basement.member.model.dto.MemberLevelDto; incompatible types for field lvlPer",
  "data" : null
}


[B_MEMBER].[dbo].[USP_Get_OauthMmbrYnChck_002]
여기서 조회된 아이디와 비밀번호로 로그인 신청을 하거든요


암호화된 비밀번호로 OUTPUT 받으셨으면.

B_MEMBER.dbo.USP_Mod_MmbrLoginProcessEncpt_002 로 로그인 되어야 합니다.
USP_Mod_MmbrLoginProcess_002 는 평문 비밀번호 로그인시 사용


더 확인이 필요하겠지만, 결국 ,
오픈인증 가입회원
 - USP_Mod_MmbrLoginProcessEncpt_002
일반 회원
 - USP_Mod_MmbrLoginProcess_002
   

[B_MEMBER].[dbo].[USP_Get_OauthMmbrYnChck_002]

[B_MEMBER].[dbo].[USP_Get_MmbrLoginPrtsCd_002]
[B_MEMBER].[dbo].[USP_Mod_MmbrLoginProcess_002]


오지훈
/member/snsJoinChk.asp
{
  "SC_SC": "2",
  "SC_SK": "2753391535",
  "SC_PC": "P-00001"
}


{
  "rst": {
    "rstCode": "0",
    "rstMsg": "로그인 처리 가능",
    "signId": "k2613164109630231004",
    "signPwd": "0xFDD5561C206703B3891DC1F391D7844CB2B66741AC856F93CFB6EA7929A5E670",
    "isNickChgNeed": "0"
  }
}




/member/naSignOnCast.asp
{
  "SC_SI": "k2613164109630231004",
  "SC_SP": "0xFDD5561C206703B3891DC1F391D7844CB2B66741AC856F93CFB6EA7929A5E670",
  "SC_PC": "P-00001",
  "SC_EP": "7",
  "SC_SK": "7538c524-669c-4c85-8d7b-37ec93be9b4d"
}


{
  "rst": {
    "rstCode": "1",
    "rstMsg": "아이디 또는 비밀번호를 다시 확인하세요."
  },
  "signOn": {
    "memberSex": "",
    "isAdult": "",
    "nickName": "",
    "memberType": "",
    "pFileName": "",
    "accountLevel": "",
    "pwdCode": "0xFDD5561C206703B3891DC1F391D7844CB2B66741AC856F93CFB6EA7929A5E670",
    "partnerCode": "P-00001",
    "isNewBJ": "0",
    "isNameCheck": "0",
    "levelUp": "0",
    "svcLvl": ""
  },
  "memberBlockCheck": {
    "isBlock": "0",
    "isLoginBlock": "0",
    "blockRegDate": "",
    "blockDate": "",
    "blockMemo": ""
  }
}
--------------------------

ttps://plugins.jetbrains.com/plugin/8321-free-mybatis-plugin


define('FS_METHOD', 'direct');

Listen 80
<VirtualHost *:8080>
    ServerName localhost
    DocumentRoot "/var/www/html/theenm"
    <Directory "/var/www/html/theenm">
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog logs/site1-error_log
    CustomLog logs/site1-access_log combined
</VirtualHost>

Listen 81
<VirtualHost *:81>
    ServerName wordpress
    DocumentRoot "/var/www/html/wordpress"
    <Directory "/var/www/html/wordpress">
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
    ErrorLog logs/site2-error_log
    CustomLog logs/site2-access_log combined
</VirtualHost>


 
개인계정에서 theenm계정으로 전환하신다음에 
theenm 계정에서 작업하셔야 해요
sudo su - theenm
201928+IcytWvR^@%&
-------------
https://roykeum1998.tistory.com/181

서버 설치
sudo yum install php mysql-server
service mysqld start -- 시작해야 mysql 접속 가능
gd 라이브러리 설치
sudo yum install php-gd

mysql db, user 생성
    sudo mysql -uroot



    # mydatabase, myuser, mypassword는 상황에 맞게 수정하세요
    CREATE DATABASE mydatabase;
    CREATE USER 'myuser'@'localhost' IDENTIFIED BY 'mypassword';
    GRANT ALL PRIVILEGES ON mydatabase.* TO 'myuser'@'localhost';

mysql 시작
sudo systemctl start mysqld
자동 시작 설정
sudo systemctl enable mysqld
보안설정
sudo mysql_secure_installation

아파치 설치
yum install httpd

아파치 시작
systemctl start httpd

아파치 자동 시작
systemctl enable httpd

아파치 상태 확인
systemctl status httpd

웹 안뜨는 경우 
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-service=https
sudo firewall-cmd --reload

data 디렉토리의 퍼미션을 707로 변경하여 주십시오.
아래 실행 후 진행
# setenforce 0

짧은 주소
etc/httpd   httpd.conf 수정
<Directory "/var/www/html">
아래에 AllowOverride none 를 All로 변경 -> 재시작

모니터링 툴 설치
https://velog.io/@suk13574/Promehteus-prometheus-%EC%82%AC%EC%9A%A9%ED%95%B4%EB%B3%B4%EA%B8%B0-%EC%84%A4%EC%B9%98-%EA%B5%AC%EC%84%B1-%EC%8B%A4%ED%96%89

https://tikus.tistory.com/5
wget 설치 필요
yum install wget

--   prometheus 설정

cmd> vi conf/prometheus.yml
---
global:
  scrape_interval: 15s
  evaluation_interval: 15s

alerting:
  alertmanagers:
    - static_configs:
        - targets:

scrape_configs:
  - job_name: "prometheus"
    static_configs:
      - targets: ["192.168.56.112:9090"]

cmd> vi startPrometheus.sh
./bin/prometheus \
  --config.file=/monitoring/prometheus/prometheus-2.41.0.linux-amd64/conf/prometheus.yml \
  --storage.tsdb.path=/monitoring/prometheus/prometheus-2.41.0.linux-amd64/data &

cmd> vi stopPrometheus.sh
ps -ef | grep prometheus | grep 2.41.0 | awk {'print "kill -9 " $2'} | sh -x

cmd> chmod 750 *.sh

-- 실행
cmd> ./startPrometheus.sh

-- 데몬 등록
cmd> sudo vi /etc/systemd/system/prometheus.service
[Unit]
Description=Prometheus Server
Documentation=https://prometheus.io/docs/introduction/overview/
After=network-online.target

[Service]
User=grafana
Restart=on-failure
ExecStart=/monitoring/prometheus/prometheus-2.41.0.linux-amd64/bin/prometheus \
  --config.file=/monitoring/prometheus/prometheus-2.41.0.linux-amd64/conf/prometheus.yml \
  --storage.tsdb.path=/monitoring/prometheus/prometheus-2.41.0.linux-amd64/data

[Install]
WantedBy=multi-user.target

cmd> sudo systemctl daemon-reload
cmd> sudo systemctl enable prometheus --now

cmd> ./stopPrometheus.sh
cmd> sudo systemctl restart prometheus

cmd> curl -X GET http://192.168.56.112:9090
<a href="/graph">Found</a>.

grafana 설치
sudo yum install -y https://dl.grafana.com/enterprise/release/grafana-enterprise-12.0.2-1.x86_64.rpm

grafana 데몬 등록
cmd> sudo vi /etc/systemd/system/grafana.service
[Unit]
Description=Grafana Server
Documentation= https://grafana.com/docs/grafana/latest/
Wants=network-online.target
After=network-online.target

[Service]
User=grafana
Group=grafana
Type=simple
Restart=on-failure
WorkingDirectory=/monitoring/grafana/grafana-9.3.2
ExecStart=/monitoring/grafana/grafana-9.3.2/bin/grafana-server

[Install]
WantedBy=multi-user.target

cmd> sudo systemctl daemon-reload
cmd> sudo systemctl enable grafana --now

cmd> ./stopGrafana.sh
cmd> sudo systemctl restart grafana

cmd> curl -X GET http://192.168.56.111:3000
INFO [01-25|16:25:48] Request Completed
                        logger=context userId=0 orgId=0 uname= method=GET path=/ status=302 remote_addr=192.168.56.111 time_ms=0 duration=266.603µs size=29 referer= handler=/
<a href="/login">Found</a>.



-- 워드 프로세스 설치
https://comnrose.tistory.com/entry/%EB%A6%AC%EB%88%85%EC%8A%A4-%EC%84%9C%EB%B2%84%EC%97%90-%EC%9B%8C%EB%93%9C%ED%94%84%EB%A0%88%EC%8A%A4wordpress-%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0-1%ED%8E%B8


wordpress
theenm / as1234

테마 추가하기 시 오류 발생
Warning: wp_update_themes(): 예상하지 않은 오류가 발생했습니다.

ssh 연결 정보 확인
curl https://api.wordpress.org/

해결
sudo setenforce 0


wp-content/plugins 폴더 및 하위 파일들의 권한을 확인
폴더: 일반적으로 755
파일: 일반적으로 644

https://docs.redhat.com/ko/documentation/red_hat_enterprise_linux/8/html/deploying_different_types_of_servers/setting-up-and-configuring-nginx_deploying-different-types-of-servers
nginx 설치
sudo yum install nginx

# firewall-cmd --permanent --add-port={8080/tcp,8081/tcp}
# firewall-cmd --reload

서비스 등록
systemctl enable nginx

nginx 구동
systemctl start nginx

포트 두개 설정
/etc/nginx/nginx.conf

http {
  ...
  server {
    listen 80;
    server_name example.com;
    root /usr/share/nginx/html/site1;
    index index.html;
  }

  server {
    listen 8080;
    server_name example.org;
    root /usr/share/nginx/html/site2;
    index index.html;
  }
  ...
}

sudo firewall-cmd --permanent --add-port=80/tcp
sudo firewall-cmd --permanent --add-port=8080/tcp
sudo firewall-cmd --reload

서버 php 연결
php-fpm

install php php-fpm php-mysqlnd php-xml php-mbstring


server {
    listen       80;
    server_name  localhost;
    root         /usr/share/nginx/html;

    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include        fastcgi_params;
        fastcgi_pass   unix:/run/php-fpm/www.sock;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }

    location ~ /\.ht {
        deny all;
    }
}



php 연동
sudo vi /etc/php-fpm.d/www.conf
user = nginx
group = nginx
listen = /run/php-fpm/www.sock
listen.owner = nginx
listen.group = nginx
listen.mode = 0660

---------------------
WP_DEBUG to false in your wp-config.php
define('WP_DEBUG', false);

아래는 추가 설정
ini_set('display_errors','Off');
ini_set('error_reporting', E_ALL );
define('WP_DEBUG', false);
define('WP_DEBUG_DISPLAY', false);

-----------
wp-config.php 아래 코드 추가
define('FS_METHOD', 'direct');
------------------------
.htaccess
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]
RewriteBase /
RewriteRule ^index\.php$ - [L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.php [L]
</IfModule>

----------------
etc/httpd/httpd.conf 수정
Listen 80
<VirtualHost *:8080>
    ServerName localhost
    DocumentRoot "/var/www/html/theenm"
    <Directory "/var/www/html/theenm">
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog logs/site1-error_log
    CustomLog logs/site1-access_log combined
</VirtualHost>

Listen 81
<VirtualHost *:81>
    ServerName wordpress
    DocumentRoot "/var/www/html/wordpress"
    <Directory "/var/www/html/wordpress">
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
    ErrorLog logs/site2-error_log
    CustomLog logs/site2-access_log combined
</VirtualHost>
-=-------------------

서버 설치
sudo yum install php mysql-server
service mysqld start -- 시작해야 mysql 접속 가능
gd 라이브러리 설치
sudo yum install php-gd

mysql db, user 생성
    sudo mysql -uroot



    # mydatabase, myuser, mypassword는 상황에 맞게 수정하세요
    CREATE DATABASE mydatabase;
    CREATE USER 'myuser'@'localhost' IDENTIFIED BY 'mypassword';
    GRANT ALL PRIVILEGES ON mydatabase.* TO 'myuser'@'localhost';

mysql 시작
sudo systemctl start mysqld
자동 시작 설정
sudo systemctl enable mysqld
--보안설정
--sudo mysql_secure_installation

아파치 설치
yum install httpd

아파치 시작
systemctl start httpd

아파치 자동 시작
systemctl enable httpd

아파치 상태 확인
systemctl status httpd

웹 안뜨는 경우 
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-service=https
sudo firewall-cmd --reload

data 디렉토리의 퍼미션을 707로 변경하여 주십시오.
아래 실행 후 진행
# setenforce 0

짧은 주소
etc/httpd   httpd.conf 수정
<Directory "/var/www/html">
아래에 AllowOverride none 를 All로 변경 -> 재시작

모니터링 툴 설치
https://velog.io/@suk13574/Promehteus-prometheus-%EC%82%AC%EC%9A%A9%ED%95%B4%EB%B3%B4%EA%B8%B0-%EC%84%A4%EC%B9%98-%EA%B5%AC%EC%84%B1-%EC%8B%A4%ED%96%89

https://tikus.tistory.com/5
wget 설치 필요
yum install wget

--   prometheus 설정

cmd> vi conf/prometheus.yml
---
global:
  scrape_interval: 15s
  evaluation_interval: 15s

alerting:
  alertmanagers:
    - static_configs:
        - targets:

scrape_configs:
  - job_name: "prometheus"
    static_configs:
      - targets: ["192.168.56.112:9090"]

cmd> vi startPrometheus.sh
./bin/prometheus \
  --config.file=/monitoring/prometheus/prometheus-2.41.0.linux-amd64/conf/prometheus.yml \
  --storage.tsdb.path=/monitoring/prometheus/prometheus-2.41.0.linux-amd64/data &

cmd> vi stopPrometheus.sh
ps -ef | grep prometheus | grep 2.41.0 | awk {'print "kill -9 " $2'} | sh -x

cmd> chmod 750 *.sh

-- 실행
cmd> ./startPrometheus.sh

-- 데몬 등록
cmd> sudo vi /etc/systemd/system/prometheus.service
[Unit]
Description=Prometheus Server
Documentation=https://prometheus.io/docs/introduction/overview/
After=network-online.target

[Service]
User=grafana
Restart=on-failure
ExecStart=/monitoring/prometheus/prometheus-2.41.0.linux-amd64/bin/prometheus \
  --config.file=/monitoring/prometheus/prometheus-2.41.0.linux-amd64/conf/prometheus.yml \
  --storage.tsdb.path=/monitoring/prometheus/prometheus-2.41.0.linux-amd64/data

[Install]
WantedBy=multi-user.target

cmd> sudo systemctl daemon-reload
cmd> sudo systemctl enable prometheus --now

cmd> ./stopPrometheus.sh
cmd> sudo systemctl restart prometheus

cmd> curl -X GET http://192.168.56.112:9090
<a href="/graph">Found</a>.

grafana 설치
sudo yum install -y https://dl.grafana.com/enterprise/release/grafana-enterprise-12.0.2-1.x86_64.rpm

grafana 데몬 등록
cmd> sudo vi /etc/systemd/system/grafana.service
[Unit]
Description=Grafana Server
Documentation= https://grafana.com/docs/grafana/latest/
Wants=network-online.target
After=network-online.target

[Service]
User=grafana
Group=grafana
Type=simple
Restart=on-failure
WorkingDirectory=/monitoring/grafana/grafana-9.3.2
ExecStart=/monitoring/grafana/grafana-9.3.2/bin/grafana-server

[Install]
WantedBy=multi-user.target

cmd> sudo systemctl daemon-reload
cmd> sudo systemctl enable grafana --now

cmd> ./stopGrafana.sh
cmd> sudo systemctl restart grafana

cmd> curl -X GET http://192.168.56.111:3000
INFO [01-25|16:25:48] Request Completed
                        logger=context userId=0 orgId=0 uname= method=GET path=/ status=302 remote_addr=192.168.56.111 time_ms=0 duration=266.603µs size=29 referer= handler=/
<a href="/login">Found</a>.



-- 워드 프로세스 설치
https://comnrose.tistory.com/entry/%EB%A6%AC%EB%88%85%EC%8A%A4-%EC%84%9C%EB%B2%84%EC%97%90-%EC%9B%8C%EB%93%9C%ED%94%84%EB%A0%88%EC%8A%A4wordpress-%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0-1%ED%8E%B8


wordpress
theenm / as1234

테마 추가하기 시 오류 발생
Warning: wp_update_themes(): 예상하지 않은 오류가 발생했습니다.

ssh 연결 정보 확인
curl https://api.wordpress.org/

해결
sudo setenforce 0


wp-content/plugins 폴더 및 하위 파일들의 권한을 확인
폴더: 일반적으로 755
파일: 일반적으로 644
----------------------------------------------------------------







https://velog.io/@jhkim31/%ED%85%8C%EC%8A%A4%ED%8A%B8-%EC%9D%B8%ED%94%84%EB%9D%BC-%EA%B5%AC%EC%B6%95-1.-docker-swarm-%EC%84%B8%ED%8C%85

sudo apt update
sudo apt install build-essential dkms linux-headers-$(uname -r)
cd /media/$USER/VBox_GAs_*/  # 또는 /run/media/USERNAME/VBox_GAs_*/
sudo ./VBoxLinuxAdditions.run




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

