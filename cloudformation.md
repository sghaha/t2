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

* 잘되니까, 퍼블릭2개, 프라이빗2개 만들자
* 퍼블릭 a : 10.0.1.0/24
* 퍼블릭 c : 10.0.2.0/24
* 프라이빗 a : 10.0.3.0/24
* 프라이빗 c : 10.0.4.0/24

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
    "SubnetPublicA": {
      "Type": "AWS::EC2::Subnet",
      "Properties": {
        "AvailabilityZone": "ap-northeast-2a",
        "CidrBlock": "10.0.1.0/24",
        "Tags": [
          {
            "Key": "Name",
            "Value": {
              "Fn::Sub": "${AWS::StackName}/SubnetPublicA"
            }
          }
        ],
        "VpcId": {
          "Ref": "VPC"
        }
      }
    },
    "SubnetPublicC": {
      "Type": "AWS::EC2::Subnet",
      "Properties": {
        "AvailabilityZone": "ap-northeast-2c",
        "CidrBlock": "10.0.2.0/24",
        "Tags": [
          {
            "Key": "Name",
            "Value": {
              "Fn::Sub": "${AWS::StackName}/SubnetPublicC"
            }
          }
        ],
        "VpcId": {
          "Ref": "VPC"
        }
      }
    },
    "SubnetPrivateA": {
      "Type": "AWS::EC2::Subnet",
      "Properties": {
        "AvailabilityZone": "ap-northeast-2a",
        "CidrBlock": "10.0.3.0/24",
        "Tags": [
          {
            "Key": "Name",
            "Value": {
              "Fn::Sub": "${AWS::StackName}/SubnetPrivateA"
            }
          }
        ],
        "VpcId": {
          "Ref": "VPC"
        }
      }
    },
    "SubnetPrivateC": {
      "Type": "AWS::EC2::Subnet",
      "Properties": {
        "AvailabilityZone": "ap-northeast-2c",
        "CidrBlock": "10.0.4.0/24",
        "Tags": [
          {
            "Key": "Name",
            "Value": {
              "Fn::Sub": "${AWS::StackName}/SubnetPrivateC"
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

### 3. Outputs로 묶어주기
이제는 길어서 부분부분만 적어야겠따.   
Resources랑 동일한 레벨로 
```
  "Outputs": {
    "SubnetsPublic": {
      "Value": {
        "Fn::Join": [
          ",",
          [
            {
              "Ref": "SubnetPublicA"
            },
            {
              "Ref": "SubnetPublicC"
            }
          ]
        ]
      },
      "Export": {
        "Name": {
          "Fn::Sub": "${AWS::StackName}::SubnetsPublic"
        }
      }
    },
    "SubnetsPrivate": {
      "Value": {
        "Fn::Join": [
          ",",
          [
            {
              "Ref": "SubnetPrivateA"
            },
            {
              "Ref": "SubnetPrivateC"
            }
          ]
        ]
      },
      "Export": {
        "Name": {
          "Fn::Sub": "${AWS::StackName}::SubnetsPrivate"
        }
      }
    },
    "VPC": {
      "Value": {
        "Ref": "VPC"
      },
      "Export": {
        "Name": {
          "Fn::Sub": "${AWS::StackName}::VPC"
        }
      }
    }
  }
```


### 4. 인터넷 게이트 웨이

* 리스소

```
    "InternetGateway": {
      "Type": "AWS::EC2::InternetGateway",
      "Properties": {
        "Tags": [
          {
            "Key": "Name",
            "Value": {
              "Fn::Sub": "${AWS::StackName}/InternetGateway"
            }
          }
        ]
      }
    },
```

### 5. 라우팅 테이블
* 리소스
```
    "PublicRouteTable": {
      "Type": "AWS::EC2::RouteTable",
      "Properties": {
        "Tags": [
          {
            "Key": "Name",
            "Value": {
              "Fn::Sub": "${AWS::StackName}/PublicRouteTable"
            }
          }
        ],
        "VpcId": {
          "Ref": "VPC"
        }
      }
    }

```

* 여기까지
<img width="764" alt="스크린샷 2022-06-16 오후 5 11 23" src="https://user-images.githubusercontent.com/98567497/174024569-492f5728-dc87-4bd0-97c6-825fd4f7b5ec.png">
