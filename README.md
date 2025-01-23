fhcadhmenfhmlmikccopnhne.AO-J1Ox1O3U6rPkoailZdTRjsCPUg3aDLsx_-4XmNPfermQtGldd73hKseFRBPnRtOz2Sf4a2RU_Dz8S9OZcKoZBk7vCowN2iA



https://daco2020.tistory.com/786

// 환불리스트
https://developers.google.com/android-publisher/api-ref/rest/v3/purchases.voidedpurchases/list?hl=ko

https://github.com/googleapis/google-api-java-client-services/blob/main/clients/google-api-services-androidpublisher/v3/2.0.0/com/google/api/services/androidpublisher/AndroidPublisherRequest.java


import com.google.api.client.auth.oauth2.Credential;
import com.google.api.client.googleapis.auth.oauth2.GoogleCredential;
import com.google.api.client.googleapis.javanet.GoogleNetHttpTransport;
import com.google.api.client.http.HttpTransport;
import com.google.api.client.json.JsonFactory;
import com.google.api.client.json.gson.GsonFactory;
import com.google.api.services.androidpublisher.AndroidPublisher;
import com.google.api.services.androidpublisher.AndroidPublisherScopes;
import com.google.api.services.androidpublisher.model.VoidedPurchasesListResponse;
import lombok.extern.slf4j.Slf4j;

import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.security.GeneralSecurityException;
import java.util.Collections;

/**
 * 구글 스토어에 유저가 구매 취소한 리스트를 조회하는 API 사용 샘플 소스
 * - Lists the purchases that were canceled, refunded or charged-back
 *
 * @author
 */
@Slf4j
public class GoogleVoidedpurchasesListSample {

    /**
     * API 호출할때의 어플리케이션 명. 자체 정의해서 사용
     */
    public static final String APPLICATION_NAME = "TEST-VoidedpurchasesListSample";

    /**
     * 테스트대상 구글앱의 패키지명
     */
    public static final String PACKAGE_NAME = "입력필요";

    /**
     * 인증을 위한 인증파일
     * - 프로토타이핑 중에 임시로 코드저장소외 외부환경 요소로 파일 저장 후 사용, 보안을 위해서 GIT과 같은 VCS에 올라가면 안되며, 라이브환경에서는 AWS Secrets Manager 등을 활용
     */
    public static final String AUTH_FILE_PATH = "인증용 json파일 경로. 구글 Cloud 콘솔에서 다운로드";

    private static final JsonFactory JSON_FACTORY = GsonFactory.getDefaultInstance();
    private static HttpTransport HTTP_TRANSPORT;

