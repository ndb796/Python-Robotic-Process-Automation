### 3장 파이썬 문법 핵심 요약 – 심화

#### 프로그래밍을 제어하기 위한 문법

* 다양한 업무를 자동화할 때, 조건에 따라서 데이터를 처리해야 하는 경우가 많습니다.

#### 1) 조건문

* 조건문은 프로그램 실행의 흐름을 제어합니다.
* 일반적으로 프로그램은 사용자의 입력에 따라서 결과를 뱉는 방식으로 작성됩니다.
    * 사용자로부터 입력을 받을 때는 input() 함수를 사용합니다. 

```
x = int(input())
y = int(input())

print(x / y)
```

* 조건문은 <b>if 구문</b>을 이용해 작성합니다.
    * 조건문 내부에 대하여 띄어쓰기를 4번 사용합니다.
    * 어떠한 값이 다른 값과 동일한지 구할 때는 등호를 2번 사용해 "=="라고 씁니다.

```
x = int(input())
y = int(input())

if y == 0:
    print('0으로 나눌 수 없습니다.')
else:
    print(x / y)
```

* if에 해당하지 않는다면 elif가 수행되고, 위쪽에 있는 모든 조건문에 해당하지 않을 때 else 구문이 실행됩니다.
    * 이때 elif나 else는 옵션으로, 없어도 됩니다.

```
score = 75

if score >= 94: # 94점부터 100점
    print('1등급입니다.')
elif score >= 87: # 93점부터 87점
    print('2등급입니다.')
elif score >= 81: # 86점부터 81점
    print('3등급입니다.')
else:
    print('3등급 미만입니다.')
```

#### 2) 반복문

* 반복적인 반복적인 작업을 대신해주기 위해 효과적입니다.

```
for x in [1, 2, 3, 4, 5, 6, 7, 8, 9]:
    print(x)
```

* for문은 어떠한 시퀀스의 원소에 차례대로 접근한다는 점에서 range() 함수와 함께 사용됩니다.
    * range(start, end) 형태가 가장 많이 사용됩니다.
* for문과 range() 함수를 배웠기 때문에, 다양한 프로그램을 작성할 수 있습니다.
* 1부터 50까지의 수를 더한 값을 계산해 봅시다.

```
result = 0
for i in range(1, 51): # 1부터 50까지 방문
    result += i

print(result)
```

* 1부터 50까지의 수 중에서 10의 배수만 더하는 프로그램을 작성할 수 있습니다.

```
result = 0
for i in range(1, 51):
    if i % 10 == 0:
        result += i

print(result)
``` 

* enumerate() 함수를 사용하면 인덱스와 함께 반복할 수 있습니다.

```
name_list = ['홍길동', '이순신', '장보고']

for i, element in enumerate(name_list):
    print(i, element)
```

* 반복문을 중첩해서 사용할 수도 있습니다.
    * 구구단 예제를 확인해 봅시다.

```
for i in range(1, 10):
    for j in range(1, 10):
        print(i, "X", j, "=", i * j)
```

* 1부터 N까지의 수 중에서 소수를 찾는 프로그램을 작성할 수 있습니다.
    * 소수가 아닌 경우, 어떤 수의 배수인지 출력한 뒤에 해당 수에 대한 반복문을 탈출합니다.
    * break 구문은 해당 break 구문을 포함하는 반복문을 탈출합니다.

```
n = 10
for x in range(i, n + 1):
    prime_number = True
    for y in range(2, x):
        if x % y == 0: # 나누어 떨어지는 수가 있다면
            print(x, "=", y, "*", x // y)
            prime_number = False
            break # 반복문 탈출
    if prime_number:
        print(x, "는 소수입니다.")
```

#### 3) 함수

* 함수를 이용해 소스 코드를 기능별로 분리할 수 있습니다.
    * 각 부품(함수)이 서로 조화를 이루어 하나의 완성된 프로그램을 만들 수 있습니다.
* 함수는 def 구문을 이용하여 작성할 수 있습니다.
* 세 개의 수를 입력받아 더한 결과를 반환하는 함수를 작성해 봅시다.
 
 ```
def add(a, b, c):
    result = a + b + c
    return result

print(add(3, 5, 7))
```

```
def add(a, b, c):
    result = a + b + c
    return result

print(add(3, 5, 7))
print(add(5, 5, 2))
print(add(100, 200, 300))
```
 
* 리스트 내 원소 중에서 가장 큰 값의 인덱스(위치)를 찾아서 반환하는 함수를 작성해 봅시다.

```
def find_max_index(arr):
    max_index = 0
    for i in range(len(arr)):
        if arr[max_index] < arr[i]: # 더 큰 값을 찾은 경우
            max_index = i
    return i

data = [7, 1, 5, 9, 3, 2, 4]
max_index = find_max_index(data)
print(max_index)
```

* 특정한 값을 가지는 원소의 인덱스를 찾는 함수를 작성해 봅시다.

```
def find_certain_value(arr, value):
    for i, x in enumerate(arr):
        if x == value:
            return i
    return -1 # 찾지 못한 경우 -1을 반환

print(find_certain_value([3, 5, 7, 9], 2))
print(find_certain_value([3, 5, 7, 9], 7))
```
