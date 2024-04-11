SC_STYP (0:최신순, 1:시청순, 2:추천순, 3:90일이내 랜덤 )
192.168.1.14
SC_STYP 값이 3인 경우
    [B_VOD].[dbo].[LHY_WEB_vodCategory_Listrandom]
그 외
    [B_VOD].[dbo].[LHY_cateGrpVodList] 
    

SC_PN - 목록 페이지 넘버
SC_GP - 카테고리 그룹코드(groupCode. 13: 셀럽전용)
SC_IA - 성인 여부(1 : 성인, 0: 비성인)
SC_STYP - 정렬 순서(0:최신순, 1:시청순, 2:추천순, 3:90일이내 랜덤)
SC_SCTE - 검색 카테고리(0: 전체, 1: groupCode 13 일 경우 셀럽 전용: 나머지VOD, 2: groupCode 13 일 경우 셀럽 전용: I’m Celuv, 3: groupCode 13 일 경우 셀럽 전용: Celuv news)
SC_PC - 실행프로그램 파트너사 코드


URL:https://devsys.popkontv.kr:9002/AS/castData/cateGrpVodList.asp
 PARAMS:["SC_PN": "1", "SC_GP": "17", "SC_IA": "0", "SC_STYP": "0", "SC_SCTE": "0", "SC_PC": "P-00001"]
 

USP_GetList_CastOnListTopForWeb_003
우선 순위 방송 갯수 조회	 USP_Get_CastOnCnt
라이브 리스트  USP_GetList_CastOnListForWeb_003


농협 은행 입금금액(입금, 원 text 붙어 있음) / 입금일자 계좌번호 입금자명
{"SNDN":"1588-2100","RCVN":"010-6201-3839","TXT":"[Web발신]\n농협 입금66,000원\n04/07 14:01 352-****-1275-13 송재영","DATE":"20240407020130","TID":1081964859032}

신한 은행 입금시간 / 계좌번호 / 입금 금액(입금 text 붙어 있음) / 입금자명
{"SNDN":"1577-8000","RCVN":"010-3058-3837","TXT":"[Web발신]\n신한04/07 20:12\n100-036-207773\n입금     11,000\n원병철","DATE":"20240407081252","TID":1246712215073}
{"SNDN":"1577-8000","RCVN":"010-2966-3839","TXT":"[Web발신]\n신한04/08 11:11\n140-012-603310\n입금      3,300\n하지훈","DATE":"20240408111147","TID":958134215622}
{"SNDN":"1577-8000","RCVN":"010-3244-3839","TXT":"[Web발신]\n신한04/08 11:06\n140-014-196870\n입금      5,500\n문요한","DATE":"20240408110640","TID":519902972591}
{"SNDN":"1577-8000","RCVN":"010-2529-3839","TXT":"[Web발신]\n신한04/08 11:05\n100-035-229699\n입금    330,000\n김동진","DATE":"20240408110544","TID":953527830088}
{"SNDN":"1577-8000","RCVN":"010-9957-3839","TXT":"[Web발신]\n신한04/08 11:05\n100-033-097099\n입금     33,000\n이금호","DATE":"20240408110527","TID":275474426612}
{"SNDN":"1577-8000","RCVN":"010-3058-3837","TXT":"[Web발신]\n신한04/08 11:05\n100-036-207773\n입금    330,000\n최동욱","DATE":"20240408110507","TID":279860721862}
{"SNDN":"1577-8000","RCVN":"010-3058-3837","TXT":"[Web발신]\n신한04/08 08:19\n100-036-207773\n입금    110,000\n진대현","DATE":"20240408081932","TID":2491669195532}
{"SNDN":"1577-8000","RCVN":"010-2966-3839","TXT":"[Web발신]\n신한04/08 04:32\n140-012-603310\n입금     55,000\n윤승호","DATE":"20240408043246","TID":3636335239975}

