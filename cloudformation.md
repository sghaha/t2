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
