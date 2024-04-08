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

- 탭별 설명
# Jobs : 빌드 배포를 수행할 job 설정
# Repositories : git 등 저장소 설정
# Credentials : git, btp등 인증 설정 > Jobs에서 연결해서 사용함. 

2-1. Credentials 설정
![image](https://github.com/kangseunghyun/cicdtest/assets/21374560/514a6fa8-bb2e-4a64-8fb2-58065617c7d3)
# CloudFoundry 인증에 사용 (cf로 생성)
# github 인증에 사용(github로 생성) => pulic git인 경우 불필요
# webhook 인증에 사용(whathook로 생성) => 인증 생성 후 발급되는 key를 github에 설정해야 webhook를 수신받을 수 있음. 

2. manifest.yml 수정
  
3. 


   