kb 은행 입금시간 / 계좌번호(?) / 입금자명 / 입금형식(전자금융입금, FBS입금) / 금액
{"SNDN":"1644-9999","RCVN":"010-2529-3839","TXT":"[Web발신]\n[KB]04/06 16:15\n606401**772\n방선옥\n전자금융입금\n55,000","DATE":"20240406041506","TID":924689516532}
{"SNDN":"1644-9999","RCVN":"010-2529-3839","TXT":"[Web발신]\n[KB]04/05 11:12\n606401**772\n방선옥\n전자금융입금\n33,000","DATE":"20240405111245","TID":643418295003}
{"SNDN":"1644-9999","RCVN":"010-2529-3839","TXT":"[Web발신]\n[KB]04/05 10:25\n606401**772\n김우열\nFBS입금\n11,000","DATE":"20240405102504","TID":572762246822}
{"SNDN":"1644-9999","RCVN":"010-2529-3839","TXT":"[Web발신]\n[KB]04/04 01:14\n606401**772\n방선옥\n전자금융입금\n110,000","DATE":"20240404011457","TID":2981417301522}
{"SNDN":"1644-9999","RCVN":"010-2529-3839","TXT":"[Web발신]\n[KB]04/03 17:29\n606401**772\n김성옥\n전자금융입금\n3,300","DATE":"20240403052927","TID":1398716984731}


https://github.com/seunghuibaek/02.redburn

/AS/castData/naViewCastList.asp
Select Case partnerCode 
	' [방송공유 주] - 킹콩티비 [방송공유 이하] 강냉이티비 킹티비 96티비 99티비 포도티비 3040티비 77티비 여기티비' 인스타티비
	case "P-00041", "P-00002", "P-00060", "P-00067", "P-00069", "P-00070", "P-00072", "P-00073", "P-00075", "P-00008"
		cmdTxt = "EXEC [B_CASTDATA].[dbo].[USP_GetList_CastOnListSrchForAPI_Kingkong_004] "
	case else
		cmdTxt = "EXEC [B_CASTDATA].[dbo].[USP_GetList_CastOnListSrchForAPI_004] "
	end select

exec USP_GetList_CastOnListSrchForAPI_004 0, '', 0, 0, 0, 'P-00001', 'Y', 'Y'
0:전체목록, 1:방송제목+아이디+닉네임검색
검색어
카테고리 :: [0: 전체, 10:개인, 11:신인, 20:19+, 14:스포츠, 16:게임, 13:음악, 12:영화]  
정렬타입 :: [0: 최신순, 1: 인기순, 2: 시청자순] 
방송노출디바이스 :: [0:방송 목록 전체, 1:모바일, 2:PC]  
파트너코드
로그인_여부 :: [Y: YES N: NO]  
성인_인증_여부 :: [Y: YES N: NO]  

TestMapper.java
import org.apache.ibatis.annotations.Mapper;

@Mapper
public interface TestMapper {
	public String selectTest() throws Exception;
}

service
@Service
public class TestService {
	@Autowired TestMapper testMapper;
	
	public String getTest() throws Exception {
		return testMapper.selectTest();
	}
}


controller
@Slf4j
@SpringBootTest
public class TestController {
	@Autowired TestService service;
	
	@Test
	public void test() throws Exception {
		log.info(service.getTest());
	}
}


import org.jasypt.encryption.StringEncryptor;
import org.jasypt.encryption.pbe.PooledPBEStringEncryptor;
import org.jasypt.encryption.pbe.config.SimpleStringPBEConfig;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class JasyptConfig {

    @Value("${jasypt.encryptor.password}")
    private String PASSWORD_KEY;

    @Bean("jasyptStringEncryptor")
    public StringEncryptor stringEncryptor(){
        PooledPBEStringEncryptor encryptor = new PooledPBEStringEncryptor();
        SimpleStringPBEConfig config = new SimpleStringPBEConfig();
        config.setPassword(PASSWORD_KEY);
        config.setPoolSize("1");
        config.setAlgorithm("PBEWithMD5AndDES");
        config.setStringOutputType("base64");
        config.setKeyObtentionIterations("1000");
        config.setSaltGeneratorClassName("org.jasypt.salt.RandomSaltGenerator");
        encryptor.setConfig(config);
        return encryptor;
    }
}


