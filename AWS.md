How to store the data created by Lambda function?  
Store it in '/tmp' directory  
```
f = open("/tmp/example.txt","w")
f.write("Hello World!")
f.close()
f = open("/tmp/example.txt","r")
f.read()
# Hello World!
```

Upgrade node.js  
```
sudo npm cache clean -f
sudo npm install -g n
sudo n stable
```

DynamoDB saves float number `-3.19` with `Decimal('-3.19')`  
Save the number with `decimal.Decimal(str(number))` instead of number  
Then, we will recieve Decimal('-3.19') when we try to get the number from DynamoDB
```
from decimal import Decimal
data = {"name":"John","salary":123.45}
data["salary"] = Decimal(str(data["salary"]))
# data now is {"name":"John","salary":Decimal("123.45")}
data["salary"]
# Decimal("123.45")
float(data["salary"])
# 123.45
```

Some murmur  
1. Sometime when linked the trigger with S3 before and want to unlink it. Remember to check if the trigger in S3 bucket also turn off  
2. If there is some unknow error happened in lambda function, check permission  