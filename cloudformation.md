# cloudformation 체험해보기

공부중!

### 1. VPC 만들기
```
{
    "Resources": {
        "VPC": {
            "Type": "AWS::EC2::VPC",
            "Properties": {
                "CidrBlock" : "10.0.0.0/16",
                "Tags" : [
                     {"Key" : "Name", "Value" : "sghahaVPC" },
                ],
            }
        }
    }
}
```
