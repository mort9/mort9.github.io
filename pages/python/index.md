---
title: Mort9 Posts
author: Mortie Torabi 
---

# Python

## Useful techniques

#### Environment Variables

```python
print(os.environ['HOME_ADDR']) # get
os.environ['HOME_ADDR']='xyz' # set
```

#### Global Variables

```python
global x # use global inside functions to avoid getting a local variable
```

#### JSON Parsing

[Reading and Writing JSON to a File in Python (stackabuse.com)](https://stackabuse.com/reading-and-writing-json-to-a-file-in-python/)

#### Language Syntax

```python
isApple = True if fruit == 'Apple' else False # One liner if statements

myNewList = [[a,b] for a,b in mainList if a in secondaryList] # Array manipulation based on cond.

list_1 = [['good',100, 20, 0.2],['bad', 10, 0, 0.0],['change', 1, 2, 2]]
list_1 = [item for item in list_1 if item[2] >= 5 or item[3] >= 0.3]
```

#### Program Argument Handling

[python - How to read/process command line arguments? - Stack Overflow](https://stackoverflow.com/questions/1009860/how-to-read-process-command-line-arguments)

#### Saving Variables to Files

```python
sample_list = [1, 2, 3]
file_name = "sample.pkl"

open_file = open(file_name, "wb")
pickle.dump(sample_list, open_file)
open_file.close()

open_file = open(file_name, "rb")
loaded_list = pickle.load(open_file)
open_file.close()

print(loaded_list)
```

#### Converting a List to String

```py
strlist = ' '.join(map(str, list))
```