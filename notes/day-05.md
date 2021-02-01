# U-Stage Week1(Python) - Day 05

## Introduction


## Exception

```python
try:
    # 예외 발생 가능 코드
except <Exception Type>:
    # 예외 발생시 동작하는 코드
else:
    # 예외가 발생하지 않을 때 동작하는 코드
finally:
    # 예외 발생 여부와 상관없이 실행됨
```

```python
try:
    10 / 0
except ZeroDivisionError as e:
    print(e)
except IndexError as e:
    print(e)
except Exception as e:
    print(e)
```

## Raise
강제로 Exception 발생  
```python
raise <Exception Type>(예외정보)
raise ValueError("Value Error!")
```

## Assert
특정 조건을 만족하지 않을 경우 예외 발생  
```python
assert 예외조건
assert isinstance(1, int)
```


## File

```python
f = open("파일이름", "접근모드")
f.close()
```

### Read
```python
f = open("파일이름", "r")
print(f.readline())
print(f.read())
f.close()

with open("파일이름", "r") as f:
    print(f.readline())
    print(f.read())
```

### Write
```python
f = open("파일이름", "w", encoding="utf8")
f.wrtie("write")
f.close()

f = open("파일이름", "a", encoding="utf8")
f.wrtie("append")
f.close()
```

### Directory
```python
import os
import pathlib
```

### Pickle
```python
import pickle

class Test:
    pass
test = Test()

f = open("test_object.pickle", "wb")
pickle.dump(test, f)
f.close()

f = open("test_object.pickle", "rb")
test_pickle = pickle.load(f)
```

## Log Handling
### Logging
```python
import logging

logging.debug("debugging")
logging.info("information")
logging.warning("warning")
logging.error("err")
logging.critical ("critical")
```

### Configparser
프로그램 실행 설정을 file에 저장  
section, key, value 형태  
```
# example.cfg
[SectionOne]
Status: Single
Name: Derek
Value: Yes

[SectionTwo]
Color = Green

[SectionThree]
Age: 30
```
```python
import configparser
config = configparser.ConfigParser()
config.sections()

config.read('example.cfg')
config.sections()

for key in config['SectionOne']:
    print(key)

config['SectionOne']["status"]
```

### Argparser
console에서 프로그램 실행시 setting  

```python
import argparse
parser = argparse.ArgumentParser(description='PyTorch MNIST Example')
parser.add_argument('--batch-size', type=int, default=64, metavar='N', help='input batch size for training (default:64)')
parser.add_argument('--test-batch-size', type=int, default=1000, metavar='N', help='input batch size for testing(default: 1000)')
parser.add_argument('--epochs', type=int, default=10, metavar='N', help='number of epochs to train (default: 10)')
parser.add_argument('--lr', type=float, default=0.01, metavar='LR', help='learning rate (default: 0.01)')
parser.add_argument('--momentum', type=float, default=0.5, metavar='M', help='SGD momentum (default: 0.5)')
parser.add_argument('--no-cuda', action='store_true', default=False, help='disables CUDA training')
parser.add_argument('--seed', type=int, default=1, metavar='S', help='random seed (default: 1)’)
parser.add_argument('--save-model', action='store_true', default=False, help='For Saving the current Model')
args = parser.parse_args()
```

## Data Handling
### CSV (Comma Separate Value)

### HTML (Hyper Text Markup Language)

### XML (eXtensible Markup Language)

### JSON (JavaScript Object Notation)

### 정규식 (Regular Expression)
[정규식 연습](https://regexr.com/)

```python
import re
re.findall(r"([A-Za-z0-9])", "ABC_abc_123")
```


## Team
- 아이스 브레이킹
- 조교님과 간단한 자기소개
- 팀에 대한 조언 등

