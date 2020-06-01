# Vim Script for Python Developers

A guide to Vim Script development for Python developers. Sample code for the various expressions, statements, functions and programming constructs is shown in both Python and Vim Script. This is not intended to be a tutorial for developing Vim scripts. It is assumed that the reader is familiar with programming in Python.

For an introduction to Vim Script development, refer to [usr_41.txt](https://vimhelp.org/usr_41.txt.html), [eval.txt](https://vimhelp.org/eval.txt.html) and [Learn Vimscript the Hard Way](https://learnvimscriptthehardway.stevelosh.com/)

For a similar guide for JavaScript developers, refer to [Vim Script for the JavaScripter](https://w0rp.com/blog/post/vim-script-for-the-javascripter/)

This guide only describes the programming constructs that are present in both Python and Vim. The constructs that are unique to Vim (e.g. [autocommands](https://vimhelp.org/autocmd.txt.html#autocommands), [key-mapping](https://vimhelp.org/map.txt.html#key-mapping), [abbreviations](https://vimhelp.org/map.txt.html#abbreviations), [user-commands](https://vimhelp.org/map.txt.html#user-commands), [plugins](https://vimhelp.org/usr_05.txt.html#plugin), etc.) are not described in this guide.

Some of the features described in this guide are available are only in recent versions of Vim (8.1).

The Github repository for this gist is available at: https://github.com/yegappan/VimScriptForPythonDevelopers.

------------------------------------------------------------------------------

## Variables

### Creating a Variable
**Python:**
```python
i = 10
pi = 3.1415
str = "Hello"
a, b, s = 10, 20, "sky"
```

**VimScript:**
```vim
let i = 10
let pi = 3.1415
let str = "Hello"
let [a, b, s] = [10, 20, "sky"]
```

*Help:* [variables](https://vimhelp.org/eval.txt.html#variables)

### Deleting a Variable
**Python:**
```python
del str
```

**VimScript:**
```vim
unlet str
```

*Help:* [:unlet](https://vimhelp.org/eval.txt.html#%3Aunlet)

### Here Document
Assigning multi-line values to a variable.

**Python:**
```python
i = """
    one
    two
    three
"""
i = i.strip().split()
```

**VimScript:**
```vim
let i =<< trim END
    one
    two
    three
END
```

*Help:* [:let-heredoc](https://vimhelp.org/eval.txt.html#%3Alet-heredoc)

## Print an expression

**Python:**
```python
print("Hello World\n")
s = "vim"
print("Editor = %s" % (s))
```

**VimScript:**
```vim
echo "Hello World"
let s = "vim"
echo "Editor = " .. s
```

*Help:* [:echo](https://vimhelp.org/eval.txt.html#%3Aecho)

------------------------------------------------------------------------------

## Arithmetic Operators

What|Python|VimScript
----|------|---------
addition| a = 10 + 20 | let a = 10 + 20
subtraction| a = 30 - 10 | let a = 30 - 10
multiplication| a = 3 * 5 | let a = 3 * 5
division| a = 22 / 7 | let a = 22 / 7
addition| a += 1 | let a += 1
subtraction| a -= 2 | let a -= 2
multiplication| a *= 4 | let a *= 4
division| a /= 2 | let a /= 2
modulus| a = 10 % 3 | let a = 10 % 3
exponentiation| a = 2 ** 3 | let a = float2nr(pow(2, 3))
floor division| a = 10 // 3 | let a = floor(10 / 3.0)

*Help:* [expr5](https://vimhelp.org/eval.txt.html#expr5)

------------------------------------------------------------------------------

## Comparison Operators

What|Python|VimScript
----|------|---------
equal to|  a == b  |  a == b
not equal to|  a != b  |  a != b
greater than|  a > b |  a > b
less than|  a < b  |  a < b
greater than or equal to|  a >= b  |  a >= b
less than or equal to|  a <= b  |  a <= b

*Help:* [expr4](https://vimhelp.org/eval.txt.html#expr4)

------------------------------------------------------------------------------

## Logical Operators

What|Python|VimScript
----|------|---------
logical and| x and y | x && y
logical or| x or y | x \|\| y
logical not| not x | !x

*Help:* [expr2](https://vimhelp.org/eval.txt.html#expr2)

------------------------------------------------------------------------------

## Bitwise Operators

What|Python|VimScript
----|------|---------
bitwise AND| c = a & b | let c = and(a, b)
bitwise OR| c = a \| b | let c = or(a, b)
bitwise NOT| c = ~a | let c = invert(a)
bitwise XOR| c = x ^ y | let c = xor(a, b)

*Help:* [and()](https://vimhelp.org/eval.txt.html#and%28%29), [or()](https://vimhelp.org/eval.txt.html#or%28%29), [invert()](https://vimhelp.org/eval.txt.html#invert%28%29), [xor()](https://vimhelp.org/eval.txt.html#xor%28%29)

------------------------------------------------------------------------------

## String

Vim has functions for dealing with both multibyte and non-multibyte strings. Some functions deal with bytes and some functions deal with characters. Refer to the reference guide for the various functions to get the detailed information.

### Raw string

**Python:**
```python
s1 = r"one\ntwo\n"
s2 = "one\ntwo\n"
```

**VimScript:**
```vim
let s1 = 'one\ntwo\n'
let s2 = "one\ntwo\n"
```

*Help:* [literal-string](https://vimhelp.org/eval.txt.html#literal-string), [string](https://vimhelp.org/eval.txt.html#string)

### Finding string length
**Python:**
```python
n = len("Hello World")
```

**VimScript:**
```vim
let n = len("Hello World")
let n = strlen("Hello World")
```

*Help:* [len()](https://vimhelp.org/eval.txt.html#len%28%29), [strlen()](https://vimhelp.org/eval.txt.html#strlen%28%29), [strwidth()](https://vimhelp.org/eval.txt.html#strwidth%28%29), [strdisplaywidth()](https://vimhelp.org/eval.txt.html#strdisplaywidth%28%29)

### String Concatenation
**Python:**
```python
str1 = "blue"
str2 = "sky"
s = str1 + str2
```

**VimScript:**
```vim
let str1 = "blue"
let str2 = "sky"
let s = str1 .. str2
```

*Help:* [expr-..](https://vimhelp.org/eval.txt.html#expr-..)

### Getting a substring

In Python, when using an index range to specify a sequence of characters in a string, the character at the end index is not included. In Vim, the character at the end index is included.

**Python:**
```python
str = "HelloWorld"
sub = str[2:5]
```

**VimScript:**
```vim
let str = "HelloWorld"
let sub = str[2:4]
let sub = strpart(str, 2, 3)
```

*Help:* [expr-[:]](https://vimhelp.org/eval.txt.html#expr-[%3a]), [strpart()](https://vimhelp.org/eval.txt.html#strpart%28%29)

### Counting the occurrences of a substring
**Python:**
```python
str = "Hello World"
c = str.count("l")
```

**VimScript:**
```vim
let str = "Hello World"
let c = str->count("l")
```

*Help:* [count()](https://vimhelp.org/eval.txt.html#count%28%29)

### Checking whether a substring is present
**Python:**
```python
str = "running"
idx = str.find("nn")
idx = str.rfind("ing")
```

**VimScript:**
```vim
let str = "running"
let idx = str->stridx("nn")
let idx = str->strridx("ing")
endif
```

*Help:* [stridx()](https://vimhelp.org/eval.txt.html#stridx%28%29), [strridx()](https://vimhelp.org/eval.txt.html#strridx%28%29)

### Checking whether a string starts with or ends with a substring
**Python:**
```python
str = "running"
if str.startswith("run"):
    print("starts with run")
if str.endswith("ing"):
    print("ends with ing")
```

**VimScript:**
```vim
let str = "running"
if str =~# "^ing"
    echo "starts with ing"
if str =~# "ing$"
    echo "ends with ing"
endif
```

*Help:* [expr-=~#](https://vimhelp.org/eval.txt.html#expr-=~#)

### Merging strings in a List with a separator
**Python:**
```python
s = ":".join(['a', 'b', 'c'])
```

**VimScript:**
```vim
let s = join(['a', 'b', 'c'], ':')
```

*Help:* [join()](https://vimhelp.org/eval.txt.html#join%28%29)

### Changing the case of letters in a string
**Python:**
```python
s = "Hello World"
l = s.lower()
l = s.upper()
```

**VimScript:**
```vim
let s = "Hello World"
let l = s->tolower()
let l = s->toupper()
```

*Help:* [tolower()](https://vimhelp.org/eval.txt.html#tolower%28%29), [toupper()](https://vimhelp.org/eval.txt.html#toupper%28%29)

### Replace a substring
**Python:**
```python
s = "Hello World"
s2 = s.replace("Hello", "New")
```

**VimScript:**
```vim
let s = "Hello World"
let s2 = s->substitute("Hello", "New", 'g')
```

*Help:* [substitute()](https://vimhelp.org/eval.txt.html#substitute%28%29)

### Split a string
**Python:**
```python
s = "a:b:c"
s2 = s.split(":")
```

**VimScript:**
```vim
let s = "a:b:c"
let s2 = s->split(":")
```

*Help:* [split()](https://vimhelp.org/eval.txt.html#split%28%29), [join()](https://vimhelp.org/eval.txt.html#join%28%29),

### Stripping leading and trailing whitespace from a string
**Python:**
```python
s = "  vim  "
s2 = s.strip()
```

**VimScript:**
```vim
let s = "  vim  "
let s2 = s->trim()
```

*Help:* [trim()](https://vimhelp.org/eval.txt.html#trim%28%29)

### Checking whether a string contains specific type of characters
**Python:**
```python
s = "text"
if s.isalnum():
    print("Contains only alphanumeric characters")
if s.isalpha():
    print("Contains only alphabetic characters")
if s.isdigit():
    print("Contains only digits")
if s.isspace():
    print("Contains only whitespace characters")
if s.isupper():
    print("Contains only uppercase characters")
if s.islower():
    print("Contains only lowercase characters")
```

**VimScript:**
```vim
let s = "text"
if s =~ '^[:alnum:]\+'
    echo "Contains only alphanumeric characters"
endif
if s =~ '^\a\+$'
    echo "Contains only alphabetic characters"
endif
if s =~ '^\d\+$'
    echo "Contains only digits"
endif
if s =~ '^\s\+$'
    echo "Contains only whitespace characters"
endif
if s =~ '^\u\+$'
    echo "Contains only uppercase characters"
endif
if s =~ '^\l\+$'
    echo "Contains only lowercase characters"
endif
```

*Help:* [/collection](https://vimhelp.org/pattern.txt.html#%2fcollection)

## Data type conversion to string

**Python:**
```python
s = str(268)
s = str(22.7)
s = str([1, 2, 3])
s = str({'a' : 1, 'b' : 2})
```

**VimScript:**
```vim
let s = string(268)
let s = string(22.7)
let s = string([1, 2, 3])
let s = string({'a' : 1, 'b' : 2})
```

*Help:* [string()](https://vimhelp.org/eval.txt.html#string%28%29)

## Evaluating a string

**Python:**
```python
x = 10
y = eval("x * 2")
print(y)
n = eval("min([4, 3, 5])")
```

**VimScript:**
```vim
let x = 10
let y = eval("x * 2")
echo y
let n = eval("min([4, 3, 5])")
```

*Help:* [eval()](https://vimhelp.org/eval.txt.html#eval%28%29)

## Executing commands in a string

**Python:**
```python
exec("for i in range(5):\n    print(i)\n")
```

**VimScript:**
```vim
execute "for i in range(5)\necho i\nendfor"
```

*Help:* [:execute](https://vimhelp.org/eval.txt.html#:execute)

------------------------------------------------------------------------------

## List

### Creating a List

**Python:**
```python
l = [1, 2, 3, 4]
```

**VimScript:**
```vim
let l = [1, 2, 3, 4]
```

*Help:* [List](https://vimhelp.org/eval.txt.html#List)

### Accessing a List element

**Python:**
```python
l = [1, 2, 3, 4]
v1 = l[2]
v2 = l[-2]
```

**VimScript:**
```vim
let l = [1, 2, 3, 4]
let v1 = l[2]
let v2 = l[-2]
```

*Help:* [list-index](https://vimhelp.org/eval.txt.html#list-index)

### Changing the value of a List element

**Python:**
```python
l = [1, 2, 3, 4]
l[3] = 5
```

**VimScript:**
```vim
let l = [1, 2, 3, 4]
let l[3] = 5
```

*Help:* [list-modification](https://vimhelp.org/eval.txt.html#list-modification)

### Adding an item to a List

**Python:**
```python
l = []
l.append(5)
l += [6, 7]
```

**VimScript:**
```vim
let l = []
call add(l, 5)
let l += [5, 6]
```

*Help:* [add()](https://vimhelp.org/eval.txt.html#add%28%29)

### Extending a List using a List

**Python:**
```python
l = []
l.extend([2, 3])
l += [6, 7]
```

**VimScript:**
```vim
let l = []
call extend(l, [2, 3])
let l += [6, 7]
```

*Help:* [extend()](https://vimhelp.org/eval.txt.html#extend%28%29)

### Inserting an item in a List

**Python:**
```python
l = [1, 3]
l.insert(1, 2)
```

**VimScript:**
```vim
let l = [1, 3]
call insert(l, 2, 1)
```

*Help:* [insert()](https://vimhelp.org/eval.txt.html#insert%28%29)

### Removing an item from a List

**Python:**
```python
l = [4, 5, 6]
l.remove(5)
del l[0]
```

**VimScript:**
```vim
let l = [4, 5, 6]
call remove(l, index(l, 5))
unlet l[0]
```

*Help:* [remove()](https://vimhelp.org/eval.txt.html#remove%28%29), [:unlet](https://vimhelp.org/eval.txt.html#%3aunlet)

### Removing the last element from a List

**Python:**
```python
l = [1, 2, 3]
v = l.pop()
```

**VimScript:**
```vim
let l = [1, 2, 3]
let v = l->remove(-1)
```

*Help:* [remove()](https://vimhelp.org/eval.txt.html#remove%28%29)

### Find the index of an item in a List

**Python:**
```python
l = [1, 2, 3]
x = l.index(2)
```

**VimScript:**
```vim
let l = [1, 2, 3]
let x = l->index(2)
```

*Help:* [index()](https://vimhelp.org/eval.txt.html#index%28%29)

### List slices

In Python, when using an index range to specify a series of items in a List, the item at the end index is not included. In Vim, the item at the end index is included.

**Python:**
```python
l = [1, 2, 3, 4]
m = l[1:3]
m = l[2:]
```

**VimScript:**
```vim
let l = [1, 2, 3, 4]
let m = l[1:3]
let m = l[2:]
```

*Help:* [sublist](https://vimhelp.org/eval.txt.html#sublist)

### List Concatenation

**Python:**
```python
l = [1, 2] + [3 ,4]
```

**VimScript:**
```vim
let l = [1, 2] + [3 ,4]
```

*Help:* [list-index](https://vimhelp.org/eval.txt.html#list-index)

### Adding multiple items to a List using repetition

**Python:**
```python
l = ['vim'] * 4
```

**VimScript:**
```vim
let l = ['vim']->repeat(4)
```

*Help:* [repeat()](https://vimhelp.org/eval.txt.html#repeat%28%29)

### Count the number of occurrences of an item in a List

**Python:**
```python
l = [2, 4, 4, 5]
x = l.count(4)
```

**VimScript:**
```vim
let l = [2, 4, 4, 5]
let x = l->count(2)
```

*Help:* [count()](https://vimhelp.org/eval.txt.html#count%28%29)

### Finding the List length

**Python:**
```python
l = ['a', 'b', 'c']
n = len(l)
```

**VimScript:**
```vim
let l = ['a', 'b', 'c']
let n = l->len()
```

*Help:* [len()](https://vimhelp.org/eval.txt.html#len%28%29)

### Sort a List

**Python:**
```python
l = [3, 2, 1]
l.sort()
```

**VimScript:**
```vim
let l = [3, 2, 1]
call sort(l)
```

*Help:* [sort()](https://vimhelp.org/eval.txt.html#sort%28%29)

### Reverse a List

**Python:**
```python
l = [1, 2, 3]
l.reverse()
```

**VimScript:**
```vim
let l = [1, 2, 3]
call reverse(l)
```

*Help:* [reverse()](https://vimhelp.org/eval.txt.html#reverse%28%29)

### Copy a List

**Python:**
```python
l = [3, 2, 1]
l2 = l.copy()
```

**VimScript:**
```vim
let l = [3, 2, 1]
let l2 = l->copy()
```

*Help:* [copy()](https://vimhelp.org/eval.txt.html#copy%28%29)

### Empty a List

**Python:**
```python
l = [3, 2, 1]
l.clear()
```

**VimScript:**
```vim
let l = [3, 2, 1]
unlet l[:]
```

*Help:* [:unlet](https://vimhelp.org/eval.txt.html#%3aunlet)

### Comparing two Lists

**Python:**
```python
l1 = [1, 2]
l2 = [1, 2]
if l1 == l2:
    print("Lists are equal")
```

**VimScript:**
```vim
let l1 = [1, 2]
let l2 = [1, 2]
if l1 == l2
    echo "Lists are equal"
endif
```

*Help:* [list-identity](https://vimhelp.org/eval.txt.html#list-identity)

### Filter selected elements from a List

**Python:**
```python
odd = list(filter(lambda x: x % 2, range(10)))
odd = [x for x in range(10) if x % 2]
```

**VimScript:**
```vim
let odd = filter(range(10), {idx, v -> v % 2})
```

*Help:* [filter()](https://vimhelp.org/eval.txt.html#filter%28%29)

### Map List elements

**Python:**
```python
num_str = list(map(lambda x: str(x), range(10)))
num_str = [str(x) for x in range(10)]
```

**VimScript:**
```vim
let num_str = map(range(10), {idx, v -> string(v)})
```

*Help:* [map()](https://vimhelp.org/eval.txt.html#map%28%29)

### Finding the max/min value in a List

**Python:**
```python
n = max([3, 10, 8])
n = min([3, 10, 8])
```

**VimScript:**
```vim
let n = max([3, 10, 8])
let n = min([3, 10, 8])
```

*Help:* [max()](https://vimhelp.org/eval.txt.html#max%28%29), [min()](https://vimhelp.org/eval.txt.html#min%28%29)

### Converting a List to a string

**Python:**
```python
s = str([3, 5, 7])
```

**VimScript:**
```vim
let s = string([3, 5, 7])
```

*Help:* [string()](https://vimhelp.org/eval.txt.html#string%28%29)

------------------------------------------------------------------------------

## Dictionary
### Creating a Dict
**Python:**
```python
d = {'red' : 10, 'blue' : 20}
x = {}
```

**VimScript:**
```vim
let d = {'red' : 10, 'blue' : 20}
let d = #{red : 10, blue : 20}
let x = {}
```

*Help:* [Dict](https://vimhelp.org/eval.txt.html#Dict)

### Retrieving the value of a Dict item
**Python:**
```python
d = {'red' : 10, 'blue' : 20}
x = d['red']
```

**VimScript:**
```vim
let d = #{red : 10, blue : 20}
let x = d['red']
let x = d.red
```

*Help:* [dict](https://vimhelp.org/eval.txt.html#dict)

### Changing the value of a Dict item
**Python:**
```python
d = {'red' : 10, 'blue' : 20}
d['red'] = 15
```

**VimScript:**
```vim
let d = #{red : 10, blue : 20}
let d.red = 15
```

*Help:* [dict-modification](https://vimhelp.org/eval.txt.html#dict-modification)

### Accessing a Dict item
**Python:**
```python
d = {'red' : 10, 'blue' : 20}
v = d.get('red')
```

**VimScript:**
```vim
let d = {'red' : 10, 'blue' : 20}
let v = get(d, 'red')
```

*Help:* [get()](https://vimhelp.org/eval.txt.html#get%28%29)

### Adding a new Dict item
**Python:**
```python
d = {'red' : 10, 'blue' : 20}
d['green'] = 30
```

**VimScript:**
```vim
let d = {'red' : 10, 'blue' : 20}
let d.green = 30
```

*Help:* [dict-modification](https://vimhelp.org/eval.txt.html#dict-modification)

### Removing a Dict item
**Python:**
```python
d = {'red' : 10, 'blue' : 20}
d.pop('red')
```

**VimScript:**
```vim
let d = {'red' : 10, 'blue' : 20}
call remove(d, 'red')
```

*Help:* [remove()](https://vimhelp.org/eval.txt.html#remove%28%29),

### Clearing all the  items from a Dict
**Python:**
```python
d = {'red' : 10, 'blue' : 20}
d.clear()
```

**VimScript:**
```vim
let d = {'red' : 10, 'blue' : 20}
call filter(d, "0")
```

*Help:* [dict-modification](https://vimhelp.org/eval.txt.html#dict-modification)

### Getting the size of a Dict
**Python:**
```python
d = {'red' : 10, 'blue' : 20}
n = len(d)
```

**VimScript:**
```vim
let d = {'red' : 10, 'blue' : 20}
let n = d->len()
```

*Help:* [len()](https://vimhelp.org/eval.txt.html#len%28%29)

### Checking Dict membership
**Python:**
```python
d = {'red' : 10, 'blue' : 20}
if 'red' in d:
    print("found red key")
```

**VimScript:**
```vim
let d = {'red' : 10, 'blue' : 20}
if d->has_key('red')
    echo "found red key"
endif
```

*Help:* [has_key()](https://vimhelp.org/eval.txt.html#has_key%28%29)

### Iterating through all the keys in a Dict
**Python:**
```python
d = {'red' : 10, 'blue' : 20}
for k in d:
    print(k)
for k in d:
    print(d[k])
```

**VimScript:**
```vim
let d = {'red' : 10, 'blue' : 20}
for k in keys(d)
    echo k
endfor
for k in d->keys()
    echo d[k]
endfor
```

*Help:* [keys()](https://vimhelp.org/eval.txt.html#keys%28%29)

### Iterating through all the values in a Dict
**Python:**
```python
d = {'red' : 10, 'blue' : 20}
for v in d.values():
    print(v)
```

**VimScript:**
```vim
let d = {'red' : 10, 'blue' : 20}
for v in d->values()
    echo v
endfor
```

*Help:* [values()](https://vimhelp.org/eval.txt.html#values%28%29)

### Iterating through all the key, value pairs in a Dict
**Python:**
```python
d = {'red' : 10, 'blue' : 20}
for k, v in d.items():
    print(k, v)
```

**VimScript:**
```vim
let d = {'red' : 10, 'blue' : 20}
for [k, v] in d->items()
    echo k v
endfor
```

*Help:* [items()](https://vimhelp.org/eval.txt.html#items%28%29)

### Copying a Dict
**Python:**
```python
d = {'red' : 10, 'blue' : 20}
new_d = d.copy()
```

**VimScript:**
```vim
let d = {'red' : 10, 'blue' : 20}
let new_d = d->copy()
```

*Help:* [copy()](https://vimhelp.org/eval.txt.html#copy%28%29)

### Converting a Dict to a string
**Python:**
```python
d = str({'a' : 1, 'b' : 2})
```

**VimScript:**
```vim
let d = string({'a' : 1, 'b' : 2})
```

*Help:* [string()](https://vimhelp.org/eval.txt.html#string%28%29)

### Comparing two Dicts

**Python:**
```python
d1 = {'a' : 10, 'b' : 20}
d2 = {'a' : 10, 'b' : 20}
if d1 == d2:
    print("Dicts are equal")
```

**VimScript:**
```vim
let d1 = {'a' : 10, 'b' : 20}
let d2 = {'a' : 10, 'b' : 20}
if d1 == d2
    echo "Dicts are equal"
endif
```

*Help:* [dict-identity](https://vimhelp.org/eval.txt.html#dict-identity)

------------------------------------------------------------------------------

## If statement

### Basic If statement

**Python:**
```python
if a > b:
    print("a is greater than b")
```

**VimScript:**
```vim
if a > b
    echo "a is greater than b"
endif
```

*Help:* [:if](https://vimhelp.org/eval.txt.html#%3aif)

### If-else statement

**Python:**
```python
if a > b:
    print("a is greater than b")
else:
    print("a is less than or equal to b")
```

**VimScript:**
```vim
if a > b
    echo "a is greater than b"
else
    echo "a is less than or equal to b"
endif
```

*Help:* [:else](https://vimhelp.org/eval.txt.html#%3aelse)

### If-elseif statement

**Python:**
```python
if a > b:
    print("a is greater than b")
elif a < b:
    print("a is less than b")
else:
    print("a is equal to b")
```

**VimScript:**
```vim
if a > b
    echo "a is greater than b"
elseif a < b
    echo "a is less than b"
else
    echo "a is equal to b"
endif
```

*Help:* [:elseif](https://vimhelp.org/eval.txt.html#%3aelseif)

### Checking multiple conditions

**Python:**
```python
if a > b and (a > c or a > d):
    print "a is greater than b and greater than c or d"
```

**VimScript:**
```vim
if a > b && (a > c || a > d)
    echo "a is greater than b and greater than c or d"
endif
```

*Help:* [expr2](https://vimhelp.org/eval.txt.html#expr2)

### Nested If statements
**Python:**
```python
if status == True:
    if a >= 1:
	print("Nested if")
```

**VimScript:**
```vim
if status == v:true
    if a >= 1
	echo "Nested if"
    endif
endif
```

*Help:* [:if](https://vimhelp.org/eval.txt.html#%3aif)

------------------------------------------------------------------------------

## For Loop
**Python:**
```python
for i in range(5) :
    print(i)
```

**VimScript:**
```vim
for i in range(5)
    echo i
endfor
```

*Help:* [:for](https://vimhelp.org/eval.txt.html#%3afor)

### Breaking out of a For loop
**Python:**
```python
for i in ['a', 'b', 'c']:
    if i == 'b':
        break
    print(i)
```

**VimScript:**
```vim
for i in ['a', 'b', 'c']
    if i == 'b'
        break
    endif
    echo i
endfor
```

*Help:* [:break](https://vimhelp.org/eval.txt.html#%3abreak)

### Continuing a For loop
**Python:**
```python
for i in ['a', 'b', 'c']:
    if i == 'b':
        continue
    print(i)
```

**VimScript:**
```vim
for i in ['a', 'b', 'c']
    if i == 'b'
        continue
    endif
    echo i
endfor
```

*Help:* [:continue](https://vimhelp.org/eval.txt.html#%3acontinue)

### Nested For Loops
**Python:**
```python
for i in range(10):
    for j in range(10):
	print(str(i) + 'x' + str(j) + '=' + str(i * j))
```

**VimScript:**
```vim
for i in range(4)
    for j in range(4)
	echo i .. 'x' .. j .. '=' .. i * j
    endfor
endfor
```

*Help:* [:for](https://vimhelp.org/eval.txt.html#%3afor)

------------------------------------------------------------------------------

## While Loop

**Python:**
```python
i = 1
while i <= 5 :
   print(i)
   i += 1
```

**VimScript:**
```vim
let i = 1
while i <= 5
    echo i
    let i += 1
endwhile
```

*Help:* [:while](https://vimhelp.org/eval.txt.html#%3awhile)

------------------------------------------------------------------------------

## Comments

**Python:**
```python
# This is a python comment
i = 0    # First iteration
```

**VimScript:**
```vim
" This is a Vimscript comment
let i = 0    " First iteration
```

*Help:* [:comment](https://vimhelp.org/cmdline.txt.html#%3acomment)

------------------------------------------------------------------------------

## Functions

The names of global functions in Vim must start with an uppercase letter.
The examples in this document use the "function" and "endfunction" keywords for
defining a function. But these can be abbreviated as "func" and "endfunc".

When a function encounters an error, it will continue to execute the rest of the function unless the "abort" argument is specified when defining the function. So it is recommended to specify the "abort" keyword at the end of the "function" line. To simplify the example code, this keyword is not used in this guide.

### Defining a Function

**Python:**
```python
def Min(x, y):
    return x if < y else y

print(Min(6, 3)
```

**VimScript:**
```vim
function Min(x, y) abort
    return a:x < a:y ? a:x : a:y
endfunction

echo Min(6, 3)
```

*Help:* [user-functions](https://vimhelp.org/eval.txt.html#user-functions)

### Calling a Function

**Python:**
```python
def EchoValue(v):
    print(v)

EchoValue(100)
```

**VimScript:**
```vim
function EchoValue(v)
    echo a:v
endfunction

call EchoValue(100)
```

*Help:* [:call](https://vimhelp.org/eval.txt.html#%3acall)

### Function return value

**Python:**
```python
def Sum(a, b):
    return a + b

s = Sum(10, 20)
```

**VimScript:**
```vim
function Sum(a, b)
    return a:a + a:b
endfunction

let s = Sum(10, 20)
```

*Help:* [:return](https://vimhelp.org/eval.txt.html#%3areturn)

### Pass by reference

**Python:**
```python
def AddValues(l):
    l.extend([1, 2, 3, 4])
```

**VimScript:**
```vim
function AddValues(l)
    call extend(a:l, [1, 2, 3, 4])
endfunction
```

*Help:* [function-argument](https://vimhelp.org/eval.txt.html#function-argument)

### Variable number of arguments

**Python:**
```python
def Sum(v1, *args):
    sum = v1
    for i in *args:
	sum += i
    return sum
```

**VimScript:**
```vim
function Sum(v1, ...)
    let sum = a:v1
    for i in a:000
	let sum +=i
    endfor
    return sum
endfunction
let s1 = Sum(10, 20, 30, 40)
let s1 = Sum(10)
```

*Help:* [a:000](https://vimhelp.org/eval.txt.html#a%3a000)

### Default value for arguments

**Python:**
```python
def Powerof(base, exp = 2):
    return base ** exp
```

**VimScript:**
```vim
function PowerOf(base, exp = 2)
    return float2nr(pow(a:base, a:exp))
endfunction
let val = PowerOf(4)
let val = PowerOf(4, 3)
```

*Help:* [optional-function-argument](https://vimhelp.org/eval.txt.html#optional-function-argument)

### Accessing global variables

**Python:**
```python
counter = 1
def Incr():
    global counter
    counter += 1
```

**VimScript:**
```vim
let counter = 1
function Incr()
    let g:counter += 1
endfunction
cal Incr()
```

*Help:* [global-variable](https://vimhelp.org/eval.txt.html#global-variable)

### Function reference

**Python:**
```python
def Foo():
    print("Foo")
Bar = Foo
Bar()
```

**VimScript:**
```vim
function Foo()
    echo "Foo"
endfunction
let Bar = function("Foo")
call Bar()
```

*Help:* [Funcref](https://vimhelp.org/eval.txt.html#Funcref)

------------------------------------------------------------------------------

## Lambda Function

**Python:**
```python
F = lambda x , y: x - y
print(F(5,2))
```

**VimScript:**
```vim
let F = {x, y -> x - y}
echo F(5,2)
```

*Help:* [lambda](https://vimhelp.org/eval.txt.html#lambda)

------------------------------------------------------------------------------

## Partial Function

**Python:**
```python
import functools
def Mylog(subsys, msg):
    print("%s: %s" % (subsys, msg))

ErrLog = functools.partial(Mylog, 'ERR')
ErrLog("Failed to open file")
```

**VimScript:**
```vim
function Mylog(subsys, msg)
    echo printf("%s: %s", a:subsys, a:msg)
endfunction

let ErrLog = function('Mylog', ['ERR'])
call ErrLog("Failed to open file")
```

*Help:* [Partial](https://vimhelp.org/eval.txt.html#Partial)

------------------------------------------------------------------------------

## Closures

### Closure with a lambda function

**Python:**
```python
def foo(arg):
  i = 3
  return lambda x: x + i - arg

bar = foo(4)
print(bar(6))
```

**VimScript:**
```vim
function Foo(arg)
  let i = 3
  return {x -> x + i - a:arg}
endfunction

let Bar = Foo(4)
echo Bar(6)
```

*Help:* [closure](https://vimhelp.org/eval.txt.html#closure)

### Closure with a function reference

**Python:**
```python
def Foo(base):
    def Bar(val):
	return base + val
    return Bar

F = Foo(10)
print(F(2))
F = Foo(20)
print(F(2))
```

**VimScript:**
```vim
function Foo(base)
    function Bar(val) closure
	return a:base + a:val
    endfunction
    return funcref('Bar')
endfunction

let F = Foo(10)
echo F(2)
let F = Foo(20)
echo F(2)
```

*Help:* [func-closure](https://vimhelp.org/eval.txt.html#%3Afunc-closure)

------------------------------------------------------------------------------

# Classes

## Defining a class

**Python:**
```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def getX(self):
        return self.x

    def getY(self):
        return self.y

    def setX(self, x):
        self.x = x

    def setY(self, y):
        self.y = y

    def Print(self):
        print("Pt = (" + str(self.x) + ", " + str(self.y) + ")")

pt = Point(10, 20)
pt.setX(40)
pt.setY(50)
pt.Print()
```

**VimScript:**
```vim
function s:new(x, y) dict
  let newpt = copy(self)
  let newpt.x = a:x
  let newpt.y = a:y
  return newpt
endfunction

function s:getX() dict
  return self.x
endfunction

function s:getY() dict
  return self.y
endfunction

function s:setX(x) dict
  let self.x = a:x
endfunction

function s:setY(y) dict
  let self.y = a:y
endfunction

function s:Print() dict
  echo "Pt = (" .. self.x .. ", " .. self.y .. ")"
endfunction

let Point = {}
let Point.new = function("s:new")
let Point.getX = function("s:getX")
let Point.getY = function("s:getY")
let Point.setX = function("s:setX")
let Point.setY = function("s:setY")
let Point.Print = function("s:Print")

let p = Point.new(10, 20)
call p.setX(40)
call p.setY(50)
call p.Print()
```

*Help:* [Dictionary-function](https://vimhelp.org/eval.txt.html#Dictionary-function), [numbered-function](https://vimhelp.org/eval.txt.html#numbered-function), [:func-dict](https://vimhelp.org/eval.txt.html#%3afunc-dict)

------------------------------------------------------------------------------

## Exception Handling

### Basic exception handling

**Python:**
```python
try:
    f = open('buf.java', 'r')
    lines = f.readlines()
    f.close()
except IOError:
    print("Failed to open file")
```

**VimScript:**
```vim
try
    let l = readfile('buf.java')
catch /E484:/
    echo "Failed to read file"
endtry
```

*Help:* [exception-handling](https://vimhelp.org/eval.txt.html#exception-handling)

### Catching all exceptions

**Python:**
```python
try:
    f = open('buf.java', 'r')
    lines = f.readlines()
    f.close()
except Exception as e:
    print("Caught " + str(e))
```

**VimScript:**
```vim
try
    let l = readfile('buf.java')
catch
    echo "Caught " .. v:exception
endtry
```

*Help:* [catch-errors](https://vimhelp.org/eval.txt.html#catch-errors)

### Executing code after a try block (finally)

**Python:**
```python
try:
    f = open('buf.java', 'r')
    lines = f.readlines()
    f.close()
finally:
    print("executing code in finally block")
```

**VimScript:**
```vim
try
    let l = readfile('buf.java')
finally
    echo "executing code in finally block"
endtry
```

*Help:* [try-finally](https://vimhelp.org/eval.txt.html#try-finally)

### Raising a custom exception

**Python:**
```python
try:
    raise Exception('MyException')
except Exception as e:
    if str(e) == 'MyException':
	print("Caught MyException")
finally:
    print("Finally block")
```

**VimScript:**
```vim
try
    throw 'MyException'
catch /MyException/
    echo "Caught MyException"
finally
    echo "Finally block"
endtry
```

*Help:* [throw-catch](https://vimhelp.org/eval.txt.html#throw-catch)

------------------------------------------------------------------------------

## Formatted Output

**Python:**
```python
name = "John"
id = 1001
print(f"Name: {name}, ID: {id}")
print("Name: {}, ID: {}".format(name, id))
print("Name: %s, ID: %d" % (name, id))
```

**VimScript:**
```vim
let name = "John"
let id = 1001
echo printf("Name: %s, ID: %d", name, id)
```

*Help:* [printf()](https://vimhelp.org/eval.txt.html#printf%28%29)

------------------------------------------------------------------------------

## Line Continuation

**Python:**
```python
a = 1 + 2 + 3 + \
      4 + 5 + 6
```

**VimScript:**
```vim
let a = 1 + 2 + 3 +
      \ 4 + 5 + 6
```

*Help:* [line-continuation](https://vimhelp.org/eval.txt.html#line-continuation)

------------------------------------------------------------------------------

## File Operations

### Reading all the lines from a file

Vim has a function to read the entire file but doesn't have a function to read a file one line at a time.

**Python:**
```python
with open('myfile.txt', 'r') as f:
    lines = f.readlines()
```

**VimScript:**
```vim
let lines = readfile("myfile.txt")
```

*Help:* [readfile()](https://vimhelp.org/eval.txt.html#readfile%28%29)

### Writing lines to a file
**Python:**
```python
lines = ['line1', 'line2']
with open('myfile.txt', 'w') as fh:
    fh.writelines("\n".join(lines))
```

**VimScript:**
```vim
call writefile(['line1', 'line2'], 'myfile.txt')
```

*Help:* [writefile()](https://vimhelp.org/eval.txt.html#writefile%28%29)

### Appending lines to a file
**Python:**
```python
lines = ["line3\n", "line4\n"]
with open('myfile.txt', 'a') as fh:
    fh.writelines(lines)
```

**VimScript:**
```vim
call writefile(['line3', 'line4'], 'myfile.txt', 'a')
```

*Help:* [writefile()](https://vimhelp.org/eval.txt.html#writefile%28%29)

### Checking whether a file exists
**Python:**
```python
import os.path
if os.path.isfile('myfile.txt'):
    print("File exists")
```

**VimScript:**
```vim
if filereadable('myfile.txt')
    echo "File is readable"
endif
```

*Help:* [filereadable()](https://vimhelp.org/eval.txt.html#filereadable%28%29)

### Deleting a file
**Python:**
```python
import os
os.remove('myfile.txt')
```

**VimScript:**
```vim
call delete('myfile.txt')
```

*Help:* [remove()](https://vimhelp.org/eval.txt.html#remove%28%29)

### Renaming a file
**Python:**
```python
import os
os.rename('myfile.txt', 'somefile.txt)
```

**VimScript:**
```vim
call rename('myfile.txt', 'somefile.txt')
```

*Help:* [rename()](https://vimhelp.org/eval.txt.html#rename%28%29)

### Getting the size of a file
**Python:**
```python
import os
sz = os.path.getsize('move.py')
```

**VimScript:**
```vim
let sz = getfsize('move.py')
```

*Help:* [getfsize()](https://vimhelp.org/eval.txt.html#getfsize%28%29)

------------------------------------------------------------------------------

## Directory Operations

### Creating a directory
**Python:**
```python
os.mkdir('somedir')
```

**VimScript:**
```vim
call mkdir('somedir')
```

*Help:* [mkdir()](https://vimhelp.org/eval.txt.html#mkdir%28%29)

### Changing to a directory
**Python:**
```python
os.chdir('someotherdir')
```

**VimScript:**
```vim
call chdir('someotherdir')
```

*Help:* [chdir()](https://vimhelp.org/eval.txt.html#chdir%28%29)

### Getting the current directory
**Python:**
```python
dir = os.getcwd()
```

**VimScript:**
```vim
let dir = getcwd()
```

*Help:* [getcwd()](https://vimhelp.org/eval.txt.html#getcwd%28%29)

### Deleting a directory
**Python:**
```python
os.rmdir('somedir')
```

**VimScript:**
```vim
call delete('somedir', 'd')
```

*Help:* [delete()](https://vimhelp.org/eval.txt.html#delete%28%29)

------------------------------------------------------------------------------

## Random numbers

### Generating a random number
**Python:**
```python
import random
r = random.randint(0, 2147483647)
```

**VimScript:**
```vim
let r = rand()
```

*Help:* [rand()](https://vimhelp.org/eval.txt.html#rand%28%29)

### Generating a random number from a seed
**Python:**
```python
import random
random.seed()
r = random.randint(0, 2147483647)
print(r)
```

**VimScript:**
```vim
let seed = srand()
let r = rand(seed)
```

*Help:* [srand()](https://vimhelp.org/eval.txt.html#srand%28%29)

------------------------------------------------------------------------------

## Mathematical functions

**Python:**
```python
import math
f = math.ceil(1.2)
f = math.fabs(-10)
f = math.floor(1.4)
f = math.fmod(4, 3)
f = math.trunc(1.3)
f = math.exp(2)
f = math.log(12)
f = math.log10(100)
f = math.pow(2, 3)
f = math.sqrt(9)
f = math.cos(4)
f = math.sin(4)
f = math.tan(4)
f = math.cosh(4)
f = math.sinh(4)
f = math.tanh(4)
f = math.acos(0.8)
f = math.asin(0.8)
f = math.atan(0.8)
f = math.atan2(0.4, 0.8)

```

**VimScript:**
```vim
let f = ceil(1.2)
let f = abs(-10)
let f = floor(1.4)
let f = fmod(4, 3)
let f = trunc(1.3)
let f = exp(2)
let f = log(12)
let f = log10(100)
let f = pow(2, 3)
let f = sqrt(9)
let f = cos(4)
let f = sin(4)
let f = tan(4)
let f = cosh(4)
let f = sinh(4)
let f = tanh(4)
let f = acos(0.8)
let f = asin(0.8)
let f = atan(0.8)
let f = atan2(0.4, 0.8)
```

*Help:* [ceil()](https://vimhelp.org/eval.txt.html#ceil%28%29), [abs()](https://vimhelp.org/eval.txt.html#abs%28%29), [floor()](https://vimhelp.org/eval.txt.html#floor%28%29), [fmod()](https://vimhelp.org/eval.txt.html#fmod%28%29), [trunc()](https://vimhelp.org/eval.txt.html#trunc%28%29), [exp()](https://vimhelp.org/eval.txt.html#exp%28%29), [log()](https://vimhelp.org/eval.txt.html#log%28%29), [log10()](https://vimhelp.org/eval.txt.html#log10%28%29), [pow()](https://vimhelp.org/eval.txt.html#pow%28%29), [sqrt()](https://vimhelp.org/eval.txt.html#sqrt%28%29), [cos()](https://vimhelp.org/eval.txt.html#cos%28%29), [sin()](https://vimhelp.org/eval.txt.html#sin%28%29), [tan()](https://vimhelp.org/eval.txt.html#tan%28%29), [cosh()](https://vimhelp.org/eval.txt.html#cosh%28%29), [sinh()](https://vimhelp.org/eval.txt.html#sinh%28%29), [tanh()](https://vimhelp.org/eval.txt.html#tanh%28%29), [acos()](https://vimhelp.org/eval.txt.html#acos%28%29), [asin()](https://vimhelp.org/eval.txt.html#asin%28%29), [atan()](https://vimhelp.org/eval.txt.html#atan%28%29), [atan2()](https://vimhelp.org/eval.txt.html#atan2%28%29)

------------------------------------------------------------------------------

## Date/Time functions

### Get current date and time

**Python:**
```python
from datetime import date
d = date.today()
print d.strftime("%c")
```

**VimScript:**
```vim
echo strftime("%c")
```

*Help:* [strftime()](https://vimhelp.org/eval.txt.html#strftime%28%29)

### Parse a date/time string

**Python:**
```python
from datetime import datetime
print(datetime.strptime("1997 Apr 27 11:49:23", "%Y %b %d %X"))
```

**VimScript:**
```vim
echo strptime("%Y %b %d %X", "1997 Apr 27 11:49:23")
```

*Help:* [strptime()](https://vimhelp.org/eval.txt.html#strptime%28%29)

### Getting the time in seconds since epoch

**Python:**
```python
import time
print int(time.time())
```

**VimScript:**
```vim
echo localtime()
```

*Help:* [localtime()](https://vimhelp.org/eval.txt.html#localtime%28%29)

------------------------------------------------------------------------------

## External commands

### Getting the output of an external command as a string

**Python:**
```python
import subprocess
procObj = subprocess.Popen('grep class *.java',
			stdout=subprocess.PIPE,
			shell=True)
lines, err = procObj.communicate()
print(lines)
print("Error = " + str(procObj.returncode))
```

**VimScript:**
```vim
let lines = system('grep class *.java')
echo lines
echo "Error = " .. v:shell_error
```

*Help:* [system()](https://vimhelp.org/eval.txt.html#system%28%29), [v:shell_error](https://vimhelp.org/eval.txt.html#v%3ashell_error)

### Splitting the output of an external command into lines

**Python:**
```python
import subprocess
procObj = subprocess.Popen('grep class *.java',
			stdout=subprocess.PIPE,
			shell=True)
lines, err = procObj.communicate()
print("Number of matches = " + str(len(lines.split("\n"))))
```

**VimScript:**
```vim
let lines = systemlist('grep class *.java')
echo "Number of matches = " .. len(lines)
```

*Help:* [systemlist()](https://vimhelp.org/eval.txt.html#systemlist%28%29)

### Sending input to an external command and getting the output

**Python:**
```python
import subprocess
procObj = subprocess.Popen('wc',
			stdout=subprocess.PIPE,
			stdin=subprocess.PIPE,
			shell=True)
lines, err = procObj.communicate("one\ntwo\n")
print(lines)
print("Error = " + str(procObj.returncode))
```

**VimScript:**
```vim
let lines = system('wc', "one\ntwo\n")
echo lines
echo "Error = " .. v:shell_error
```

*Help:* [system()](https://vimhelp.org/eval.txt.html#system%28%29)

------------------------------------------------------------------------------

## Environment Variables

### Getting the value of an environment variable

**Python:**
```python
import os
h = os.environ.get('HOME', '')
if h == '':
    print("HOME is not set")
else:
    print("HOME = " + h)
```

**VimScript:**
```vim
let h = getenv('HOME')
if h == v:null
    echo 'HOME is not set'
else
    echo 'HOME = ' .. h
endif

if !exists('$HOME')
    echo 'HOME is not set'
else
    echo 'HOME = ' .. $HOME
endif
```

*Help:* [getenv()](https://vimhelp.org/eval.txt.html#getenv%28%29), [expr-env](https://vimhelp.org/eval.txt.html#expr-env), [exists()](https://vimhelp.org/eval.txt.html#exists%28%29)

### Setting an environment variable

**Python:**
```python
import os
os.environ['FOO'] = "BAR"
```

**VimScript:**
```vim
call setenv('FOO', 'BAR')

let $FOO = 'BAR'
```

*Help:* [setenv()](https://vimhelp.org/eval.txt.html#setenv%28%29), [:let-environment](https://vimhelp.org/eval.txt.html#%3alet-environment)

### Removing an environment variable

**Python:**
```python
import os
del os.environ['FOO']
```

**VimScript:**
```vim
call setenv('FOO', v:null)

unlet $FOO
```

*Help:* [setenv()](https://vimhelp.org/eval.txt.html#setenv%28%29), [:unlet-environment](https://vimhelp.org/eval.txt.html#%3aunlet-environment)

### Getting all the environment variables

**Python:**
```python
import os
print(os.environ)
```

**VimScript:**
```vim
echo environ()
```

*Help:* [environ()](https://vimhelp.org/eval.txt.html#environ%28%29)

------------------------------------------------------------------------------

## Command-line Arguments

### Displaying the command-line arguments

**Python:**
```python
import sys
print("Number of arguments = " + str(len(sys.argv)))
print("Arguments = " + str(sys.argv))
for arg in sys.argv:
    print(arg)
```

**VimScript:**
```vim
echo "Number of arguments = " .. len(v:argv)
echo "Arguments = " .. string(v:argv)
for arg in v:argv
    echo arg
endfor
```

*Help:* [v:argv](https://vimhelp.org/eval.txt.html#v%3aargv)

------------------------------------------------------------------------------

## Regular Expressions

### Finding whether a pattern matches a string

**Python:**
```python
import re
s = 'Test failed with error E123:'
if re.search(r'E\d+:', s):
    print('Error code found')

s = 'Test successful'
if re.search(r'E\d+:', s) == None:
    print("Test passed")
```

**VimScript:**
```vim
let s = 'Test failed with error E123:'
if s =~# 'E\d\+:'
    echo "Error code found"
endif

let s = 'Test successful'
if s !~# 'E\d\+:'
    echo "Test passed"
endif
```

*Help:* [expr-=~](https://vimhelp.org/eval.txt.html#expr-%3d~), [expr-!~](https://vimhelp.org/eval.txt.html#expr-%21~)

### Finding the beginning or ending index of a pattern in a string

**Python:**
```python
import re
m = re.search(r'\d+', "Abc 123 Def")
if m != None:
    idx = m.start()
    end_idx = m.end()
```

**VimScript:**
```vim
let idx = match("Abc 123 Def", '\d\+')
let end_idx = matchend("Abc 123 Def", '\d\+')

let l = matchstrpos("Abc 123 Def", '\d\+')
echo "start:" l[1] "end:" l[2]
```

*Help:* [match()](https://vimhelp.org/eval.txt.html#match%28%29), [matchend()](https://vimhelp.org/eval.txt.html#matchend%28%29), [matchstrpos()](https://vimhelp.org/eval.txt.html#matchstrpos%28%29)

### Getting matching substring using a pattern

**Python:**
```python
import re
m = re.search(r'\d+', "Abc 123 Def")
if m != None:
    s = m.group(0)
    print s
```

**VimScript:**
```vim
let s = matchstr("Abc 123 Def", '\d\+')
```

*Help:* [matchstr()](https://vimhelp.org/eval.txt.html#matchstr%28%29)

### Getting multiple matches using a pattern

**Python:**
```python
import re
m = re.match(r'(\w+) (\w+) (\w+)', "foo bar baz")
if m != None:
    print("Full match: " + m.group(0))
    print("1: " + m.group(1) + " 2: " + m.group(2) + " 3: " + m.group(3))
```

**VimScript:**
```vim
let list = matchlist("foo bar baz", '\(\w\+\) \(\w\+\) \(\w\+\)')
echo "Full match:" list[0]
echo "1:" list[1] "2:" list[2] "3:" list[3]
```

*Help:* [matchlist()](https://vimhelp.org/eval.txt.html#matchlist%28%29)

### Substituting text using a pattern

**Python:**
```python
import re
s = re.sub(r'bar', r'baz', "foo bar")
print(s)
```

**VimScript:**
```vim
let s = substitute("foo bar", 'bar', 'baz', '')
echo s
```

*Help:* [substitute()](https://vimhelp.org/eval.txt.html#substitute%28%29)

### Using a function to get the replacement string

**Python:**
```python
import re
def Dashrepl(m):
  if m.group(0) == '-':
    return ' '
  else:
    return '-'
s = re.sub('-{1,2}', Dashrepl, 'pro----gram-files')
print(s)
```

**VimScript:**
```vim
function Dashrepl(m)
  if a:m[0] == '-'
    return ' '
  else
    return '-'
  endif
endfunction
let s = substitute("pro----gram-files", '-\{1,2}', function('Dashrepl'), 'g')
echo s
```

*Help:* [substitute()](https://vimhelp.org/eval.txt.html#substitute%28%29)

### Regular expression comparison

Note that the below table contains only the regular expressions that are present in both Python and Vim. There are some minor differences between the behavior of Vim and Python regular expression atoms listed below. For example, in Python the (?i) atom ignores case after the atom. But in Vim, the \c atom ignores case everywhere before and after the atom. Refer to the help pages for these atoms for more information.

What|Python|Vim
----|------|---
single character|  .  |  .
start of string|  ^  |  ^
end of string|  $  |  $
0 or more matches|  *  |  *
1 or more matches|  +  |  \\+
0 or 1 match|  ?  |  \\?
non-greedy match|  \*?  |  \\{-}
fixed matches|  {n}  |  \\{n}
m to n matches|  {m,n}  |  \\{m,n}
m to n non-greedy matches|  {m,n}?  | \\{-m,n}
character class|  [...]  |  [...]
negated character class|  [\^...]  |  [\^...]
range|  [a-z]  |  [a-z]
either-or branch|  \|  | \\\|
capturing group|  (...)  |  \\(...\\)
non-capturing match|  (?:...)  |  \\%(...\\)
positive look-ahead|  (?=...)  |  \\(...\\)\\@=
negative look-ahead|  (?!...)  |  \\(...\\)\\@!
positive look-behind|  (?<=...)  |   \\(...\\)\\@<=
negative look-behind|  (?\<!...)  |  \\(...\\)\\@\<!
start of word|  \\b  |  \\<
end of word|  \\b  |  \\>
digit|  \\d  |  \\d
non-digit|  \\D  |  \\D
whitespace|  \\s  |  \\s
non-whitespace|  \\S  |  \\S
word character|  \\w  |  \\w
non-word character|  \\W  |  \\W
ignore case|  (?i)  |  \\c

*Help:* [pattern](https://vimhelp.org/pattern.txt.html#pattern)

------------------------------------------------------------------------------

## Binary Data

### Storing binary data in a variable

**Python:**
```python
data = bytearray(b'\x12\xF6\xAB\xFF\x49\xC0\x88\x3A\xE2\xC1\x42\xAA')
print(data)
print(data[0:4])
```

**VimScript:**
```vim
let data = 0z12F6ABFF.49C0883A.E2C142AA
echo data
echo data[0:3]
```

*Help:* [blob](https://vimhelp.org/eval.txt.html#blob)

### Manipulating binary data stored in a variable

**Python:**
```python
data = bytearray(b'')
data.append(0xC2)
data += b'\xB3\xF7\xA5'
del data[2]
print(data)
```

**VimScript:**
```vim
let data = 0z
let data[0] = 0xC2
let data += 0zB3F7A5
call remove(data, 2)
echo data
```

*Help:* [blob-index](https://vimhelp.org/eval.txt.html#blob-index), [blob-modification](https://vimhelp.org/eval.txt.html#blob-modification)

### Reading and writing binary data from a file

**Python:**
```python
with open("datafile.bin", "rb") as bin_fh:
    data = bytearray(bin_fh.read())

with open("data2.bin", "wb") as bin_fh:
    bin_fh.write(data)
```

**VimScript:**
```vim
let data = readfile('datafile.bin', 'B')
call writefile(data, 'data2.bin')
```

*Help:* [readfile()](https://vimhelp.org/eval.txt.html#readfile%28%29), [writefile()](https://vimhelp.org/eval.txt.html#writefile%28%29)

