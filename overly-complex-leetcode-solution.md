# Overcomplex LeetCode Solution
## OK Sean so here it is

```python
class AddableArray:
    def __init__(self, addables):
        self.__addables = addables
        total_sum = sum(addables)
        self.__memo = {
            (0, len(self.__addables)): total_sum
        }
    def __call__(self, lower=0, upper=None):
        if (lower, upper) in self.__memo:
            return self.__memo[(lower, upper)]
        else:
            new_sum = sum(self.__addables[lower:upper])
            self.__memo[(lower, upper)] = new_sum
            return new_sum

leetcode_solution = AddableArray(range(10))

print(leetcode_solution(2, 5))
print(sum(range(2, 5)))

# More testing etc. find the bugs!
```

Well, it does what I've asked it to so far, including responding specifically to any objects using the `__add__` method, not just numbers, implementing memoization as well as the `__call__` method rather than using an explicitly named method to avoid extra typing. It also respects Pythonic style conventions.

All this in a few minutes after my first bout of epilepic convulsion just this night. Yay me!
