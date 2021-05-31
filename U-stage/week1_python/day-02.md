# Week 1 - Day 02 - 파이썬 기초 문법

## Introduction

### Lecture

- Variables
- Function and Console I/O
- Conditionals and Loops
- String and advanced function concept

python 기초 중심의 강의  
변수, 문자열, 리스트, 함수, 조건문, 반복문 등 프로그래밍 언어의 필수적인 내용들이었다.  
그 중에서 python의 특색있는, 잘모르던 부분을 정리하려한다.

## List

다음과 같은 유연함이 데이터 분석 분야에서 python이 중심이 되는데 큰 역할을 했다고 생각한다.  
특히 지금까지 python에서 c나 java처럼 list를 사용했는데, 지금 생각해보면 slicing 으로 좀더 간단하게 해결할 상황이 많았던것 같다.

```python
arr = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
print(arr[:3])  #[0, 1, 2]
print(arr[-3:]) #[7, 8, 9]
print(arr[::2]) #[0, 2, 4, 6, 8]

arr = [1, 99.99, 'string', [0, 0, 1, 0]]

arr = [1, 2, 3]
a, b, c = t
```

## Call by Object Reference

python은 모든것이 object  
객체의 주소가 전달된다는 것만 알면 동작을 이해하기 쉽다.

## Function Type Hint

python의 특징인 dynamic typing  
편리하지만 사용자가 알기 어렵다는 단점도 있다.  
이러한 단점을 해결하기 위해서 type hint 기능을 지원한다.

```python
def function(name:str) -> str:
    return name
```

## docstring

함수에 대한 상세 스펙 정보  
vs code 의 extension 등으로 편리하게 작성 가능하다.

```python
def function():
    """
    docstring
    """
    return
```

## 과제

github에 classroom 기능으로 채점이 자동화 되어있다.  
사실 처음보는 기능인데 교육에는 유용해보이지만, 내가 운영하는 입장이 될 일은 없어보인다.

간단한 수학, 문자열 처리, 야구게임  
문제는 간단했고, 함수 정의에 맞게 처리하는 구조라서 복잡하지 어렵지 않았다.  
팀원들간에 코드리뷰를 할 예정이라서 문제 풀이 자체보다 간결하고 가독성 높은 코드를 만드는 노력을 했다.

## Team

- 협업 툴 논의
- 시간 조율
