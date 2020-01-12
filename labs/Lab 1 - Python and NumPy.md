---
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.1'
      jupytext_version: 1.2.4
  kernelspec:
    display_name: Python 3
    language: python
    name: python3
---

# Name(s)
**Matthew Mazzagatte**


**Instructions:** This is an individual assignment, but you may discuss your code with your neighbors.


# Python and NumPy

While other IDEs exist for Python development and for data science related activities, one of the most popular environments is Jupyter Notebooks.

This lab is not intended to teach you everything you will use in this course. Instead, it is designed to give you exposure to some critical components from NumPy that we will rely upon routinely.

## Exercise 0
Please read and reference the following as your progress through this course. 

* [What is the Jupyter Notebook?](https://nbviewer.jupyter.org/github/jupyter/notebook/blob/master/docs/source/examples/Notebook/What%20is%20the%20Jupyter%20Notebook.ipynb#)
* [Notebook Tutorial](https://www.datacamp.com/community/tutorials/tutorial-jupyter-notebook)
* [Notebook Basics](https://nbviewer.jupyter.org/github/jupyter/notebook/blob/master/docs/source/examples/Notebook/Notebook%20Basics.ipynb)

**In the space provided below, what are three things that still remain unclear or need further explanation?**


**The first thing is that I would love to continue to learn more tips and tricks of using Jupyter.
Also, I'm still not fully clear on how to send to github from here and how we will be using github through this. 
Lastly, do we need to do anything to have the md update automatically for future labs or will it always be synced?**


## Exercises 1-7
For the following exercises please read the Python appendix in the Marsland textbook and answer problems A.1-A.7 in the space provided below.


## Exercise 1

```python
import numpy as np
a = np.ones((6, 4)) * 2
a
```

## Exercise 2

```python
b = np.insert(np.insert((np.eye(4) * 2) + 1, 4, 1, axis=0), 5, 1, axis=0)
b
#b[range(4), range(4)] = 3
```

## Exercise 3

```python
a * b
```

a*b works because it is just element wise multiplication

dot(a,b) does not work because this is using matrix multiplication and here the number of columns
in a != the number of rows in b


## Exercise 4

```python
np.dot(a.transpose(), b)
```

```python
np.dot(a, b.transpose())
```

They are different shapes because the first multiplication is a 4x6 * 6x4 which results in a 4x4
whereas the second one is 6x4 * 4x6 which results in a 6x6


## Exercise 5

```python
def funct(x):
    print(x*3)
funct(4)
```

## Exercise 6

```python
def matmaking():
    a = np.random.rand(5, 5)
    print("Sum: ", sum(sum(a)))
    print("Mean: ", a.mean())
matmaking()
```

## Exercise 7

```python
def count_ones(x):
    c = 0
    for i in range(x.shape[0]):
        for j in range(x.shape[1]):
            if x[i][j] == 1:     
                c += 1
    print(c, len(np.where(x==1)[0]))
count_ones(b)
```

## Excercises 8-???
While the Marsland book avoids using another popular package called Pandas, we will use it at times throughout this course. Please read and study [10 minutes to Pandas](https://pandas.pydata.org/pandas-docs/stable/getting_started/10min.html) before proceeding to any of the exercises below.


## Exercise 8
Repeat exercise A.1 from Marsland, but create a Pandas DataFrame instead of a NumPy array.

```python
import pandas as pd
```

```python
a = pd.DataFrame((np.ones((6,4)) * 2))
a
```

## Exercise 9
Repeat exercise A.2 using a DataFrame instead.

```python
b = pd.DataFrame(np.insert(np.insert((np.eye(4) * 2) + 1, 4, 1, axis=0), 5, 1, axis=0))
b
```

## Exercise 10
Repeat exercise A.3 using DataFrames instead.

```python
a*b

# dot(a, b) still does not work as these matrices cannot be multiplied together using matrix multiplication
```

## Exercise 11
Repeat exercise A.7 using a dataframe.

```python
def count_ones_again(x):
    c = 0
    for i in range(x.shape[1]):
        for j in range(x.shape[0]):
            if x[i][j] == 1:
                c += 1
    print(c, len(np.where(x==1)[0]))
count_ones_again(b)
```

## Exercises 12-14
Now let's look at a real dataset, and talk about ``.loc``. For this exercise, we will use the popular Titanic dataset from Kaggle. Here is some sample code to read it into a dataframe.

```python
titanic_df = pd.read_csv(
    "https://raw.githubusercontent.com/dlsun/data-science-book/master/data/titanic.csv"
)
titanic_df
```

Notice how we have nice headers and mixed datatypes? That is one of the reasons we might use Pandas. Please refresh your memory by looking at the 10 minutes to Pandas again, but then answer the following.


## Exercise 12
How do you select the ``name`` column without using .iloc?

```python
titanic_df.name
```

## Exercise 13
After setting the index to ``sex``, how do you select all passengers that are ``female``? And how many female passengers are there?

```python
titanic_df.set_index('sex',inplace=True)
titanic_df.loc["female"]
```

```python
print(len(titanic_df.loc["female"]), "female passengers")
```

## Exercise 14
How do you reset the index?

```python
titanic_df = titanic_df.reset_index()
titanic_df.head()
```

We can see that the index was reset.
