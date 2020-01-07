# 자료구조 및 알고리즘 정리


## 자료구조  



### 1. 배열(Array)  

* 같은 종류의 데이터를 효율적으로 관리하기 위해 사용  
* 같은 종류의 데이터를 순차적으로 저장

* 장점 : 빠른 접근 가능 - 첫 데이터의 위치에서 상대적인 위치로 데이터 접근(인덱스 번호로 접근)

* 단점 : 데이터 추가 및 삭제가 어려움 - 미리 최대 길이를 지정해야함(다만, 파이썬에서는 자동적으로 처리해준다)  


#### C와 파이썬 배열 Example  
(1) C


```c
#include <stdio.h>

int main(int argc, char * argv[])
{
    char country[6] = "Korea";
    printf ("%c%c\n", country[0], country[1], country[2], country[3], country[4], country[5]);
    printf ("%s\n", country);    
    return 0;
}
```

(2) Python
```python
country = "Korea"
print(country[0], country[1], country[2], country[3], country[4], country[5])
print(country)
```
  
  
  
### 2. 큐 (Queue)  

* 가장 먼저 넣은 데이터를 가장 먼저 꺼낼 수 있는 구조  
	- 줄을 서는 행위와 유사함  
	- 일반적으로는 FIFO(First-In, First-Out) 방식
	
* 용어
	- Enqueue: 큐에 데이터를 넣는 것  
	- Dequeue: 큐에서 데이터를 꺼내는 것

* 주로 멀티 태스킹을 위한 프로세스 스케쥴링 방식을 구현하기 위해 많이 사용됨 (운영체제쪽)

* 파이썬 Queue 라이브러리
```python
import queue
Fifo_queue = queue.Queue()
Fifo_queue.put('Enqueue')  #데이터 입력
Fifo_queue.put(1)

Fifo_queue.get()   #데이터 출력, 출력물 = "Enqueue"
Fifo_queue.qsize()

```

* Lifo(Last-In, First-Out) Queue
	- 마지막에 넣은 것이 먼저 나오는 방식
	- 경우에 따라서 Lifo가 사용될 때가 있음

```python
Lifo_queue = queue.LifoQueue()
```
	
* Priority Queue
	-우선순위에 따라서 출력된다
	
```python
priority_queue = queue.PriorityQueue()
priority_queue.put((10, "Important"))
priority_queue.put((5, "Very important"))
priority_queue.put((15, "so so"))

priority_queue.get() # --> 우선순위가 가장 높은 (5, 'Very important') 출력  
# (우선순위, data) --> Tuple형태로 입력
```
  
  
### 3. 스택 (Stack)  
  
* LIFO(Last In, Fisrt Out) 또는 FILO(First In, Last Out) 데이터 관리 방식을 따르는 구조
	- Queue의 정책(FIFO)와 반대 개념으로 볼 수 있다
	
* 대표적인 활용: 컴퓨터 내부의 프로세스 구조의 함수 동작 방식, 프로세스 스택

* 주요 기능  
  - push(): 데이터를 스택에 넣기  (파이썬 리스트기능에서 제공하는 append 메소드로 구현가능)
  - pop(): 데이터를 스택에서 꺼내기