    static {
        try {
            HTTP_TRANSPORT = GoogleNetHttpTransport.newTrustedTransport();
        } catch (GeneralSecurityException e) {
            throw new RuntimeException(e);
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    }

    /**
     * 실행 메소드
     * - 구글 API 정의서: https://developers.google.com/android-publisher/api-ref/rest/v3/purchases.voidedpurchases/list?=en
     *
     * @param args
     * @throws IOException
     */
    public static void main(String[] args) throws IOException {

        final AndroidPublisher apiClient = getApiClient(AUTH_FILE_PATH, APPLICATION_NAME);


        AndroidPublisher.Purchases.Voidedpurchases.List listRequest = apiClient.purchases().voidedpurchases().list(PACKAGE_NAME);

        //추가 조회 필터링 조건들 설정
        listRequest.setMaxResults(2L);
        //listRequest.setToken("넥스트페이징 토큰");
        VoidedPurchasesListResponse voidedpurchasesList = listRequest.execute(); //실행

        //구글 응답 필드들 참고
        // 1) https://developers.google.com/android-publisher/api-ref/rest/v3/purchases.voidedpurchases/list#response-body
        // 2) https://developers.google.com/android-publisher/api-ref/rest/v3/purchases.voidedpurchases#VoidedPurchase
        log.info("voidedpurchasesList : {}", voidedpurchasesList);

        //응답 결과 중 voidedSource와 voidedReason 등을 참고해서 스토어 취소 악용한 유저에 대해서 블럭과 같은 이용제한 기능을 구현하면 됨


    }

    /**
     * 구글 인증 후 API를 바로 사용 가능한 클라이언트 객체를 리턴
     *
     * @param authFilePath
     * @param applicationName
     * @return
     * @throws IOException
     */
    public static AndroidPublisher getApiClient(String authFilePath, String applicationName) throws IOException {

        // Authorization.
        final Credential credential = authorizeWithServiceAccount(authFilePath);

        log.debug("credential : {}", credential);

        // Set up and return API client.
        return new AndroidPublisher.Builder(HTTP_TRANSPORT, JSON_FACTORY, credential).setApplicationName(applicationName).build();
    }

    /**
     * 구글 Android Publisher 인증
     *
     * @param apiAuthFilePath
     * @return
     * @throws IOException
     */
    public static Credential authorizeWithServiceAccount(String apiAuthFilePath)
            throws IOException {

        InputStream inputStream = new FileInputStream(apiAuthFilePath);

        GoogleCredential credential = GoogleCredential.fromStream(inputStream, HTTP_TRANSPORT,
                JSON_FACTORY);
        credential = credential.createScoped(Collections.singleton(AndroidPublisherScopes.ANDROIDPUBLISHER));

        return credential;
    }

}
--------

ipnglibkaajacmhanmfacehp.AO-J1OxSSstLX2y5GjcrWhmNjuygT0pjK1HmSDmGOw1Z8KTDoxBQ9lhdjqz410wyFcLAHzN1rtm3ir2p8e_qP1l4rPBQcfTvyg


try {

    ClassPathResource resource = new ClassPathResource("키파일_위치.json");
    InputStream inputStream = resource.getInputStream();

    GoogleCredentials credentials = GoogleCredentials.fromStream(inputStream)
            .createScoped(AndroidPublisherScopes.ANDROIDPUBLISHER);

    AndroidPublisher publisher = new AndroidPublisher.Builder(
            GoogleNetHttpTransport.newTrustedTransport(),
            GsonFactory.getDefaultInstance(),
            new HttpCredentialsAdapter(credentials)
    ).setApplicationName("앱패키지 이름").build();

    AccessToken accessToken = credentials.refreshAccessToken();

    AndroidPublisher.Purchases.Subscriptions.Get get1 = publisher.purchases().subscriptions().get("패키지명", "구매상품아이디", "구매자 토큰값");
    get1.setAccessToken(accessToken.getTokenValue());
    SubscriptionPurchase subscriptionPurchase =  get1.execute();
    log.info("subscriptionPurchase :: "+subscriptionPurchase);
    /* 구매 확정 */
    if(subscriptionPurchase != null && !"0".equals(subscriptionPurchase.getAcknowledgementState())){
        AndroidPublisher.Purchases.Subscriptions.Acknowledge post = publisher.purchases().subscriptions().acknowledge("com.mobile.android", "구매상품아이디", "구매자 토큰값", new SubscriptionPurchasesAcknowledgeRequest());
        post.setAccessToken(accessToken.getTokenValue());
        post.execute();
    }

} catch (IOException e) {
    log.error(e.toString());
} catch (Exception e) {
    log.error(e.toString());
}


decpbgpikmanlopklkkdnofa.AO-J1OzAE7WwJBHGQBhQI84cGh4CA8SK3CZ9jJHTE8BvzBlgfrokKSqP_vZsBXGhug8g_YXAtNthg9nf5wWixPthIrKuGwPQYQ
"9378d0b1-2a89-4b13-1004-001000000001"


com.doyouing.test

developerPayLoad = c0b1b258-036b-4afe-마켓구분(4자리)-회원번호(12자리)
애플리케이션_마켓_코드 (마이크로소프트_스토어:71001, 앱스토어 (맥오에스):71002, 앱스토어 (IPadOS):71003, 앱스토어 (IOS):71004, 구글플레이 (안드로이드):71005, 원스토어 (안드로이드):71006, 갤럭시스토어 (안드로이드):71007, 애플리케이션_마켓_공통:71008

InputStream inputStream = new ClassPathResource(privateKey).getInputStream();

        GoogleCredentials credentials = GoogleCredentials.fromStream(inputStream).createScoped(
            AndroidPublisherScopes.ANDROIDPUBLISHER);

        return new AndroidPublisher.Builder(
            GoogleNetHttpTransport.newTrustedTransport(),
            GsonFactory.getDefaultInstance(),
            new HttpCredentialsAdapter(credentials)
        ).setApplicationName(DramaConstants.AND_BUNDLEID).build();

 

Get get = publisher.purchases().products().get(
                packageId, productId, pToken
            );
	    
[Purchase. Json: {"orderId":"GPA.3302-0738-0285-11646","packageName":"com.jhoh.celuv.test","productId":"ac_0001","purchaseTime":1737002818057,"purchaseState":0,"purchaseToken":"fbbjhbiiknhcnhnjhdlpkmjh.AO-J1OzVHpQVZ5-7uy6SmmYDgjkl-I5Ilo0nm1ApSd7wIN072ZAZl80uiBKNJ8vwc22AgXxGjIak7fP44WrupButFD4xWoSnng","quantity":1,"acknowledged":false}]


products().get(

Purchase. Json: {"orderId":"GPA.3348-9297-3116-55339","packageName":"com.jhoh.celuv.test","productId":"ac_0001","purchaseTime":1736989662823,"purchaseState":0,"purchaseToken":"cnndfobkopgaacacpmdkbbaa.AO-J1Oyr7rFDINq5Fl1nq39JXp6iyPcH1rl2RblHym_FlBzmdqsUN83E2MV1UljFxRHGE0AGvw5hMPz7WPKgEpC-YC68WhNoyw","quantity":1,"acknowledged":false}]

{"orderId":"GPA.3353-6501-1685-47077","packageName":"com.jhoh.celuv.test","productId":"ac_0001","purchaseTime":1736987261344,"purchaseState":0,"purchaseToken":"nhnieamcfcgijmdoahefjfja.AO-J1Oyoe9aiz_GcB-b6Yg82RNvjlawfJlnA-mpbTN9BKwYvyQEchCN_yVMu5nDXNY5FHKUeEkevwvqzFXiC2yMjwHAIeHDSlg","quantity":1,"acknowledged":false}]


/*구매 확정 호출 aos*/
try {

    ClassPathResource resource = new ClassPathResource("키파일_위치.json");
    InputStream inputStream = resource.getInputStream();

    GoogleCredentials credentials = GoogleCredentials.fromStream(inputStream)
            .createScoped(AndroidPublisherScopes.ANDROIDPUBLISHER);

    AndroidPublisher publisher = new AndroidPublisher.Builder(
            GoogleNetHttpTransport.newTrustedTransport(),
            GsonFactory.getDefaultInstance(),
            new HttpCredentialsAdapter(credentials)
    ).setApplicationName("앱패키지 이름").build();

    AccessToken accessToken = credentials.refreshAccessToken();

    AndroidPublisher.Purchases.Subscriptions.Get get1 = publisher.purchases().subscriptions().get("패키지명", "구매상품아이디", "구매자 토큰값");
    get1.setAccessToken(accessToken.getTokenValue());
    SubscriptionPurchase subscriptionPurchase =  get1.execute();
    log.info("subscriptionPurchase :: "+subscriptionPurchase);
    /* 구매 확정 */
    if(subscriptionPurchase != null && !"0".equals(subscriptionPurchase.getAcknowledgementState())){
        AndroidPublisher.Purchases.Subscriptions.Acknowledge post = publisher.purchases().subscriptions().acknowledge("com.mobile.android", "구매상품아이디", "구매자 토큰값", new SubscriptionPurchasesAcknowledgeRequest());
        post.setAccessToken(accessToken.getTokenValue());
        post.execute();
    }

} catch (IOException e) {
    log.error(e.toString());
} catch (Exception e) {
    log.error(e.toString());
}

[Purchase. Json: {"orderId":"GPA.3365-2109-3509-14619","packageName":"com.jhoh.celuv.test","productId":"ac_0001","purchaseTime":1736905672787,"purchaseState":0,"purchaseToken":"difgmjijkfppejnkhfhdflic.AO-J1OzFwbUh-0lFpF1HkZfB7XhKymDcGYHN6jqfWZ1I83ZMgAXqp9HGyVilkkvsdc9Kkpt_Mlz-7OXGWonqTvsqzcjz8ZJVSQ","quantity":1,"acknowledged":false}]

import org.springframework.web.bind.annotation.*;
import org.springframework.http.ResponseEntity;
import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper;
import java.util.Base64;

@RestController
@RequestMapping("/google/rtdn")
public class RTDNController {

