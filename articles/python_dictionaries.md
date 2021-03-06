# Dictionaries



Dictionary is the Python's <code>HashTable</code> implementation and might be one of the most common used data structures in programming. But they are named differently in almost most common languages. In Java they're called <code>HashMap</code>, in .NET <code>KeyValuePair</code>. In the most simplest form, a dictionary is;

<img src='https://developers.google.com/edu/python/images/dict.png' alt='python dictionary' />

## Creating a dictionary

There are two ways to create dictionaries in Python;

```python
>>> michaeljordan = { "name" : "Micheal", "surname" : "Jordan", "nick" : "AirJordan", "status" : "Legend", "age" : 50}
>>> michaeljordan_two = dict(name="Micheal",surname='Jordan',nick="AirJordan",status="Legend",age=50)
```

<code>"name"</code> is the key, and <code>"Michael"</code> is the value of the key. This is why .NET call them KeyValuePairs, and behind the scenes, dictionary objects' keys are stored as hashed, thus in Java they call them HashMaps. 

As you see when you define a dictionary via curly brackets <code>{}</code>, you have to use string declaration syntax for keys as well. 



## How to get the value of a key ?

 There are a number of ways to get the value(s) of a key

```python
>>> michaeljordan['name']
'Michael'
```

there is a side effect when using this version; if the given <code>key</code> does not exist, Python will throw a <code>KeyError</code> exception. I typed the following into the Python REPL, and got the following result

```python
>>> michaeljordan["python_articles"]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'python_articles'
```


Python is a straightforward language, if you want to get a value of a key, use <code>get</code> function.

```python
>>> michaeljordan.get("python_articles")
```


will return <code>None</code> so that you won't see anything in the terminal.

```python
>>> michaeljordan.get.__doc__
'D.get(k[,d]) -> D[k] if k in D, else d.  d defaults to None.'
``` 


The value of a non-existing key is None, Let's specify a default value <code>&lt;no_name&gt;</code>

```python
>>> michaeljordan.get("python_articles","<no_name>")
'<no_name>'
``` 


## Check if a key exist

Dictionaries have **has_key** method which returns a bool value; ( **Note : Python 3 does not have <code>has_key</code> function anymore.**)

```python
>>> michaeljordan.has_key("python_articles")
False
```

but it's not the preferred way. The better way to do it is;

```python
>>> 'python_articles' in michaeljordan
False
>>> 'name' in michaeljordan
True
```


## Iterate all the key/values of the dictionary


```python
>>> michaeljordan.items()
[('status', 'Legend'), ('nick', 'AirJordan'), ('age', 50), ('surname', 'Jordan'), ('name', 'Micheal')]
>>> for key, value in michaeljordan.items():
...     print key, value
... 
status Legend
nick AirJordan
age 50
surname Jordan
name Micheal
```

To print key values, sorted by the key, you can use the built in <code>sorted</code> function

```python
>>> for key, value in sorted(michaeljordan.items()):
...     print key, value
... 
age 50
name Micheal
nick AirJordan
status Legend
surname Jordan
```


## How to get all the keys within a dictionary ? 

<code>keys</code> method helps you to get all the keys of a dictionary. It returns a list of strings 

```python
>>> michaeljordan.keys()
['status', 'nick', 'surname', 'name']
```

## Updating the value of a key

I made a typo while setting the name of Mr Jordan. Let's fix it.

```python
michaeljordan['name'] = "Michael"
michaeljordan_two['name'] = "Michael"
```

## Adding a new key value to existing Dictionary

It's pretty straight forward as well

```python
michaeljordan['team'] = "Chicago Bulls"
```

adds the key **team** to the dictionary


## Dictionaries inside dictionaries

If you are going to work on any API, you have the understand the nested concept of dictionaries which are inside lists, tuples or in other dictionaries.

Let's add Mr. Jordans work history. Starting with Chicago Bulls

```python
>>> michaeljordan = { "name" : "Micheal", "surname" : "Jordan", "nick" : "AirJordan", "status" : "Legend", "age" : 50 , "team" : { "name" : "Chicago Bulls" , "start_year" : 1984 , "end_year" : 1998 } }
```

Lets get the **start_year** and **end_year** from the dictionary.

```python
>>> michaeljordan['team']['start_year']
1984
```

But Mr. Jordan did not play only for Chicago Bulls