![stack](https://user-images.githubusercontent.com/46666862/71476609-366b6700-2829-11ea-9729-80d4cabb3396.png)

```python
# 재귀 함수
def recursive(data):
    if data < 0:
        print ("ended")
    else:
        print(data)
        recursive(data - 1)
        print("returned", data)
		
reculsive(4)
```
```
결과
4
3
2
1
0
ended
returned 0
returned 1
returned 2
returned 3
returned 4
```

* 위처럼 함수의 동작방식이 스택과 유사하다. 프로세스 함수 동작방식에서 많이쓰인다

* 장점
	- 구조가 단순해서, 구현이 쉽다
	- 데이터 저장 및 읽기 속도가 빠르다

* 단점
	- 데이터 최대 개수를 미리 정해야 한다
		- 파이썬에서 재귀 함수는 1000번까지만 호출 가능
	- 따라서, 저장 공간의 낭비가 발생할 수 있다
	
	
	
	  
### 4. 링크드 리스트 (=연결 리스트)  



* 배열은 순차적으로 연결된 공간에 데이터를 나열하는 데이터 구조  
* 링크드 리스트는 떨어진 곳에 존재하는 데이터를 화살표로 연결해서 관리하는 구조  
* 배열은 미리 특정한 공간(사이즈)을 예약해야하지만 링크드리스트는 추가할 수 있음. 배열의 단점 극복  
* <font color='#BF360C'>본래 C언어에서는 주요한 데이터 구조이지만, 파이썬은 리스트 타입이 링크드 리스트의 기능을 모두 지원</font>  


* 데이터값과 포인터(주소)로 구성되어있음 --> 이를 노드라고 부른다.  
* 포인터 : 각 노드 안에서, 다음이나 이전 노드와의 연결 정보를 가지고 있는 공간

![노드,포인터](https://user-images.githubusercontent.com/46666862/71557091-927df780-2a84-11ea-9a8e-9eb5d57eacd0.PNG)


  

* 간단한 링크드 리스트 예시  
	
```python
Node 구현하기
```  
```python
class Node:
	def __init__(self, data, next=None):
		self.data = data
		self.next = next

```

	- Node와 Node 연결하기(포인터 활용)
	
```python
node1 = Node(1)
node2 = Node(2)
node1.next = node2
head = node1   # 가장 앞에있는 주소를 저장해놓기
```
  
	- 데이터 추가하기
	  
```python
def add(data):
	node = head
	while node.next:
		node = node.next
	node.next = (data)
	
node1 = Node(1)
head = node1
for index in range(2,10):
	add(index)
```
  
	- 링크드 리스트 데이터 출력하기
	
```python
node = head
while node.next:
	print(node.data)
	node = node.next
print(node.data)
```
  
  
  
#### 링크드 리스트의 장단점(C언어에서의)

* 장점
  - 미리 데이터 공간을 미리 할당하지 않아도 됨
    - 배열은 **미리 데이터 공간을 할당** 해야 함
  

* 단점
  - 연결을 위한 별도 데이터 공간이 필요하므로, 저장공간 효율이 높지 않음
  - 연결 정보를 찾는 시간이 필요하므로 접근 속도가 느림
  - 중간 데이터 삭제시, 앞뒤 데이터의 연결을 재구성해야 하는 부가적인 작업 필요
  
  
  
   
#### Double Linked list (이중 연결 리스트)

  
- 장점 : 양방향으로 연결되어 있어 노드 탐색이 양쪽으로 모두 가능(뒤에서부터도 탐색 가능)
![이중연결리스트](https://user-images.githubusercontent.com/46666862/71594663-2b436e80-2b7c-11ea-89a0-4a210bf15e29.PNG)
  
  
- 더블 링크드 리스트 : 특정 노드 앞과 뒤에 데이터 추가하기  
  
```python
class Node:
    def __init__(self, data, prev=None, next=None):
        self.prev = prev
        self.data = data
        self.next = next

class NodeMgmt:
    def __init__(self, data):
        self.head = Node(data)
        self.tail = self.head
    
    def insert_before(self, data, before_data):
        if self.head == None:
            self.head = Node(data)
            return True            
        else:
            node = self.tail
            while node.data != before_data:
                node = node.prev
                if node == None:
                    return False
            new = Node(data)
            before_new = node.prev
            before_new.next = new
            new.next = node
            return True

    def insert_after(self, data, after_data):
        if self.head == None:
            self.head = Node(data)
            return True            
        else:
            node = self.head
            while node.data != after_data:
                node = node.next
                if node == None:
                    return False
            new = Node(data)
            after_new = node.next
            new.next = after_new
            new.prev = node
            node.next = new
            if new.next == None:
                self.tail = new
            return True

    def insert(self, data):
        if self.head == None:
            self.head = Node(data)
        else:
            node = self.head
            while node.next:
                node = node.next
            new = Node(data)
            node.next = new
            new.prev = node
            self.tail = new

    def desc(self):
        node = self.head
        while node:
            print (node.data)
            node = node.next


# 테스트

node_mgmt = NodeMgmt(0)
for data in range(1, 10):
    node_mgmt.insert(data)

node_mgmt.desc()

node_mgmt.insert_after(1.5, 1)
node_mgmt.desc()


```
  
  
  
  
### 시간 복잡도

- 동일한 문제를 풀 때 알고리즘을 구현하는 방법은 여러가지가 될 수 있다.  
- 따라서, 다양한 알고리즘 중 어떤 것이 더 좋은지를 분석하기 위해, 복잡도를 정의하고 계산한다.  

- 알고리즘 복잡도에는 2가지 항목이 있다.  
	- 1)시간 복잡도: 알고리즘의 실행 속도
	- 2)공간 복잡도: 알고리즘이 사용하는 메모리 사이즈
	
- 최근에는 시간 복잡도만을 주로 사용한다.  
- 알고리즘 시간 복잡도에 영향을 가장 많이 미치는 요소는 **반복문**이다.
  
#### 알고리즘 성능 표기법

- Big O (빅-오) 표기법: O(N)
  - 알고리즘 최악의 실행 시간을 표기
  - **가장 많이/일반적으로 사용함**
  - **아무리 최악의 상황이라도, 이정도의 성능은 보장한다는 의미도 지닌다**

- Ω (오메가) 표기법:  Ω(N)
  - 오메가 표기법은 알고리즘 최상의 실행 시간을 표기

- Θ (세타) 표기법: Θ(N)
  - 오메가 표기법은 알고리즘 평균 실행 시간을 표기

> 시간 복잡도 계산은 반복문이 핵심 요소임을 인지하고, 계산 표기는 최악의 시간인 Big-O 표기법을 중심으로 익히면 된다.  


#### Big-O 표기법

* O(입력)
  - 입력 n 에 따라 결정되는 시간 복잡도 함수
  - O(1), O(log n), O(n), O(nlog n), O(n^2), O(2^n), O(n!)등으로 표기한다
  - 입력 n 의 크기에 따라 기하급수적으로 시간 복잡도가 늘어날 수 있다
    - O(1) < O(log n) < O(n) < O(nlog n) < O(n^2) < O(2^n) < O(n!)
      - cf)log n 의 밑은 2 - log_2 n
  

* 단순하게 입력 n에 따라, 몇번 실행이 되는지를 계산하면 된다.
  - **표현식에 가장 큰 영향을 미치는 n 의 단위로 표기한다.**
  - n이 1이든 100이든, 1000이든, 10000이든
    - 무조건 2회(상수회) 실행한다: O(1) 
       ```python
            if n > 10:
                 print(n)
       ```
    - n에 따라, n번, n + 10 번, 또는 3n + 10 번등 실행한다: O(n)
       ```python
            variable = 1
            for num in range(3):
                for index in range(n):
                     print(index)
       ```
    - n에 따라, n^2번, n^2 + 1000 번, 100n^2 - 100, 또는 300n^2 + 1번등 실행한다: O(n^2)
       ```python
            variable = 1
            for i in range(300):
                for num in range(n):
                    for index in range(n):
                         print(index)
		```
						 
						 
![시간복잡도](https://user-images.githubusercontent.com/46666862/71728827-85e11100-2e81-11ea-8cdd-523c5adf49b1.png)