    private final ObjectMapper objectMapper = new ObjectMapper();

    @PostMapping
    public ResponseEntity<String> handleRTDN(@RequestBody String requestBody) {
        try {
            // 요청 본문을 JSON으로 파싱
            JsonNode rootNode = objectMapper.readTree(requestBody);
            JsonNode messageNode = rootNode.path("message");

            if (!messageNode.has("data")) {
                return ResponseEntity.badRequest().body("No data field found under message.");
            }

            // message.data 추출 및 디코딩
            String dataBase64 = messageNode.path("data").asText();
            byte[] decodedBytes = Base64.getDecoder().decode(dataBase64);
            String decodedJson = new String(decodedBytes);

            // 디코딩된 JSON 파싱
            JsonNode decodedNode = objectMapper.readTree(decodedJson);

            // oneTimeProductNotification 데이터 추출
            JsonNode oneTimeProductNode = decodedNode.path("oneTimeProductNotification");
            if (oneTimeProductNode.isMissingNode()) {
                return ResponseEntity.badRequest().body("No oneTimeProductNotification found in the data.");
            }

            String orderId = oneTimeProductNode.path("order_id").asText();
            String productId = oneTimeProductNode.path("product_id").asText();

            // 로그 출력 또는 비즈니스 로직 처리
            String responseMessage = String.format("Order ID: %s, Product ID: %s", orderId, productId);
            return ResponseEntity.ok(responseMessage);

        } catch (Exception e) {
            return ResponseEntity.status(500).body("Error processing RTDN: " + e.getMessage());
        }
    }
}

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-web'
    implementation 'com.fasterxml.jackson.core:jackson-databind'
}

import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;
import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper;

@RestController
public class RtdnController {

    private final ObjectMapper objectMapper = new ObjectMapper();

    @PostMapping("/rtdn")
    public ResponseEntity<String> handleRtdn(@RequestBody String notification) {
        try {
            JsonNode jsonNode = objectMapper.readTree(notification);
            String notificationType = jsonNode.get("notificationType").asText();
            String purchaseToken = jsonNode.get("purchaseToken").asText();
            String productId = jsonNode.get("productId").asText();
            int purchaseState = jsonNode.get("purchaseState").asInt();

            // 상태에 따라 처리
            if (purchaseState == 0) {
                // 구매 완료 처리 로직
                System.out.println("Purchase completed for product: " + productId);
            } else {
                // 다른 상태 처리 로직
            }

        } catch (Exception e) {
            e.printStackTrace();
            return ResponseEntity.badRequest().body("Error processing notification");
        }

        return ResponseEntity.ok("Received");
    }
}


구글 RTDN 설정
https://choi-seunghwan.tistory.com/entry/Google-Play-%EC%9D%B8%EC%95%B1-%EA%B5%AC%EB%8F%85-%EC%83%81%ED%92%88-%EC%8B%A4%EC%8B%9C%EA%B0%84-%EC%83%81%ED%83%9C-%EC%B6%94%EC%A0%81-%EC%8B%9C%EC%8A%A4%ED%85%9C-%EA%B5%AC%EC%B6%95-RTDN-Real-Time-Develop-Notification
	구매처리
	https://developer.android.com/google/play/billing/lifecycle/one-time?hl=ko&_gl=1*d58mxy*_up*MQ..*_ga*MTg2Nzg2MjU2NS4xNzM2ODE5MzE0*_ga_6HH9YJMN9M*MTczNjgxOTMxNC4xLjAuMTczNjgxOTMxNC4wLjAuMTM2MTcyMjI5Mg..

