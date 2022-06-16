# 3주차 도전과제

## 목표
* 정적 웹 페이지 개발/배포를 해보자   
(SAA시험에 지겹게 나오는 내용중 하나인, 정적페이지 = S3 + CloudFront)

## 결과물 미리보기
https://www.sghaha.com   
https://exam.sghaha.com



## 세부 내용

### 1. 도메인구매
> 1. aws route53콘솔에 들어가서 도메인구매 (가장싼 .click으로 구매, 3달러)

### 2. 정적페이지 개발
> 1. s3 버킷생성 ( * **주의** : S3의 버킷 명을 내가 산 도메인 명으로 만든다.  ex: sghaha.click)
> 2. www.html5up.net 으로 들어가 맘에드는 샘플 사이트 다운로드   
> 3. 본인의 로컬환경에서 다운로드 받은 샘플 내용 수정   
> 4. s3에 업로드   
> 5. s3 객체 url로 배포된 사이트 확인 (ex. https://s3.ap-northeast-2.amazonaws.com/sghaha.com/index.html)    
>   (1번 결과물)

### 3. SSL 인증서 발급
> 1. AWS Certificate Manager 에서 SSL 인증서 발급 (* **주의** : 무조건 버지니아 북부 리전에서 해야함)

### 4. CloudFront 배포
> 1. 나의 S3의 index.html을 바라보는 CloudFront를 배포한다. (* **주의** : 무조건 버지니아 북부 리전에서 해야함)
> 2. 해당 배포에 나의 도메인과 인증서를 참조한다.
   
### 5. Route 53에서 레코드 생성
> 1. www.{도메인}.click 에 대해 CloudFront배포를 바라보도록 정책배포
>    (2번 결과물)
> 2. sample.{도메인}.click 에 대해 CloudFront배포를 바라보도록 정책배포
>    (3번 결과물)

## 제출 결과물
> 1. index.html의 s3 객체 url
> 2. www.{도메인}.click url
> 3. sample.{도메인}.click url

## 발표
> 1. 소감 발표, 30분 준비
> 2. 2명 랜덤으로 추첨해서 발표
