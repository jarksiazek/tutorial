# List #
```python
numbers = [5, 2, 1, 3]
numbers.append(12)
# [5, 2, 1, 3, 12]

numbers.insert(0, 22)
# [22, 5, 2, 1, 3, 12]

numbers.remove(22)
# [5, 2, 1, 3, 12]

numbers.pop()
# [5, 2, 1, 3] - removing last item from the list

numbers.index(5)
# 0 - fist occurrence [5, 2, 1, 3]

numbers.index(6)
# value error - not in the list [5, 2, 1, 3]

6 in numbers
# false - not in the list [5, 2, 1, 3]

numbers.counter(5)
# 1 - one number 5 in the list [5, 2, 1, 3]

numbers.sort()
# [1, 2, 3, 5]

numbers.reverse()
# [5, 3, 2, 1]

numbers2 = numbers.copy()
# deep copy

numbers.clear()
# []
```