실시간 개발자 알림
https://developer.android.com/google/play/billing/rtdn-reference?hl=ko

가격 정보
https://developers.google.com/android-publisher/api-ref/rest/v3/inappproducts?hl=ko  -- 구글 설명

설정
https://minseok-study.tistory.com/entry/%EB%B0%B1%EC%97%94%EB%93%9C-%EA%B5%AC%EA%B8%80-%EC%9D%B8%EC%95%B1%EA%B2%B0%EC%A0%9C-%EC%98%81%EC%88%98%EC%A6%9D-%EA%B2%80%EC%A6%9D
인앱결제 
https://daco2020.tistory.com/786
서비스 계정 생성
https://developers.google.com/android-publisher/getting_started?hl=ko#service-account

https://minseok-study.tistory.com/entry/%EB%B0%B1%EC%97%94%EB%93%9C-%EA%B5%AC%EA%B8%80-%EC%9D%B8%EC%95%B1%EA%B2%B0%EC%A0%9C-%EC%98%81%EC%88%98%EC%A6%9D-%EA%B2%80%EC%A6%9D
implementation 'com.google.apis:google-api-services-androidpublisher:v3-rev20250102-2.0.0'

google-api-client
google-api-services-androidpublisher
google-auth-library-oauth2-http
google-http-client-jackson2

{"orderId":"GPA.3324-8391-2131-30536","packageName":"com.jhoh.celuv.test","productId":"ac_0002","purchaseTime":1736467535885,"purchaseState":0,"purchaseToken":"iphbmdnajcimglihahmhpjai.AO-J1OzH1il0bU1Z5xNRA76g7nSnIbwO0ACllMbeZlW2EcOHsenAtFWSipCY2hfcf9GPJ6JzDJPKO5WQ4agLorV7lubQzeZcug","quantity":1,"acknowledged":false}]


https://developers.google.com/android-publisher/api-ref/rest/v3/purchases.products?hl=ko


https://console.developers.google.com/apis/api/androidpublisher.googleapis.com/overview?project=592815358292

firebase-adminsdk

https://shinheechul.tistory.com/75
   <!-- https://mvnrepository.com/artifact/com.google.api-client/google-api-client -->
        <dependency>
            <groupId>com.google.api-client</groupId>
            <artifactId>google-api-client</artifactId>
            <version>2.2.0</version>
        </dependency>
        <!-- Google Play Developer API -->
        <dependency>
            <groupId>com.google.apis</groupId>
            <artifactId>google-api-services-androidpublisher</artifactId>
            <version>v3-rev20230313-2.0.0</version>
        </dependency>
        <dependency>
            <groupId>com.google.auth</groupId>
            <artifactId>google-auth-library-oauth2-http</artifactId>
            <version>1.20.0</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/com.google.http-client/google-http-client-jackson2 -->
        <dependency>
            <groupId>com.google.http-client</groupId>
            <artifactId>google-http-client-jackson2</artifactId>
            <version>1.43.1</version>
        </dependency>



 -----------
 /*구매 확정 호출 aos*/
try {

    ClassPathResource resource = new ClassPathResource("키파일_위치.json");
    InputStream inputStream = resource.getInputStream();

    GoogleCredentials credentials = GoogleCredentials.fromStream(inputStream)
            .createScoped(AndroidPublisherScopes.ANDROIDPUBLISHER);

    AndroidPublisher publisher = new AndroidPublisher.Builder(
            GoogleNetHttpTransport.newTrustedTransport(),
            GsonFactory.getDefaultInstance(),
            new HttpCredentialsAdapter(credentials)
    ).setApplicationName("앱패키지 이름").build();

    AccessToken accessToken = credentials.refreshAccessToken();

    AndroidPublisher.Purchases.Subscriptions.Get get1 = publisher.purchases().subscriptions().get("패키지명", "구매상품아이디", "구매자 토큰값");
    get1.setAccessToken(accessToken.getTokenValue());
    SubscriptionPurchase subscriptionPurchase =  get1.execute();
    log.info("subscriptionPurchase :: "+subscriptionPurchase);
    /* 구매 확정 */
    if(subscriptionPurchase != null && !"0".equals(subscriptionPurchase.getAcknowledgementState())){
        AndroidPublisher.Purchases.Subscriptions.Acknowledge post = publisher.purchases().subscriptions().acknowledge("com.mobile.android", "구매상품아이디", "구매자 토큰값", new SubscriptionPurchasesAcknowledgeRequest());
        post.setAccessToken(accessToken.getTokenValue());
        post.execute();
    }

} catch (IOException e) {
    log.error(e.toString());
} catch (Exception e) {
    log.error(e.toString());
}
---------


firebase-adminsdk-uzx25@shotform-d95e8.iam.gserviceaccount.com


dependencies {
    compile 'com.google.api-client:google-api-client:1.21.0'
    compile 'com.google.apis:google-api-services-androidpublisher:v2-rev22-1.21.0'
}

// oathu
String emailAddress = "my-new-service-account@api-project-000000.iam.gserviceaccount.com";

