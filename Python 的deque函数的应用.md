# Python 的deque函数的应用

## 在Python中， deque 是一个双向队列，

它支持从队列的两端进行插入和删除操作。以下是 deque 的一些主要函数：

-  *append(x) ：在队列的右侧添加一个元素x。*
-  *appendleft(x) ：在队列的左侧添加一个元素x。*
-  *pop() ：从队列的右侧移除一个元素并返回它。如果队列为空，则会引发 IndexError 。*
-  *popleft() ：从队列的左侧移除一个元素并返回它。如果队列为空，则会引发 IndexError 。*
-  *clear() ：清空队列中的所有元素。*
-  *count(x) ：返回队列中元素x的数量。*
-  *extend(iterable) ：在队列的右侧添加一系列元素，这些元素来自于另一个可迭代对象。*
-  *extendleft(iterable) ：在队列的左侧添加一系列元素，这些元素来自于另一个可迭代对象。*
-  *index(x, i=0, j=len(d))) ：返回队列中元素x的第一个匹配项的索引。索引是从0开始计数的。*
-  *insert(i, x) ：在队列中的指定位置插入元素x。*
-  *rotate(n=1) ：将队列向右旋转n次。如果n为负数，则向左旋转。*
-  *reverse() ：将队列中的元素顺序反转。*
-  *copy() ：返回一个新的 deque 对象，其中包含当前队列的所有元素。*
-  *maxlen ：获取或设置队列的最大长度。如果队列的长度超过了 maxlen ，那么当有新元素添加到队列时，最左边的元素将被自动删除。*

## 简单示例：

```python
from collections import deque
# 创建一个双向队列

d = deque()

# 在队列右侧添加元素

d.append(1)
d.append(2)
d.append(3)

# 在队列左侧添加元素

d.appendleft(0)

# 检查队列中的元素

print("Elements in the deque:", d)

# 移除右侧的元素

print("Pop from right:", d.pop())
```



 