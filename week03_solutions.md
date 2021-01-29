# Week 3 workshop: Summary of exception types

In the code examples, you will have seen the following types of error:

- **`IndexError`**: a sequence subscript is out of range. For instance, here, we're trying to access `my_list[4]`, but `my_list` only has elements up to `my_list[3]`.
```python
my_list = [1, 2, 3, 4]
print(my_list[4])
```
- **`NameError`**: the variable referred to does not exist -- there is no box in memory with this label. This often comes up when you mistype a variable name.
- **`SyntaxError`**: the code is not syntactically correct --- it is not valid Python, so Python doesn't know how to interpret it.
- **`TypeError`**: a *very* common error to see when learning Python! This means that an operation or a function is applied to an object of the wrong *type*. A few examples:
```python
# Trying to index something that is not a sequence...
my_int = 4
print(my_int[2])
```
```python
# Trying to multiply two lists together...
my_list = [1, 2, 3, 4]
my_other_list = [5, 6, 7]
print(my_list * my_other_list)
```
```python
# Trying to compute the square of a string...
def my_func(x):
    return x ** 2

print(my_func('Why hello there'))
```
- **`ValueError`**: raised when an operation or function is applied to an object with the right *type*, but an invalid *value*. For example, the `int()` function can cast a string to an integer, *if the string can be interpreted as a number*.
```python
a = int('432')    # all good
b = int('hello')  # ValueError (can't interpret this string as an integer)
c = int('1.5')    # ValueError (same issue)
d = int(1.5)      # all good (1.5 is already a number, int() can truncate it to an integer)
```
- **`ZeroDivisionError`**: self-explanatory -- you are trying to divide something by zero.
- **`IndentationError`**: inconsistent or incorrect indentation. Remember, Python determines which commands belong to which block of code using indentation, so it's important to get it right.


### Debugging `find_divisors()`

Reading error traces is really useful to find bugs when they trigger a runtime error. But what about bugs that don't? A mistake in your code which makes it give an incorrect or unexpected result is still a bug.

To find and solve these problems, it's usually a good idea to `print()` some values, to give yourself a better view of what is actually happening in your code. For instance, after fixing all the runtime errors in `find_divisors()`, the added `print()`  statements below are used to show the different steps, and can help you pinpoint where the problem is.

```python
def find_divisors(nums, n):
    '''
    Returns a list of all divisors of n
    present in the list nums.
    '''
    divisors = []
    for i in nums:
        
        print(f'Current number being tested is {i}.')
        print(f'Is {i} a divisor of {n}?')
        
        # Check if n is divisible by i
        print(f'{n} / {i} = {n / i}')
        
        if n // i == 0:
            print(f'Yes, adding {n} to the list\n')
            divisors.append(n)
        else:
            print('No\n')
    
    return divisors

# Test example: result should be [1, 1, 1, 1] (no matter the choice of n)
divisors = find_divisors([1, 1, 1, 1], 97)
print(f'Result: {divisors}\n')

# Test example: result should be [1, 2, 3, 4, 6]
# divisors = find_divisors([1, 2, 3, 4, 5, 6, 7, 8], 12)
# print(f'Result: {divisors}\n')
```

The main issues were:
- A few name errors and syntax errors
- To loop over the elements of `nums`, use `for i in nums:`. See the Week 2 tutorial section on loops.
- Check that the **remainder** of n/i is zero, not the quotient: `if n % i == 0:`
- Append `i` to the list (the current divisor), not `n`
- Return the result, don't just display it on the screen