JsonFactory JSON_FACTORY = JacksonFactory.getDefaultInstance();
HttpTransport httpTransport = GoogleNetHttpTransport.newTrustedTransport();
GoogleCredential credential = new GoogleCredential.Builder()
     .setTransport(httpTransport)
     .setJsonFactory(JSON_FACTORY)
     .setServiceAccountId(emailAddress)
     .setServiceAccountPrivateKeyFromP12File(new File("src/GooglePlayAndroidDeveloperPrivateKey.p12"))
     .setServiceAccountScopes(Collections.singleton("https://www.googleapis.com/auth/androidpublisher"))
     .build();

// 주문정보 호출
String packageName = "pe.kr.theeye.trivialdrive";
String productId = "gas";
String purchaseToken = "njnbhmfid...AuSkyASqY";

AndroidPublisher publisher = new AndroidPublisher.Builder(httpTransport, JSON_FACTORY, credential)
	.setApplicationName(packageName)
	.build();

AndroidPublisher.Purchases.Products.Get get = publisher.purchases().products().get(packageName, productId, purchaseToken);
ProductPurchase productPurchase = get.execute();
System.out.println(productPurchase.toPrettyString());

// 인앱 상품의 소비 상태. 0 아직 소비 안됨(Yet to be consumed) / 1 소비됨(Consumed)
Integer consumptionState = productPurchase.getConsumptionState();

// 개발자가 지정한 임의 문자열 정보
String developerPayload = productPurchase.getDeveloperPayload();

// 구매 상태. 0 구매완료 / 1 취소됨
Integer purchaseState = productPurchase.getPurchaseState();

// 상품이 구매된 시각. 타임스탬프 형태
Long purchaseTimeMillis = productPurchase.getPurchaseTimeMillis();

---------------------------------------------------------------------

{
  "consumptionState" : 1,	// 0 아직 컨슘 안됨, 1 컨슘됨
  "developerPayload" : "",
  "kind" : "androidpublisher#productPurchase",
  "purchaseState" : 0,	// 0 구매완료, 1 취소
  "purchaseTimeMillis" : "1454502702978"
}


     
http://theeye.pe.kr/archives/tag/purchasestate


https://velog.io/@givepro91/%EC%9D%B8%EC%95%B1%EA%B2%B0%EC%A0%9C-%EC%84%9C%EB%B2%84-%EA%B0%9C%EB%B0%9C


구매 정보가 유효한지 확인
https://developers.google.com/android-publisher/api-ref/rest/v3/purchases.products/get?hl=ko 

전송되는 정보
{
  "kind": string,
  "purchaseTimeMillis": string,
  "purchaseState": integer,
  "consumptionState": integer,
  "developerPayload": string,
  "orderId": string,
  "purchaseType": integer,
  "acknowledgementState": integer,
  "purchaseToken": string,
  "productId": string,
  "quantity": integer,
  "obfuscatedExternalAccountId": string,
  "obfuscatedExternalProfileId": string,
  "regionCode": string
}

가격정보 호출
HTTP 요청
https://developers.google.com/android-publisher/api-ref/rest/v3/inappproducts/list?hl=ko 

GET https://androidpublisher.googleapis.com/androidpublisher/v3/applications/{packageName}/inappproducts


 아이템 사용
 https://developers.google.com/android-publisher/api-ref/rest/v3/purchases.products/consume?hl=ko 

POST https://androidpublisher.googleapis.com/androidpublisher/v3/applications/{packageName}/purchases/products/{productId}/tokens/{token}:consume

URL은 gRPC 트랜스코딩 구문을 사용합니다.

경로 매개변수
매개변수
packageName	string
인앱 제품이 판매된 애플리케이션의 패키지 이름입니다 (예: 'com.some.thing').
productId	string
인앱 상품 SKU (예: 'com.some.thing.inapp1')입니다.
token	string
인앱 상품을 구매할 때 사용자 기기에 제공된 토큰입니다.
 

자 이제 위 API를 호출을 하고 나면 드디어 사용자는 인앱결제 -> 아이템 획득과 같은 flow를 거칠 수 있게 됩니다!
-------------------

POST https://androidpublisher.googleapis.com/androidpublisher/v3/applications/{packageName}/purchases/products/{productId}/tokens/{token}:consume

URL은 gRPC 트랜스코딩 구문을 사용합니다.

packageName string
인앱 제품이 판매된 애플리케이션의 패키지 이름입니다 (예: 'com.some.thing').
productId   string
인앱 상품 SKU (예: 'com.some.thing.inapp1')입니다.
token   string
인앱 상품을 구매할 때 사용자 기기에 제공된 토큰입니다.




https://developers.google.com/android-publisher/api-ref/rest/v3/purchases.products/consume?hl=ko



{"orderId":"GPA.3328-6916-1689-27322","packageName":"com.jhoh.celuv.test","productId":"ac_0001","purchaseTime":1736388262230,"purchaseState":0,"purchaseToken":"lafdcpnnimjbjpmipfeigcbf.AO-J1Ow2U_YEo4M1vLQ9NmhIaUxseq4iACzHxgcHoVK3t6VP-nORE9XlL6WyrMEpkNLoOL4Ke4mdfEfBp3Rp7qNEIlQYhIwnXw","quantity":1,"acknowledged":false}]


https://adapty.io/ko/blog/android-in-app-purchases-part-5-server-side-purchase-validation/
https://developer.android.com/google/play/billing/rtdn-reference?hl=ko