#mybatis setting
mybatis.mapper-locations=classpath:com/hako/web/mybatis/blog/mapper/*.xml
#mybatis.mapper-locations=classpath:com/hako/web/dao/Blog/mapper/*.xml



#Encoding UTF-8
server.servlet.encoding.charset=UTF-8
server.servlet.encoding.enabled=true
server.servlet.encoding.force=true


#mysql setting(예시)
spring.datasource.driver-class-name= com.mysql.cj.jdbc.Driver
spring.datasource.url= jdbc:mysql://localhost:3306/Main_DB
spring.datasource.username=root
spring.datasource.password=1234

Qortmdgml!@#

API
114.141.29.109
ASP MW
114.141.29.100
114.141.29.101
영상관리서버
114.31.50.115


118.129.153.138


손세웅 <sw.son@theenm.com>
"박남희A/팀장/모바일팀" <nh.park@theenm.com>
"허재원/부장/기술개발부" <jw.huh@theenm.com>
wjdgmdqo2


/home/theenm/.pm2/logs/pushAPI-out-74.log:5776:[2024/03/13 13:39:57] /home/theenm/pushpopkon/routes/push.js:48:8 ==## post : jeonger4303-20240313103648, jeonger4303, P-00001
/home/theenm/.pm2/logs/pushAPI-out-78.log:5587:[2024/03/13 10:37:38] /home/theenm/pushpopkon/routes/push.js:48:8 ==## post : jeonger4303-20240313103648, jeonger4303, P-00001
/home/theenm/.pm2/logs/pushAPI-out-80.log:5641:[2024/03/13 11:36:56] /home/theenm/pushpopkon/routes/push.js:48:8 ==## post : jeonger4303-20240313103648, jeonger4303, P-00001
/home/theenm/.pm2/logs/pushAPI-out-81.log:5767:[2024/03/13 11:23:09] /home/theenm/pushpopkon/routes/push.js:48:8 ==## post : jeonger4303-20240313103648, jeonger4303, P-00001
/home/theenm/.pm2/logs/pushAPI-out-81.log:5769:[2024/03/13 11:35:35] /home/theenm/pushpopkon/routes/push.js:48:8 ==## post : jeonger4303-20240313103648, jeonger4303, P-00001
/home/theenm/.pm2/logs/pushAPI-out-82.log:5601:[2024/03/13 10:54:25] /home/theenm/pushpopkon/routes/push.js:48:8 ==## post : jeonger4303-20240313103648, jeonger4303, P-00001
/home/theenm/.pm2/logs/pushAPI-out-82.log:5605:[2024/03/13 11:21:32] /home/theenm/pushpopkon/routes/push.js:48:8 ==## post : jeonger4303-20240313103648, jeonger4303, P-00001
/home/theenm/.pm2/logs/pushAPI-out-83.log:5652:[2024/03/13 13:45:10] /home/theenm/pushpopkon/routes/push.js:48:8 ==## post : jeonger4303-20240313103648, jeonger4303, P-00001



URL:https://devsys.popkontv.kr:9002/AS/member/pwdCheck.asp
 PARAMS:["SC_SI": "eirurhd", "SC_PC": "P-00001", "SC_SP": "qpwoeiruty1!"]
 
URL:https://devsys.popkontv.kr:9002/AS/member/pwdCheck.asp
 PARAMS:["SC_SI": "eirurhd", "SC_PC": "P-00001", "SC_SP": "qpwoeiruty1!"] 
- Result -
 {"rst":{"rstCode" : "1","rstMsg" : "안전하지 않은 비밀번호입니다."}}


Function get_browser()

 Dim browser_arr(3)
 os = "known"
 browser = "known"
 device = "PC"
 is_mobile = False

 agent = request.ServerVariables("HTTP_USER_AGENT")

 '//browser
 if instr(agent,"Chrome") > 0 then
  browser = "Chrome"
 end if
 if instr(agent,"MSIE") > 0 then
  browser = "IE"
 end if
 if instr(agent,"rv:") > 0 then
  browser = "IE"
 end if
 if instr(agent,"Android") > 0 then
  browser = "android"
 end if
 if instr(agent,"iPhone") > 0 then
  browser = "iphone"
 end if

 '//OS
 if instr(agent,"Windows") > 0 then
  os = "Windows"
 end If
 if instr(agent,"Linux") > 0 then
  os = "Linux"
 end If

 '//device
 if instr(agent,"Android") > 0 then
  device = "android"
 end if


로그 추가 내용..
sys1  api 호출시 -> (필수 : 시간, exepath, 기기, 방송자 id ),,(기타:전달받은 모든 파라메터)
푸시 서버 api 호출시 -> (필수: 시간, exepath, 기기, 방송자 id), (기타 : 넘기는 모든 데이터)


You can use '--warning-mode all' to show the individual deprecation warnings and determine if they come from your own scripts or plugins.

방송회원 B_MEMBER
10.20.23.28
USP_Mod_MmbrLoginProcess_002


https://devsys.popkontv.kr:9002/AS/member/naSignOn.asp
{"SC_EP":7,"SC_PC":"P-00001","SC_SI":"popios5","SC_SK":"9fc3cb9b-e3b7-498c-b020-68a73fd29e27","SC_SP":"a123123"}
data=rZGZuGT4KXtVW6r2Fhv0q3FeYnDA19VguFnL9JnX1RIf0bY6DFnEsDN56lyY6ScqH03lotFxCwEV%0APIbu1STgW3FLosCv33sLCVEk4kfYaYkwm7H5yUqqQMJc5cyOg8KhI3ksbHlxy%2FUTII0edZFI1N10%0Ay38CMxc%2FFMBxhBfxc80%3D%0A&key=781&v=2
LoginResModel(rst=ResultModel(rstCode=1, rstMsg=아이디 또는 비밀번호를 다시 확인하세요., pageNum=0, totalPageNum=0, totalListNum=0), signOn=SignOn(memberSex=0, isAdult=0, nickName=, memberType=0, pFileName=, accountLevel=, pwdCode=, isNewBJ=0, isNameCheck=0, levelUp=0, svcLvl=0), memberBlockCheck=MemberBlockCheck(isBlock=0, isLoginBlock=0, blockRegDate=, blockDate=, blockMemo=))


0x71B12A6C306E3B520569E7F14FD78661DA208F992AE7024DB1D74C3DFA81F623


https://devsys.popkontv.kr:9002/AS/member/naSignOn.asp
{"SC_EP":7,"SC_PC":"P-00001","SC_SI":"popaos3","SC_SK":"a542f1f0-bb3b-4e90-a57b-c3ae282c8e13","SC_SP":"a123123"}
LoginResModel(rst=ResultModel(rstCode=1, rstMsg=아이디 또는 비밀번호를 다시 확인하세요., pageNum=0, totalPageNum=0, totalListNum=0), signOn=SignOn(memberSex=0, isAdult=0, nickName=, memberType=0, pFileName=, accountLevel=, pwdCode=, isNewBJ=0, isNameCheck=0, levelUp=0, svcLvl=0), memberBlockCheck=MemberBlockCheck(isBlock=0, isLoginBlock=0, blockRegDate=, blockDate=, blockMemo=))


3.12. 라이브 방송 추천 : castData/naCastRecommend.asp
3.20. 방송 경고 castData/naCastWatchWarn.asp
3.21. 외침권 사용메가폰 사용 castData/castClamor.asp
4.6. VOD 추천 : recVod/mcVodRecmd.asp
5.9. VOD - 댓글 추천 : castData/cateVodCommentRecommand.asp
6.1. 코인선물/사용 : coin/naCoinUse.asp
6.2. VOD 코인사용 : coin/vodCoinUse.asp
11.4. 아이템 사용 : item/itemUse.asp


- 방송정보 확인 : 192.168.1.28 [B_CASTDATA].[dbo].[SSM_castOnData_codeSearch]
    - 실행자 권한체크 : 192.168.1.28 [B_CASTDATA].[dbo].[JBN_JSON_castWatchOn_Step1_LisenceCheck]
    - 차단자 권한체크 : 192.168.1.28 [B_CASTDATA].[dbo].[JBN_JSON_castWatchOn_Step1_LisenceCheck]
    - 차단회원 닉네임 정보 : 192.168.1.28 [B_MEMBER].[dbo].[JBN_JSON_memberNickName]
 
    - 
위의 asp들이 사용하고 있는 sp를 적어주셈.
예를 들어, castData/naCastRecommend.asp내에 실제로 추천을 플러스시키는 sp



rocket chat
http://172.17.12.15:3000/home

swagger
https://127.0.0.1:8443/swagger-ui/index.html
https://dev-api.popkontv.net/swagger-ui/index.html

java 개발 가이드
http://118.129.153.171:81/

jenkins(DEV)
http://114.141.29.144:15000/login?from=%2Fview%2FNext%2520API%2Fjob%2FNext%2520API%2520-%2520Popkon%2F
enmadmin
enmadmin123!@#


쿠베서버
https://service.whatap.io/account/login
dev@theenm.com
theenm12#

pinpoint
http://118.129.153.171/main/realtime/Next-api_dev@SPRING_BOOT






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

