# 네번째 - 도전과제

## 목표
시스템을 구축할때 VPC, 서브넷등등을 만드는건 손이 너무 많이 간다.   
클라우드 포메이션을 이용해서 간단히 인프라를 구축하는 방법을 익힌다.


## 결과물 미리보기
TODO

## 주의 사항

*** ***모든 리소스에는 꼭 Name 태그를 붙여주세요*** ***   
(Name태그 없는 리소스는 불시에 지워버립니다.)

* 처음엔 콘솔을 통해 클릭클릭으로 구축을 해보고 다음에 CloudFormation으로 작성해보는걸 추천드립니다.
* 클라우드포메이션으로 만들어진 리소스들은 클라우드포메이션 스택 삭제를 하면 다같이 지워집니다.
* 각각의 스탭마다 제대로 만들었는지 모를수있습니다. 그럴때는 저에게 연락주시면 리뷰해드립니다.

## 세부 내용

### 1. VPC 생성
> 1. 10.0.0.0/16의 CIDR로 VPC를 생성합니다. 
> 2. 생성할때는 꼭 Name태그를 붙여주세요
> 3. 여기까지 CloudFormation을 이용하여 구축해봅니다.   
>  (***CIDR은 파라미터로 콘솔에서 입력받게합니다.***)   
>  (***VPC의 네임태그는 CloudFormation 스택이름을 참조하게 만듭니다.***)
> 4. 제출물 1-1 : 여기까지의 CloudFormation yaml 파일 
> 5. 제출물 1-2 : 여기까지의 CloudFormation json 파일

### 2. Subnet 생성
> 1. Public 서브넷 2개, Private 서브넷 2개를 만듭니다.
> 2. Public 서브넷 CIDR : 10.0.1.0/24, 10.0.2.0/24 
> 3. Private 서브넷 CIDR : 10.0.3.0/24, 10.0.4.0/24 
> 4. 여기까지 CloudFormation을 이용하여 구축해봅니다.   
>  (***CIDR은 파라미터로 콘솔에서 입력받게합니다.***)   
>  (***서브넷의 네임태그는 CloudFormation 스택이름을 참조하게 만듭니다.***)
> 5. 제출물 2-1 : 여기까지의 CloudFormation yaml 파일
> 6. 제출물 2-2 : 여기까지의 CloudFormation json 파일

### 3. 인터넷 게이트웨이
> 1. 인터넷 게이트웨이를 만듭니다.
> 2. 퍼블릭 서브넷용 라우팅 테이블을 만듭니다.
> 3. 라우팅 테이블에 인터넷 게이트웨이와 public 서브넷을 연결합니다.
> 4. 여기까지 CloudFormation을 이용하여 구축해봅니다.    
>  (***IGW의 네임태그는 CloudFormation 스택이름을 참조하게 만듭니다.***)
> 5. 제출물 3-1 : 여기까지의 CloudFormation yaml 파일
> 6. 제출물 3-2 : 여기까지의 CloudFormation json 파일


### 4. NAT 게이트 웨이
> 1. public 서브넷에 NAT 게이트웨이를 만듭니다.
> 2. 프라이빗 서브넷용 라우팅 테이블을 만듭니다.
> 3. 라우팅 테이블에 NAT 게이트웨이와 프라이빗 서브넷을 연결합니다.
> 4. 여기까지 CloudFormation을 이용하여 구축해봅니다.   
>  (***NAT Gateway의 네임태그는 CloudFormation 스택이름을 참조하게 만듭니다.***)
> 5. 제출물 4-1 : 여기까지의 CloudFormation yaml 파일
> 6. 제출물 4-2 : 여기까지의 CloudFormation json 파일

### 5. CloudFormation 파일 output 만들기
> 새 CloudFormation 파일을 만들고 이전에 만든 파일의 리소스를 참조할 것입니다.   
> 그렇기 위해선 '구' 파일에서 output으로 빼주고 '신'파일에서 참조해주어야 합니다.   
> (즉 다른 스택으로 리소스값을 전달하려면 output을 이용해야합니다.)   
>    
> 이 작업을 진행합니다.   
>     
> 아웃풋으로 뽑을 리스트는 아래와 같습니다.(네이밍은 각자 다를테니 참고만하세요)
> * VPC
> * VPCCIDR
> * PublicSubnetA
> * PublicSubnetACIDR
> * PublicSubnetC
> * PublicSubnetCCIDR
> * PrivateSubnetA
> * PrivateSubnetACIDR
> * PrivateSubnetC
> * PrivateSubnetCCIDR
> * PublicRTB
> * PrivateRTB

### 6. 키페어 생성
> 키페어를 생성합니다.    
> 이 작업은 콘솔로만 가능합니다.   
>    
> ec2콘솔 - 키페어에 들어가서   
> RSA유형으로 만듭니다.



### 7. Bastion 서버를 위한 Security Group(보안그룹) 생성
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


### 8. Bastion 서버 생성 
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


### 9. Bastion 서버 접속 확인
> Bastion 서버가 띄워지면 퍼블릭 ip가 할당됩니다. 해당 ip와 1.에서 다운받은 키페어로 Bastion서버에 접속해봅니다.   




## 제출 결과물
> 1. 각각의 CloudFormation 파일

## 발표
> 1. 소감 발표, 30분 준비
> 2. 2명 랜덤으로 추첨해서 발표