{
  "svcPrvdSeCd": 60002,		-- 애플리케이션(APP)
  "osSeCd": 70005,			-- 안드로이드(Andrd)
  "appMrktCd": 71005			-- 구글플레이(Gglply)
}

{
  "statusCd": "S0200",
  "statusMsg": "SUCCESS",
  "data": [
    {
      "saleGudsRgstCd": "RGS1000000001",
      "appMrktRgstGudsCd": null,
      "saleGudsNm": "500토큰",
      "saleQty": 500,
      "salePrc": 6900,
      "bnsQty": 380
    },
    {
      "saleGudsRgstCd": "RGS1000000002",
      "appMrktRgstGudsCd": null,
      "saleGudsNm": "1000토큰",
      "saleQty": 1000,
      "salePrc": 13900,
      "bnsQty": 900
    },
    {
      "saleGudsRgstCd": "RGS1000000003",
      "appMrktRgstGudsCd": null,
      "saleGudsNm": "2000토큰",
      "saleQty": 2000,
      "salePrc": 27900,
      "bnsQty": 2200
    },
    {
      "saleGudsRgstCd": "RGS1000000004",
      "appMrktRgstGudsCd": null,
      "saleGudsNm": "5000토큰",
      "saleQty": 5000,
      "salePrc": 68900,
      "bnsQty": 7500
    }
  ]
}

shrtfrmpltfapisvc  /  W8tKmhf3ey@qHX?6

1. 로그인 체크

2. 결제 상품 목록 정보(가격, 상품명 등)

3. 앱에서 결제 서버에 결제 정보 전송

4. 서버에서 앱으로 실제 결제 건이 맞는지 정보 전송

5. 앱은 맞는지 확인 후 영수증 전송
- api에서 결제 상품에 대한 정보 확인이 필요한지

6. 서버는 영수증 정보를 통해 유효성 검증
- 앱에서 
   회원 아이디, uuid(앱스토어) 전송 가능한지?

7.서버의 검증이 완료되었다면 유저의 구매정보를 저장하고 
  해당 상품을 유저에게 지급
- 정상 구매가 완료 되었다면 api에 
    1) 구매일시(결제 완료시 서버에서 제공되는 정보)
    2) 트랜잭션 아이디(거래번호)
    3) 로그인 아이디 
                        4) 결제 수단 
                        5) 결제 가격 원화(서버에서 제공시)
    6) 결제 통화 코드(서버에서 제공시)
                        7) 결제 가격 현지 통화
    8) 구매 상태
    9) 소비여부
정보 전송 필요

<insert id="insert2" parameterType="com.test.sample.vo.SamplePVO">
    <selectKey keyProperty="sampleSeq" resultType="java.lang.String" order="BEFORE">
        SELECT NEXTVAL(sq_sample_seq) FROM DUAL
    </selectKey>
    INSERT INTO TBL_SAMPLE
    (
        SAMPLE_SEQ,
        SAMPLE_ID
    )
    VALUES
    (
           #{sampleSeq}
         , #{sampleId}
    )
