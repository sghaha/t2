# cloudformation 체험해보기

공부중!

### 1. VPC 만들기

* CIDR을  10.0.0.0/16으로하고
* VPC 네임 태그 걸어준 것 밖에없다.  

```
{
    "Resources": {
        "VPC": {
            "Type": "AWS::EC2::VPC",
            "Properties": {
                "CidrBlock" : "10.0.0.0/16",
                "Tags" : [
                    {
                        "Key" : "Name",
                        "Value" : "sghahaVPC"
                    },
                ],
            }
        }
    }
}

```

* 위에꺼는 VPC 네임태그를 sghahaVPC로 이름을 박아줬는데 아래처럼 하면 CloudFormation 스택 생성할때 그 이름을 따라간다

```
{
    "Resources": {
        "VPC": {
            "Type": "AWS::EC2::VPC",
            "Properties": {
                "CidrBlock" : "10.0.0.0/16",
                "Tags" : [
                    {
                        "Key" : "Name",
                        "Value" : {
                            "Fn::Sub": "${AWS::StackName}/VPC"
                        }
                    },
                ],
            }
        }
    }
}
```

* 버전이랑 설명을 적어줬다.
```
{
    "AWSTemplateFormatVersion": "2010-09-09",
    "Description": "sghaha's cloudformation study",
    "Resources": {
        "VPC": {
            "Type": "AWS::EC2::VPC",
            "Properties": {
                "CidrBlock" : "10.0.0.0/16",
                "Tags" : [
                    {
                        "Key" : "Name",
                        "Value" : {
                            "Fn::Sub": "${AWS::StackName}/VPC"
                        }
                    },
                ],
            }
        }
    }
}
```

### 2. 서브넷 만들기

* 왠지 이렇게 따로 돌리면 마지막 쪽에 VPC가 없다고 안될것같긴한데 일단 해보자
```
{
  "AWSTemplateFormatVersion": "2010-09-09",
  "Description": "sghaha's subnet",
  "Resources": {
    "SubnetPrivateAPNORTHEAST2B": {
      "Type": "AWS::EC2::Subnet",
      "Properties": {
        "AvailabilityZone": "ap-northeast-2b",
        "CidrBlock": "10.0.1.0/24",
        "Tags": [
          {
            "Key": "Name",
            "Value": {
              "Fn::Sub": "${AWS::StackName}/SubnetPrivateAPNORTHEAST2B"
            }
          }
        ],
        "VpcId": {
          "Ref": "VPC"
        }
      }
    }
  }
}

```

* 역시 안된다. 아래처럼 합쳐주자

```
{
  "AWSTemplateFormatVersion": "2010-09-09",
  "Description": "sghaha's subnet",
  "Resources": {
    "VPC": {
      "Type": "AWS::EC2::VPC",
      "Properties": {
        "CidrBlock": "10.0.0.0/16",
        "Tags": [
          {
            "Key": "Name",
            "Value": {
              "Fn::Sub": "${AWS::StackName}/VPC"
            }
          }
        ]
      }
    },
    "SubnetPrivateAPNORTHEAST2B": {
      "Type": "AWS::EC2::Subnet",
      "Properties": {
        "AvailabilityZone": "ap-northeast-2b",
        "CidrBlock": "10.0.1.0/24",
        "Tags": [
          {
            "Key": "Name",
            "Value": {
              "Fn::Sub": "${AWS::StackName}/SubnetPrivateAPNORTHEAST2B"
            }
          }
        ],
        "VpcId": {
          "Ref": "VPC"
        }
      }
    }
  }
}

```
