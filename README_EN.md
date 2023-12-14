[ English | [中文](README.md) ]
# euuid

There are a total of 5 ways to generate uuid (universal unique identification code) in python. This package provides three other methods to generate uuid, which is a supplement to the python package of uuid.

## Install

    pip install euuid

## Theory
- The first method euuid: uuid = random string + timestamp, there is a negligible probability of generating duplicate ids
   - A random string is a string consisting of n characters randomly selected from English letters and numbers. The number n defaults to 12 and can also be customized. When the number n defaults to 12, the probability of repetition per millisecond is 1/4738381338321616896. Since the probability is extremely small, it can be considered that the ID generated each time is not repeated.
   - timestamp in milliseconds
- The second method euuid2: uuid = self-increasing numeric id + random string + timestamp, which can generate a completely unique id
   - Auto-incrementing numeric id: 0, 1, 2, 3, ..., n
   - A random string is a string randomly selected from English letters. Its length is equal to the input quantity minus the character length of the self-increasing numeric ID. As the character length of the auto-incremented numeric ID becomes larger, the length of the random string will become 0

- The third method euuid3: uuid = custom tag string + # + random string + timestamp, which can generate completely unique ids
   - A random string is a string consisting of n characters randomly selected from English letters and numbers. If the length of the custom tag string is greater than or equal to 12, the random string is empty. Otherwise, the length of the random string is equal to 12 minus the custom tag. length of string
   - Returns base64 encoded data by default

## Use
### euuid
```python3
from euuid import euuid

print(euuid())
```

### euuid2
```python3
from euuid import euuid2

# Initialize the class and enter the namespace with an auto-increment number
# The default saving location for self-increasing digital IDs is the current directory, and the file name is euuid.pkl, which can also be customized.
# Customization: euid = euuid2('test', './test.pkl')
euid = euuid2('test')
# The self-increasing numeric id at the beginning of printing
print(euid.number_id)

# Print the auto-incrementing numeric id plus the length of the randomly generated str. The default is 12, which can also be customized.
print(euid.str_len)

# Output 10 uuid
for i in range(10):
    print(euid.generate_unique_id())
# Save the incremented numeric ID
euid.change_number_id()
```
### euuid3
```python3
from euuid import euuid3

# By default, base64 encoded data is returned
print(euuid3('panda'))

# Returns data without base64 encoding
print(euuid3('panda', is_base64=False))
```