</insert>
https://developer-heo.tistory.com/37
a1234567/*

https://velog.io/@hsh111366/Error%EB%A5%BC-%EB%AA%A8%EC%95%84%EB%B3%B4%EC%9E%90-Process-finished-with-exit-code-1-%ED%95%B4%EA%B2%B0%EB%B2%95


172.17.12.6

192.168.1.16,9190
[B_CASTDATA].[dbo].[USP_GetList_BkmkBrdcListForAPI_003]



7doremifasolra7   

AS/recVod/suspendRecordIFile.asp


59, 282, 486,1415


  
기존url
https://pic.popkontv.com/images/common/coin/

개발기url
https://pic.popkontv.com/images/common/coin/dev


https://bts.rink.kr/issues/12715


USP_Get_MmbrLoginPrtsCd_002
10.20.23.220



https://stagesys.popkontv.com:9002/AS/member/naSignOnCast.asp
2024-10-24 09:36:15.749  8443-8505  RetrofitUtil            com.social.media.broadcast.aospop.e  D  Retrofit Test createRequestBody jsonString {"SC_EP":7,"SC_PC":"P-00001","SC_SI":"popaos101","SC_SK":"cfd073dd-bbe0-4894-a427-d30f22276604","SC_SP":"a123123"}
2024-10-24 09:36:15.811  8443-8505  UserReposi...asterLogin com.social.media.broadcast.aospop.e  D  Retrofit Test responseEmit callbackId: LOGIN_CAST / decodeString : {"rst":{"rstCode" : "1","rstMsg" : "아이디 또는 비밀번호를 다시 확인하세요."},"signOn" : {"memberSex" : "","isAdult" : "","nickName" : "","memberType" : "","pFileName" : "","accountLevel" : "","pwdCode" : "a123123","partnerCode" : "P-00001","isNewBJ" : "0","isNameCheck" : "0","levelUp" : "0","svcLvl" : ""},"memberBlockCheck" : {"isBlock" : "0","isLoginBlock" : "0","blockRegDate" : "","blockDate" : "","blockMemo" : ""}}

USP_Mod_MmbrLoginProcess_002

<%
    Dim objError, data
    Set objError = Server.GetLastError()
%>

<%
    '에러로그 등록
    data = "IIS Error Number : " & objError.ASPCode & chr(13) &_
            "COM Error Number : " & objError.Number & " (0x" & Hex(objError.Number) & ")"& chr(13) &_
            "Error Source : " & objError.Source& chr(13) &_
            "File Name : " & objError.File& chr(13) &_
            "Line Number : " & objError.Line& chr(13) &_
            "Brief Description : " & objError.Description& chr(13) &_
            "Full Description : " & objError.ASPDescription& chr(13) &_
            "Query String : " & Request.Servervariables("query_string")& chr(13) &_
            "Post String : " & Request.Form& chr(13)
    call setApiLoginsert("Error500", data, objError.File, objError.Description)    
    
    Set objError=Nothing
%>
USP_GetList_CastOnListSrchForAPI_005

https://stagesys.popkontv.com:9002/AS/castData/naCastManager.asp

{"SC_DT":0,"SC_IIU":0,"SC_MPC":"","SC_MSI":"gdhchchcyf","SC_PC":"P-00001","SC_PCC":"popaos6-20241021133725","SC_SI":"popaos6","SC_SP":"0x0E55B5D88FFD6DCDFE52A542F252D6F477037F2106401C08B1B3A7B7CB5AF616"}
{"rst":{"rstCode" : "1","rstMsg" : "대상회원은 매니저 등록/해제를 할 수 없습니다.[MSS]"}}

{"SC_DT":0,"SC_IIU":0,"SC_MPC":"","SC_MSI":"ㅗ렿초초펴","SC_PC":"P-00001","SC_PCC":"popaos6-20241021133725","SC_SI":"popaos6","SC_SP":"0x0E55B5D88FFD6DCDFE52A542F252D6F477037F2106401C08B1B3A7B7CB5AF616"}
{"rst":{"rstCode" : "1","rstMsg" : "대상회원 아이디가 존재하지 않습니다."}}

매니저 지정하는 api인데 지정할 아이디를 영어로 보낼때("SC_MSI":"gdhchchcyf") 한글로 보낼때 (""SC_MSI":"ㅗ렿초초펴") rstMsg가 서로 다른데 확인 가능할까요?


{"SC_CT":"0","SC_SCT":"","SC_SCTE":"30","SC_PN":"1","SC_STYP":"2","SC_IA":"0","SC_EP":"9","SC_PC":"P-00117","SC_CLT":"0","SC_IAS":"1"}

{"SC_CT":"0","SC_SCT":"","SC_SCTE":"14","SC_PN":"1","SC_STYP":"2","SC_IA":"0","SC_EP":"9","SC_PC":"P-00117","SC_CLT":"0","SC_IAS":"1"}

castData/naViewCastList.asp

매니저 지정하는 api인데 지정할 아이디를 영어로 보낼때("SC_MSI":"gdhchchcyf") 한글로 보낼때 (""SC_MSI":"ㅗ렿초초펴") rstMsg가 서로 다른데 확인 가능할까요?


ppknapisvcacc:  KTW)tHC\j9#gDzx8
ppknwebsvcacc:    Vq6z7M?5n3(YHdZx
smsuser:	gy3vjaU/p&huV)Zd
smsuser 기존 비밀번호 hzaJrC2(5S$pT=B

https://devsys.popkontv.kr:9002/AS/castData/naViewCastList.asp
{"SC_CLT":1,"SC_CT":1,"SC_EP":7,"SC_IA":0,"SC_IAS":1,"SC_PC":"P-00117","SC_PN":1,"SC_PS":"","SC_SCT":"celaos","SC_SCTE":0,"SC_STYP":2}



select P.spid, P.login_time, P.last_batch, C.client_net_address
from sys.sysprocesses AS P INNER JOIN sys.dm_exec_connections AS C
ON P.spid = C.session_id


select P.spid, P.login_time, P.last_batch
from sys.sysprocesses AS P


"C:\Program Files (x86)\PopPlayer\P-00001\PopPlayerLauncher.exe" PopPlayer:site=stagew.popkontv.com&language=popkon_kr&pcode=P-00001

--2페이지
EXEC @ret2 = B_CASTDATA.dbo.USP_GetList_BrdcListMainExpsr_002 'P-00001',15,2,2,'Y','Y',1,15,0

--3페이지
EXEC @ret3 = B_CASTDATA.dbo.USP_GetList_BrdcListMainExpsr_002 'P-00001',15,2,2,'Y','Y',2,30,15



[B_CASTDATA].[dbo].[USP_GetList_BrdcListMainExpsr_002] 'P-00001', 15, 0, 0, 'Y', 'Y', 2, 15, 0


118.129.153.138
114.141.29.110
114.31.50.114
114.31.50.115
180.182.60.206


URL:https://stagesys.popkontv.com:9002/AS/castData/naViewCastList.asp
 PARAMS:["SC_IA": "1", "SC_PC": "P-00001", "SC_EP": "3", "SC_IAS": "0", "SC_CT": "0", "SC_SCTE": "0", "SC_PN": "1", "SC_STYP": "2", "SC_CLT": "1"]
 

https://bts.rink.kr/issues/12516


92.168.1.80,9190

ppknwebsvcacc

https://thumb.popcast.co.kr/POPCAST_THUMB/sys_Thumb/P-00117/14/9.jpg


SELECT
    S.SPID AS '세션 ID', S.LOGINAME AS '로그인 이름', S.LOGIN_TIME AS '로그인 시간', S.LAST_BATCH AS '마지막 일괄 처리 시간', C.CLIENT_NET_ADDRESS AS '클라이언트 IP 주소'
FROM
    sys.sysprocesses S, sys.dm_exec_connections C
WHERE
    S.spid = C.SESSION_ID
ORDER BY
    S.LOGIN_TIME DESC;

    
192.168.1.91    B_VOD
[B_VOD].[dbo].[KJM_WEB_vodCategory]


string source = "Provider=SQLOLEDB;Data Source=localhost;Initial Catalog=TEST;" +             "UID=sa;PWD=pass1234;" +            "OLE DB Services = -1;";
ppknapisvcacc


OLEDB_CAST              192.168.1.93   B_COMPAY
OLEDB_CAST8             192.168.1.92   B_AD
OLEDB_CTICAST6          192.168.1.91    B_VOD


SQLOLEDB (SQL Server native provider) : HKEY_CLASSES_ROOT\CLSID\{0C7FF16C-38E3-11d0-97AB-00C04FC2AD98} Microsoft.Jet.OLEDB.4.0 (Jet native provider) ": HKEY_CLASSES_ROOT\CLSID\{dee35070-506b-11cf-b1aa-00aa00b8de95} MSDAORA (Oracle native provider) : HKEY_CLASSES_ROOT\CLSID\{e8cc4cbe-fdff-11d0-b865-00a0c9081c1d} MSDASQL (OLE DB Provider for ODBC) : HKEY_CLASSES_ROOT\CLSID\{c8b522cb-5cf3-11ce-ade5-00aa0044773d} Wait Retry 의 경우 이 대기 시간의 전역 설정이라고 볼 수 있습니다. 아래의 값을 조정하게 되면 전체적으로 대기 하는 시간을 늘려 줄 수 있습니다.HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DataAccess\Session Pooling\Retry WaitHKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DataAccess\Session Pooling\ExpBackOff



https://learn.microsoft.com/en-us/previous-versions/ms810829(v=msdn.10)?redirectedfrom=MSDN#bkmk_ODBCConnectionPool


SELECT 
		DB_NAME(dbid) as DBName, 
		COUNT(dbid) as NumberOfConnections,
		loginame as LoginName
	FROM
		sys.sysprocesses
	WHERE 
		dbid > 0
	GROUP BY 
		dbid, loginame
	ORDER BY  COUNT(dbid) DESC
 
114.31.51.70
114.31.51.71
114.31.51.72
114.141.29.103

"SC_SP": "", "SC_RPAT": "16", "SC_SI": "popaos5", "SC_ISH": "1", "SC_PC": "P-00001", "SC_WCP": "36"


WIN-14QLC79S1T9		114.141.29.123
WIN-7DB8CE9BL51		114.141.28.18
WIN-T3EF6KQ1KUQ         114.141.28.19
WIN-UEMICJS5EIC		114.141.29.124



https://docs.google.com/document/d/1D5NOYQqjKlphWvWSAC4IoDD7bv_pHM9xuAJLRSPPOaU/edit

https://bts.rink.kr/projects/potv-cetv/files

API Test URL : https://sys1.celuvtv.co.kr:9002/AS/member/registExe.asp / jsonString : {"SC_ANK":"","SC_PC":"P-00117","SC_AID":"190353027","SC_SI":"","SC_AEM":"kulman10@naver.com","SC_ISA":1,"SC_EM":"theenm_officr@naver.com","SC_EP":7,"SC_SCD":3,"SC_PN":"01024158202","SC_NK":"kulman","SC_SP":""} / result : {"rst":{"rstCode" : "0","rstMsg" : "회원가입이 정상적으로 처리되었습니다.","signId" : "n9573165627300240724","signPwd" : ""}}



member/snsJoinChk.asp
{"SC_PC":"P-00117","SC_SC":3,"SC_SK":"190353027"}
{"rst":{"rstCode" : "0","rstMsg" : "로그인 처리 가능","signId" : "n6737175242320210427","signPwd" : "0xA524669C7B6605132A0C5122BD33BF4C367A68908AD7891537C3F916BCACA75B","isNickChgNeed" : "0"}}


member/naSignOn.asp
{"SC_EP":7,"SC_PC":"P-00117","SC_SI":"n6737175242320210427","SC_SK":"a59418f9-2cce-4b43-8bcd-fa6ed7185fdc","SC_SP":"0xA524669C7B6605132A0C5122BD33BF4C367A68908AD7891537C3F916BCACA75B"}
{"rst":{"rstCode" : "1","rstMsg" : "아이디 또는 비밀번호를 다시 확인하세요."},"signOn" : {"memberSex" : "","isAdult" : "","nickName" : "","memberType" : "","pFileName" : "","accountLevel" : "","pwdCode" : "0xA524669C7B6605132A0C5122BD33BF4C367A68908AD7891537C3F916BCACA75B","isNameCheck" : "0","levelUp" : "0","svcLvl" : ""},"memberBlockCheck" : {"isBlock" : "0","isLoginBlock" : "0","blockRegDate" : "","blockDate" : "","blockMemo" : ""}}




"C:\Program Files (x86)\PopPlayer\P-00001\PopPlayerLauncher.exe" PopPlayer:site=devw.popkontv.com&language=popkon_kr&pcode=P-00001


신규 배포된 SP =  방송목록 조회
[B_CASTDATA].[dbo].[USP_GetList_CastOnListSrchForAPI_004] = 검색용도

[B_CASTDATA].[dbo].[USP_GetList_CastOnListSrchForAPI_004]

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

