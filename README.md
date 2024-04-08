# cicdtest

1. CloudFoundry 생성
![image](https://github.com/kangseunghyun/cicdtest/assets/21374560/94d0128b-6ec0-4a3a-9825-8deeec7b693a)
- trail 버젼에서는 기본 저장소를 dev로 생성되어 있음.

2. CI/CD
- Services > Service Marketplace > continuous Integration & Delivery 구독
- 구독 완료 후 권한 부여 필요. 
![image](https://github.com/kangseunghyun/cicdtest/assets/21374560/d75d3259-2682-4c29-a268-9f660e9c0b83)
- Security > Users > Role collections > CICD Service Administrator / Developer 추가
- 재로그인?(바로 권한이 적용 안 되는듯) 하면 + 번튼 활성화
![image](https://github.com/kangseunghyun/cicdtest/assets/21374560/c5144478-c352-4f20-a3e6-db90456c9c4f)
> 탭별 설명
>> * Jobs : 빌드 배포를 수행할 job 설정
>> * Repositories : git 등 저장소 설정
>> * Credentials : git, btp등 인증 설정 > Jobs에서 연결해서 사용함. 

2-1. Credentials 설정
![image](https://github.com/kangseunghyun/cicdtest/assets/21374560/514a6fa8-bb2e-4a64-8fb2-58065617c7d3)
* CloudFoundry 인증에 사용 (cf로 생성)
* github 인증에 사용(github로 생성) => pulic git인 경우 불필요
* webhook 인증에 사용(whathook로 생성) => 인증 생성 후 발급되는 key를 github에 설정해야 webhook를 수신받을 수 있음.

2-1-1 webhook 인증
  - github > settings > Webhooks > add webhhok
  - 생성한 api url 등록
  - application/json 선택
  - 이전에 생성한 key 등록

3.  Repositories 등록
- 등록한 github 등록
- webhook evenct receiver에 2-1-1에서 등록한 whathook 선택
  
4. jobs 등록
  
4-1 기본 정보  
![image](https://github.com/kangseunghyun/cicdtest/assets/21374560/a470bb77-fd1a-4d77-9f19-2791b16c7c71)
  - 3에서 등록한 repository 등록
  - Pipeline은 Cloud Foundry environment 선택
  - 제공 Pipeline
    * Cloud Foundry environment
    * container-Based Apllications
    * Kyma Runtime
    * Sap Fiori for ABAP Platform
    * SAP Fiori in the Neo environment
    * SAP Integration Sutie Artifacts 

4-2 Stages

![image](https://github.com/kangseunghyun/cicdtest/assets/21374560/9c400bbd-b0c0-4c85-a03a-da326a9ed370)

- Configuraton Mode : Job Editor 선택
   * Job Editor는 web화면에서 빌드, Deploy 설정
   * Source Repository: 소스내에 .pipeline/config.yml에 설정한 정보로 빌드, Deploy 진행
                        Jobs에서 기존에 등록된 정보를 볼수 있음.
![image](https://github.com/kangseunghyun/cicdtest/assets/21374560/46aefeaf-3cfd-4a7f-9dfb-9351be05796e)
   
- Build
  * Build Tool 은 maven, mta, npm제공
  * Maven Static code Checks, Lint Cheack 추가 소스 유효성 체크 시 설정
  * Additional Command : 전/후 추가 커맨트 필요시 
  * Additional Credentials : 인증을 위한 추가 정보 필요 시 
  * Additional Variables : 추가 파라미터 설정 시
 
- release(Deploy)
  
  ![image](https://github.com/kangseunghyun/cicdtest/assets/21374560/f9bc725c-a3cf-4cb3-9299-867f9351e6ee)

  * Deploy to cloud Foundry Space ON
  * Application Name : source > manifext file에 설정한 이름
  * Api Endpoint : trial 계정 참조
  * Org Name : trial 계정 참조
  * Space : 1에서 생성한 저장소(dev로 설정)
  * Deploy type : standard
  * Credentials : cf 접근을 위한 인증(cf로 설정된 인증 정보 연결)
  * Cloud Transport management : 다른 저장 공간과 연동해서 배포 지원(파악 예정)
     
5. manifest.yml 수정
- 기존 applicaton 설정
- Java를 사용, 버전은 11이상, 메모리는 2G 사용, helpme instance에 배포(없을 시 자동 생성)
> 샘플
<pre>
<code>---
applications:
- name: helpme
  memory: 2G
  buildpack: sap_java_buildpack
  path: target/objectstore-sample-1.1.1.jar
  env:
    JBP_CONFIG_COMPONENTS: "jres: ['com.sap.xs.java.buildpack.jdk.SAPMachineJDK']"
    JBP_CONFIG_SAP_MACHINE_JRE: '{ jre: { version: "11.+" } }'
  services:
    helpme
</code>
</pre>



   
