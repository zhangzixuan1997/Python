Some String Motheds
===================

```python
# Some methods of Python
string.find('e').   return index 
string.split(' '). return list of words 
line.strip(‘.’)
#return the deleted stuff inside ""
```

```python
#Some notes 
#List is mutable
L = [1,2,3]
L+=[4] # normally dont use this because it will copy and operate 
L.append(4) #same function but less storage 
#List.sort funtion 
L.sort()
sorted_L = sorted(L)
#depends on wheter u care about the original list 
index_five = L.index(5)
#if cant find it, it will give you a error 
#but.find will give you a -1 
#Use a loop to find all the indeces 
find_five = [i for i in range(len(L)) if L[i] == 5]
#We cannot stack list methods
L.sort().index(5) 
#nothing returned after the sort function 
```

1)dynamic typing
either mutable or immutable 
2)number, strings and tuples are not immutable 
The keys in dictionary can only be immutable
3) objects are strongly typed. Built in Methods are strong.

```python
#Dictionary Methods 
D = {"Jake":1,"Joe":2}
D.keys()
list(D.keys())
D.values()
list.(D.values())
for num in D.values():
  print(num)
"Jake" in D.keys() #return a boolean
D.get("Jake")#will return the value 
#return "None" if the key is not in the dictionary 
#D[asdf] returns an error
```



Reading and Wrting File
=======================

```python
f = open("NewFile.text","w")
# if it already exists, it will start from a blank 
f.write("Roses are blue\n")
f.write("Violets are red")
f.close()
#Append Funtion
f = open("NewFile.text","a")
f.write("\nOh it is not correct")
f.close()
f.readline
f.readlines
f.readlines.strip("\n").split(" ")
#Writing Variables into the file 
f = open("New.csv","w")
score_list = [83,92,87]
for score in score_list:
  f.write("score")# this will only write strings in 
  f.write("%d\n" %score)
num_cookies = 10 frac_cookies = 10.234
sentence = "I ate %d cookies, %f cookies" %(num_cookies,frac_cookies)
#%d %s %f %0.1f %0.3f
# Relative File Paths 
# For a comma seperated file 
f = open("Min_Wage.csv","r")# For the same location
f.read()
f = open("../Data/Min_Wage.csv","r")# For the former location .. can jump back one directory 

```



### 

Mutable and Immutable Objects : 
================================

We can use ID(x) to get the ID of x 
Mutable objects:
list, dict, set, byte array
Immutable objects:
int, float, complex, string, tuple, frozen set [note: immutable version of set], bytes

**Mutable objects is “called by reference”**

**Immutable objects is “Passed by value”**

![](resources/14D00894966C95DFDCBAE46789D744CD.png)



About the Assignment & Reference 
=================================

```python
l = [1,2,3]
m = l
l=[1,2] # pass by value 
# m [1, 2, 3] 

l = [1,2,3]
m = l
l[0]=4 #call by reference 
#m [4, 2, 3]

l = [1,2,3]
m = [1,2,3]
print(id(l))
print(id(m))
l=[1,2]
# m [1, 2, 3]
# Different ID 

l = 1
m = 1
print(id(l))
print(id(m))
# they dont change value together even if they use same ID 

def changeList(l):
    l[0]=4
l = [1,2,3]
changeList(l)
# l [4,2,3]

import copy
l = [1,2,3]
m = copy.copy(l)#pass by value
l[0]=4;
m
# m [1, 2, 3]

import copy
l = [1,2,3]
L = ['a',l,'b']#call by reference 
m = copy.copy(L)
L[1]="aaaa"
print(L)
l.append(4)
#L ['a', 'aaaa', 'b']
#m['a', [1, 2, 3, 4], 'b']
l = [1,2,3]
L = ['a',l,'b']
m = copy.deepcopy(L) #pass by value 
l.append(4) 
# m ['a', [1, 2, 3], 'b']
```