```python
>>> michaeljordan['teams'] = [ {"name" : "Chicago Bulls" , "start_year" : 1984 , "end_year" : 1998 }, { "name" : "Washington Wizards" , "start_year" : 2001 , "end_year" : 2003 } ]
```

Iterate through all the teams that Mr. Jordan played

```python
>>> michaeljordan['teams'] = [ {"name" : "Chicago Bulls" , "start_year" : 1984 , "end_year" : 1998 }, { "name" : "Washington Wizards" , "start_year" : 2001 , "end_year" : 2003 } ]
>>> for team in michaeljordan['teams'] :
...     print team['name'], team['start_year'], team['end_year'] 
... 
Chicago Bulls 1984 1998
Washington Wizards 2001 2003
```

Lets combine our [List Comprehension knowledge](http://pythonarticles.com/list_comprehension.html) with dictionaries. Create an array of array which contains the values and key of the teams data. 

```python
>>> [team.values() for team in michaeljordan['teams']]
[[1998, 1984, 'Chicago Bulls'], [2003, 2001, 'Washington Wizards']]
>>> [team.keys() for team in michaeljordan['teams']]
[['end_year', 'start_year', 'name'], ['end_year', 'start_year', 'name']]
>>> """Rather than using a list, lets use a tuple"""
>>> [tuple(team.values()) for team in michaeljordan['teams']]
[(1998, 1984, 'Chicago Bulls'), (2003, 2001, 'Washington Wizards')]
```

## Copy a dictionary into another one

Our original Mr. Jordan information was stored in a variable called **michaeljordan** and we made some changes, but **michaeljordan_two** was not sync with the <code>michaeljordan</code>

```python
>>> michaeljordan = { "name" : "Micheal", "surname" : "Jordan", "nick" : "AirJordan", "status" : "Legend", "age" : 50}
>>> michaeljordan_two = michaeljordan.copy()
>>> id(michaeljordan)
4298505024
>>> id(michaeljordan_two)
4298523824
>>> michaeljordan['test'] = 1
>>> michaeljordan_two['test']
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'test'
>>> michaeljordan.copy.__doc__
'D.copy() -> a shallow copy of D'
```

As the copy function descriptor explains, method copies all the value of the <code>michaeljordan</code> variable into a new **dictionary instance**.

```python
>>> michaeljordan_three = michaeljordan
>>> michaeljordan['test2'] = 2
>>> michaeljordan_three['test2']
2
```

Whereas assigning <code>michaeljordan_three</code> to <code>michaeljordan</code> made the <code>michaeljordan_three</code> pointing to the value of the <code>michaeljordan</code>. So when working with dictionaries, think carefully how the new variable should act upon the changes in the original variable. 


## Delete a key from the dictionary

Our <code>team</code> key became pointless once we set the <code>teams</code> key. Lets remove it

```python
>>> del michaeljordan['team']
>>> michaeljordan
{'status': 'Legend', 'surname': 'Jordan', 'name': 'Micheal', 'age': 50, 'teams': [{'end_year': 1998, 'start_year': 1984, 'name': 'Chicago Bulls'}, {'end_year': 2003, 'start_year': 2001, 'name': 'Washington Wizards'}], 'nick': 'AirJordan'}
```

## Setdefault

It's a handy function, like a placeholder. If the key exist in the dictionary returns the value, if not the value which set by the<code>setdefault</code> call is returned. Here is an example..

```python
>>> a = {}
>>> a.setdefault("test","empty")
'empty'
>>> a['test']
'empty'
>>> a['test2']
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'test2'
>>> a['test'] = 'not-empty-anymore'
>>> a['test']
'not-empty-anymore'
```

## Dictionary comprehension

Have you read the [List Comprehension](http://pythonarticles.com/list_comprehension.html) ? 

The following code will only work **Python2.7+**

```python
>>> sequence = [(1,2), (2,3) , (3,4)]  # will work with list of tuples
>>> sequence = ((1,2), (2,3) , (3,4))  # will also work with tuple of tuples
>>> {key: value for (key, value) in sequence}
{1: 2, 2: 3, 3: 4}
```

For earlier versions of python

<code>dict((key, value) for (key, value) in sequence)</code>

### Contributors

Thanks to [@thijsdezoete](https://github.com/thijsdezoete)  and thanks Mr. Jordan for being awesome...

<iframe src="//www.youtube.com/embed/LAr6oAKieHk" frameborder="0" allowfullscreen></iframe>