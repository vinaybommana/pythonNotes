# Generators

* consider a function to square every number in a list
  and gives the result in the form of a list.

```python
def square_numbers(nums):
    result = []
    for i in nums:
        result.append(i * i)
    return result

my_nums = square_numbers([1, 2, 3, 4, 5])

print my_nums
```

* we can convert the function `square_numbers` into generator.
```python
def square_numbers(nums):
    for i in nums:
        yield (i * i)

my_nums = square_numbers([1, 2, 3, 4, 5])

for num in my_nums:
    print(num)
```
