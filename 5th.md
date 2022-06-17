# 다섯번째 - 도전과제

## 목표
TODO

## 결과물 미리보기
TODO

## 주의 사항

*** ***모든 리소스에는 꼭 Name 태그를 붙여주세요*** ***   
(Name태그 없는 리소스는 불시에 지워버립니다.)

* 처음엔 콘솔을 통해 클릭클릭으로 구축을 해보고 다음에 CloudFormation으로 작성해보는걸 추천드립니다.
* 클라우드포메이션으로 만들어진 리소스들은 클라우드포메이션 스택 삭제를 하면 다같이 지워집니다.
* 각각의 스탭마다 제대로 만들었는지 모를수있습니다. 그럴때는 저에게 연락주시면 리뷰해드립니다.

## 세부 내용
*  [네번째 - 도전 과제3](https://github.com/sghaha/t2/blob/main/4th.md) 과 이어지는 내용입니다.

### 1. 키페어 생성
> 키페어를 생성합니다.    
> 이 작업은 콘솔로만 가능합니다.   
>    
> ec2콘솔 - 키페어에 들어가서   
> RSA유형으로 만듭니다.

### 2. Bastion 서버를 위한 Security Group(보안그룹) 생성
> * 아래와 같은 Bastion SG를 "기존에 만든" VPC에 생성합니다.   
>    
> 유형 : SSH   
> 프로토콜 : TCP   
> 포트 : 22   
> from : 0.0.0.0/0 (AnyWhere)  ::: 내 아이피만 열어줘도 된다.
>   
> 여기까지 CloudFormation을 이용하여 구축해봅니다.   
>   
> 제출물 1-1 : 여기까지의 CloudFormation yaml 파일   
> 제출물 1-2 : 여기까지의 CloudFormation json 파일


### 3. Bastion 서버 생성 
> 1. Amazon Linux 2 로 인스턴스를 생성합니다.
> 2. Auto-assign public IP(퍼블릭 IP 자동 할당) 활성화
> 3. 보안그룹은 2.에서 만들어준 보안그룹
> 4. 키페어도 1.에서 만들어준것으로
> 5. VPC는 기존에 만든것으로
> 6. 서브넷은 PublicSubnet   
> 7. 여기까지 CloudFormation을 이용하여 구축해봅니다.   
>    (***키페어 이름은 스택생성할때 콘솔로 입력 받게 구성합니다.***)   
>    
> 제출물 1-1 : 여기까지의 CloudFormation yaml 파일.  
> 제출물 1-2 : 여기까지의 CloudFormation json 파일


### 4. Bastion 서버 접속 확인
> Bastion 서버가 띄워지면 퍼블릭 ip가 할당됩니다. 해당 ip 와

## 제출 결과물
> 1. 각각의 CloudFormation 파일

## 발표
> 1. 소감 발표, 30분 준비
> 2. 2명 랜덤으로 추첨해서 발표
