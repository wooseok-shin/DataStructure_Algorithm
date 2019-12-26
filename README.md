## 자료구조 및 알고리즘 정리


#### 자료구조

1. 배열(Array)

* 같은 종류의 데이터를 효율적으로 관리하기 위해 사용  
* 같은 종류의 데이터를 순차적으로 저장

* 장점 : 빠른 접근 가능 - 첫 데이터의 위치에서 상대적인 위치로 데이터 접근(인덱스 번호로 접근)

* 단점 : 데이터 추가 및 삭제가 어려움 - 미리 최대 길이를 지정해야함(다만, 파이썬에서는 자동적으로 처리해준다)  


#### C와 파이썬 배열 Example  
1) C  
'''c
#include <stdio.h>

int main(int argc, char * argv[])
{
    char country[6] = "Korea";
    printf ("%c%c\n", country[0], country[1], country[2], country[3], country[4], country[5]);
    printf ("%s\n", country);    
    return 0;
}
'''

2) Python
'''python
country = "Korea"
print(country[0], country[1], country[2], country[3], country[4], country[5])
print(country)
'''


2. 큐 (Queue)

* 가장 먼저 넣은 데이터를 가장 먼저 꺼낼 수 있는 구조  
	- 줄을 서는 행위와 유사함  
	- 일반적으로는 FIFO(First-In, First-Out) 방식
	
* 용어
	- Enqueue: 큐에 데이터를 넣는 것  
	- Dequeue: 큐에서 데이터를 꺼내는 것

* 주로 멀티 태스킹을 위한 프로세스 스케쥴링 방식을 구현하기 위해 많이 사용됨 (운영체제쪽)

* 파이썬 Queue 라이브러리
'''python
import queue
Fifo_queue = queue.Queue()
Fifo_queue.put('Enqueue')  #데이터 입력
Fifo_queue.put(1)

Fifo_queue.get()   #데이터 출력, 출력물 = "Enqueue"
Fifo_queue.qsize()

'''

* Lifo(Last-In, First-Out) Queue
	- 마지막에 넣은 것이 먼저 나오는 방식
	- 경우에 따라서 Lifo가 사용될 때가 있음
'''python
Lifo_queue = queue.LifoQueue()
'''
	
* Priority Queue
	-우선순위에 따라서 
	
	
'''python
priority_queue = queue.PriorityQueue()
priority_queue.put((10, "Important"))
priority_queue.put((5, "Very important"))
priority_queue.put((15, "so so"))

priority_queue.get() # --> 우선순위가 가장 높은 (5, 'Very important') 출력  
# (우선순위, data) --> Tuple형태로 입력
'''


3. 스택 (Stack)

* LIFO(Last In, Fisrt Out) 또는 FILO(First In, Last Out) 데이터 관리 방식을 따르는 구조
	- Queue의 정책(FIFO)와 반대 개념으로 볼 수 있다
	
* 대표적인 활용: 컴퓨터 내부의 프로세스 구조의 함수 동작 방식, 프로세스 스택

* 주요 기능  
  - push(): 데이터를 스택에 넣기  (파이썬 리스트기능에서 제공하는 append 메소드로 구현가능)
  - pop(): 데이터를 스택에서 꺼내기

![stack](https://user-images.githubusercontent.com/46666862/71476609-366b6700-2829-11ea-9729-80d4cabb3396.png)

'''python
# 재귀 함수
def recursive(data):
    if data < 0:
        print ("ended")
    else:
        print(data)
        recursive(data - 1)
        print("returned", data)
		
reculsive(4)
'''
'''
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
'''

* 위처럼 함수의 동작방식이 스택과 유사하다. 프로세스 함수 동작방식에서 많이쓰인다

* 장점
	- 구조가 단순해서, 구현이 쉽다
	- 데이터 저장 및 읽기 속도가 빠르다

* 단점
	- 데이터 최대 개수를 미리 정해야 한다
		- 파이썬에서 재귀 함수는 1000번까지만 호출 가능
	- 따라서, 저장 공간의 낭비가 발생할 수 있다