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
