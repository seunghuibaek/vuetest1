"statusMsg": "Cache 'getBrdcrsvclvlCache' does not allow 'null' values. Avoid storing null via '@Cacheable(unless=\"#result == null\")' or configure RedisCache to allow 'null' via RedisCacheConfiguration.",



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

