# Week 1 - Day 03 - 파이썬 기초 문법 II

## Introduction
### Lecture
- Python Data Structure
- Pythonic code

## Data Structure

### Stack
LIFO  
```python
stack = []
stack.append(1)
stack.pop()
```

### Queue
FIFO  
```python
queue = []
queue.append(1)
queue.pop(0)
```

### Tuple
값 변경이 불가능한 list  
```python
t = (1, 2, 3)
```

### Set
순서가 없고, 중복도 없다.  
합집합, 교집합, 차집합 등 수학의 집합 기능을 가졌다.  
```python
s = {1, 2, 3}
s = set([1, 2, 3])
```

### Dict
key, value 쌍으로 저장한다.  
```python
d = {1:'one', 2:'two'}
```

### Collections
python 자료 구조 모듈  
편의성, 속도가 좋다고 하지만, 굳이 사용하지는 않아도 될것 같다.  
```python
from collections import deque
from collections import Counter
from collections import OrderedDict
from collections import defaultdict
from collections import namedtuple
```

## Pythonic Code
### List Comprehension
```python
result = []
for i in range(10):
    result.append(i)

result = [i for i in range(10)]
```
```python
result = [i for i in range(10) if i % 2 == 0]
result = [i+j for i in range(10) for j in range(10)]
result = [[i+j for i in range(10)] for j in range(10)]
```

### Enumerate
```python
for idx, val in enumerate(['one', 'two', 'three']):
    print(idx, val)
```

### Zip
```python
list1 = [1, 2, 3]
list2 = [4, 5, 6]
for l1, l2 in zip(list1, list2):
    print(l1, l2)
```

### Lamnda
```python
def f(x, y):
    return x + y

f = lambda x, y : x + y
```

### Map
```python
ex = [1, 2, 3, 4, 5]
f = lambda x, y : x + y
list(map(f, ex, ex))
```

### Reduce
```python
from functools import reduce
print(reduce(lambda x, y: x + y, [1, 2, 3, 4, 5]))
```

### Iterable Object
sequence 
```python
arr = [1, 2, 3, 4, 5]
iter_obj = iter(arr)
next(iter_obj)
next(iter_obj)
```

### Generator
```python
def general_list(value):
    result = []
    for i in range(value):
        result.append(i)
    return result
```
```python
def general_list(value):
    for i in range(value):
        yield i
```

```python
gen_ex = (i for i in range(1000))
```

### Arguments
#### Keyword Arguments
```python
def f(arg1, arg2):
    pass

f(arg1='1', arg2='2')
```
#### Default Arguments
```python
def f(arg1, arg2='2'):
    pass

f(arg1='1')
```
#### Variable-Length
```python
def f(arg1, arg2, *args):
    pass

f(1, 2, 3, 4, 5)
```

#### Keyword Variable-Length
```python
def f(**kwargs):
    pass

f(first=1, second=2, third=3)
```

#### Unpacking
```python
arr = [1, 2, 3, 4, 5]
print(*arr) # 1 2 3 4 5
```


## Team
- 과제 코드 리뷰
- github 아이디 공유

