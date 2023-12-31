
## Heap

`Heap`은 `Binary Tree` 기반의 자료구조로, 각 노드는 오름차순 또는 내림차순의 조건을 만족하는 구조를 가진다. `Heap`은 위 조건에 따라 `최대 힙(Max Heap)` 또는 `최소 힙(Mix Heap)`으로 나뉜다. 또한 `Binary Tree`를 기반으로 하기 때문에, 중복된 원소를 허용하지 않는다. 

`최대 힙(Max Heap)`은 각 노드의 값이 그 자식 노드의 값보다 항상 커야 한다. 또한 `최소 힙(Min Heap)`은 각 노드의 값이 그 자식 노드의 값보다 항상 작아야 한다. 이러한 특성으로 `Heap` 자료구조는 정렬에 있어서 느슨한 편이다. 

```python
def push(self, value):
	self.heap.append(value)
	self.heapifyUp()

def pop(self):
	root = self.heap[0] // Heap 최소 값을 임시 저장
	self.heap[0] = self.heap.pop() // Heap의 마지막 원소를 루트로 이동
	self.heapifyDown()
	return root
```

그 이유는 `Heap`에서 삽입 또는 제거를 하는 과정에서 알 수 있는데, `Heapify`가 어떻게 동작하는지 알아야 한다. `Heapify`는 무엇일까? `Heap`의 구조를 유지하도록 해주는 메소드다.

```python
def heapifyDown(self):
	index = 0
	while True:
		leftChildIndex = 2 * index + 1
		rightChildIndex = 2 * index + 2
		
		smallest = index
		if (leftChildIndex < len(self.heap) and
		   self.heap[leftChildIndex] < self.heap[smallest]):
			smallest = leftChildIndex 
			
		if (rightChildIndex < len(self.heap) and
		    self.heap[rightChildIndex] < self.heap[smallest]): 
			smallest = rightChildIndex 
			
		if smallest != index: 
			self.heap[index], self.heap[smallest] = self.heap[smallest], self.heap[index] 
			index = smallest 
		else: 
			break
```

`pop` 메소드를 호출했을 때, 동작하는 `heapifyDown` 메소드는 위와 같다. 단계적으로 살펴보면,

```python
# pop method
self.heap[0] = self.heap.pop()
```

`Heap`의 마지막 원소를 루트로 이동시킨다.

```python
# 이하 heapifyDown
index = 0
```

루트로 이동한 마지막 원소를 `index` 변수에 담아, 초기 타겟으로 한다. 이 `index`는 아래 동작에 따라 변경된다.

```python
while True:
	leftChildIndex = 2 * index + 1
	rightChildIndex = 2 * index + 2
```

위에서 타겟으로 한 `index`의 자식 노드들의 `index`를 계산하여 저장한다.

```python
smallest = index
if (leftChildIndex < len(self.heap) and
	self.heap[leftChildIndex] < self.heap[smallest]):
	smallest = leftChildIndex 
			
if (rightChildIndex < len(self.heap) and
	self.heap[rightChildIndex] < self.heap[smallest]): 
	smallest = rightChildIndex 
```

계산한 자식 노드들의 `index`가 유효한지 검사한 이후, 현재 인덱스, 왼쪽 자식의 인덱스, 오른쪽 자식의 인덱스 중 가장 작은 값의 인덱스를 `smallest`에 저장한다.

```python
if smallest != index: 
			self.heap[index], self.heap[smallest] = self.heap[smallest], self.heap[index] 
			index = smallest
else:
	break
```

위에서 비교했던 결과와 `index`를 비교하여 같지 않은 경우에 `smallest`에 위치하는 값과 `index`에 위치하는 값의 위치를 변경한다. 

	smallest와 index를 비교하는 이유는 만약 같다면 이미 정렬이 된 상태이기 때문. (loop의 끝)

`heapifyUp`은 위와 반대로, 아래부터 올라가는 방식으로 정렬을 진행한다.

위와 같은 방식으로 `Heap`은 자체적으로 정렬을 해서 자기 자신의 조건사항(`Max Heap` 또는 `Min Heap`의 성질)을 충족시킨다.

또한 `Heapify`는 최악의 경우 `O(logN)`의 시간 복잡도를 가진다. 이 시간 복잡도를 활용하여 `N`개의 데이터를 모두 `Heap`에 넣었다가 빼면 정렬하는 것과 동일한 결과를 얻을 수 있고 최악의 경우 `O(NlogN)`의 시간 복잡도를 가지기 때문에 효율적이다.

### Priority Queue

`우선순위 큐(Priority Queue)`는 위에서 설명한 `Heap`을 활용한 자료구조로, 각 원소마다 우선순위를 가지게 된다. 기존의 `Queue`와 같이 FIFO 구조가 아닌, 원소의 우선순위에 따라 배치되므로 우선순위가 가장 높은 원소가 가장 먼저 나오는 구조다.

우선순위는 필요에 따라서 정할 수 있는데, `Max Heap` 또는 `Min Heap`을 통해 가장 작은 값이 우선순위가 될지 또는 가장 큰 값이 우선순위가 될 지를 정해줄 수 있다. 

또한 `Heap`을 직접 구현하지 않고 구현체를 사용하는 경우 구현체가 어떤 방식으로 `Heap`을 구현했는지 확인하고 필요에 따라 삽입 시와 삭제 시에 -를 붙여 반대로 동작하도록 할 수 있다.