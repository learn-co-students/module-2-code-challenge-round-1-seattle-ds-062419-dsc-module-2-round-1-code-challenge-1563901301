
# Module 2 Assessment

Welcome to your Mod 2 Assessment. You will be tested for your understanding of concepts and ability to solve problems that have been covered in class and in the curriculum.

Use any libraries you want to solve the problems in the assessment.

You will have up to two hours to complete this assessment.

The sections of the assessment are:

- Accessing Data Through APIs
- Object Oriented Programming
- SQL and Relational Databases
- HTML, CSS and Web Scraping
- Other Database Structures (MongoDB)

In this assessment you will be exploring two datasets: Pokemon and Quotes.


```python
# import the necessary libraries

import requests
import json
import pandas as pd
import sqlite3
from bs4 import BeautifulSoup
import pymongo
```

## Part 1: Accessing Data Through APIs

In this section we'll be using PokeAPI to get data on Pokemon. Let's first define functions to get information from the API. Provided below is a URL that will get you started with the first 151 Pokemon! Run the cell below to see what we get.


```python
url = 'https://pokeapi.co/api/v2/pokemon/?limit=151'
results = requests.get(url).json()['results']
results
```




    [{'name': 'bulbasaur', 'url': 'https://pokeapi.co/api/v2/pokemon/1/'},
     {'name': 'ivysaur', 'url': 'https://pokeapi.co/api/v2/pokemon/2/'},
     {'name': 'venusaur', 'url': 'https://pokeapi.co/api/v2/pokemon/3/'},
     {'name': 'charmander', 'url': 'https://pokeapi.co/api/v2/pokemon/4/'},
     {'name': 'charmeleon', 'url': 'https://pokeapi.co/api/v2/pokemon/5/'},
     {'name': 'charizard', 'url': 'https://pokeapi.co/api/v2/pokemon/6/'},
     {'name': 'squirtle', 'url': 'https://pokeapi.co/api/v2/pokemon/7/'},
     {'name': 'wartortle', 'url': 'https://pokeapi.co/api/v2/pokemon/8/'},
     {'name': 'blastoise', 'url': 'https://pokeapi.co/api/v2/pokemon/9/'},
     {'name': 'caterpie', 'url': 'https://pokeapi.co/api/v2/pokemon/10/'},
     {'name': 'metapod', 'url': 'https://pokeapi.co/api/v2/pokemon/11/'},
     {'name': 'butterfree', 'url': 'https://pokeapi.co/api/v2/pokemon/12/'},
     {'name': 'weedle', 'url': 'https://pokeapi.co/api/v2/pokemon/13/'},
     {'name': 'kakuna', 'url': 'https://pokeapi.co/api/v2/pokemon/14/'},
     {'name': 'beedrill', 'url': 'https://pokeapi.co/api/v2/pokemon/15/'},
     {'name': 'pidgey', 'url': 'https://pokeapi.co/api/v2/pokemon/16/'},
     {'name': 'pidgeotto', 'url': 'https://pokeapi.co/api/v2/pokemon/17/'},
     {'name': 'pidgeot', 'url': 'https://pokeapi.co/api/v2/pokemon/18/'},
     {'name': 'rattata', 'url': 'https://pokeapi.co/api/v2/pokemon/19/'},
     {'name': 'raticate', 'url': 'https://pokeapi.co/api/v2/pokemon/20/'},
     {'name': 'spearow', 'url': 'https://pokeapi.co/api/v2/pokemon/21/'},
     {'name': 'fearow', 'url': 'https://pokeapi.co/api/v2/pokemon/22/'},
     {'name': 'ekans', 'url': 'https://pokeapi.co/api/v2/pokemon/23/'},
     {'name': 'arbok', 'url': 'https://pokeapi.co/api/v2/pokemon/24/'},
     {'name': 'pikachu', 'url': 'https://pokeapi.co/api/v2/pokemon/25/'},
     {'name': 'raichu', 'url': 'https://pokeapi.co/api/v2/pokemon/26/'},
     {'name': 'sandshrew', 'url': 'https://pokeapi.co/api/v2/pokemon/27/'},
     {'name': 'sandslash', 'url': 'https://pokeapi.co/api/v2/pokemon/28/'},
     {'name': 'nidoran-f', 'url': 'https://pokeapi.co/api/v2/pokemon/29/'},
     {'name': 'nidorina', 'url': 'https://pokeapi.co/api/v2/pokemon/30/'},
     {'name': 'nidoqueen', 'url': 'https://pokeapi.co/api/v2/pokemon/31/'},
     {'name': 'nidoran-m', 'url': 'https://pokeapi.co/api/v2/pokemon/32/'},
     {'name': 'nidorino', 'url': 'https://pokeapi.co/api/v2/pokemon/33/'},
     {'name': 'nidoking', 'url': 'https://pokeapi.co/api/v2/pokemon/34/'},
     {'name': 'clefairy', 'url': 'https://pokeapi.co/api/v2/pokemon/35/'},
     {'name': 'clefable', 'url': 'https://pokeapi.co/api/v2/pokemon/36/'},
     {'name': 'vulpix', 'url': 'https://pokeapi.co/api/v2/pokemon/37/'},
     {'name': 'ninetales', 'url': 'https://pokeapi.co/api/v2/pokemon/38/'},
     {'name': 'jigglypuff', 'url': 'https://pokeapi.co/api/v2/pokemon/39/'},
     {'name': 'wigglytuff', 'url': 'https://pokeapi.co/api/v2/pokemon/40/'},
     {'name': 'zubat', 'url': 'https://pokeapi.co/api/v2/pokemon/41/'},
     {'name': 'golbat', 'url': 'https://pokeapi.co/api/v2/pokemon/42/'},
     {'name': 'oddish', 'url': 'https://pokeapi.co/api/v2/pokemon/43/'},
     {'name': 'gloom', 'url': 'https://pokeapi.co/api/v2/pokemon/44/'},
     {'name': 'vileplume', 'url': 'https://pokeapi.co/api/v2/pokemon/45/'},
     {'name': 'paras', 'url': 'https://pokeapi.co/api/v2/pokemon/46/'},
     {'name': 'parasect', 'url': 'https://pokeapi.co/api/v2/pokemon/47/'},
     {'name': 'venonat', 'url': 'https://pokeapi.co/api/v2/pokemon/48/'},
     {'name': 'venomoth', 'url': 'https://pokeapi.co/api/v2/pokemon/49/'},
     {'name': 'diglett', 'url': 'https://pokeapi.co/api/v2/pokemon/50/'},
     {'name': 'dugtrio', 'url': 'https://pokeapi.co/api/v2/pokemon/51/'},
     {'name': 'meowth', 'url': 'https://pokeapi.co/api/v2/pokemon/52/'},
     {'name': 'persian', 'url': 'https://pokeapi.co/api/v2/pokemon/53/'},
     {'name': 'psyduck', 'url': 'https://pokeapi.co/api/v2/pokemon/54/'},
     {'name': 'golduck', 'url': 'https://pokeapi.co/api/v2/pokemon/55/'},
     {'name': 'mankey', 'url': 'https://pokeapi.co/api/v2/pokemon/56/'},
     {'name': 'primeape', 'url': 'https://pokeapi.co/api/v2/pokemon/57/'},
     {'name': 'growlithe', 'url': 'https://pokeapi.co/api/v2/pokemon/58/'},
     {'name': 'arcanine', 'url': 'https://pokeapi.co/api/v2/pokemon/59/'},
     {'name': 'poliwag', 'url': 'https://pokeapi.co/api/v2/pokemon/60/'},
     {'name': 'poliwhirl', 'url': 'https://pokeapi.co/api/v2/pokemon/61/'},
     {'name': 'poliwrath', 'url': 'https://pokeapi.co/api/v2/pokemon/62/'},
     {'name': 'abra', 'url': 'https://pokeapi.co/api/v2/pokemon/63/'},
     {'name': 'kadabra', 'url': 'https://pokeapi.co/api/v2/pokemon/64/'},
     {'name': 'alakazam', 'url': 'https://pokeapi.co/api/v2/pokemon/65/'},
     {'name': 'machop', 'url': 'https://pokeapi.co/api/v2/pokemon/66/'},
     {'name': 'machoke', 'url': 'https://pokeapi.co/api/v2/pokemon/67/'},
     {'name': 'machamp', 'url': 'https://pokeapi.co/api/v2/pokemon/68/'},
     {'name': 'bellsprout', 'url': 'https://pokeapi.co/api/v2/pokemon/69/'},
     {'name': 'weepinbell', 'url': 'https://pokeapi.co/api/v2/pokemon/70/'},
     {'name': 'victreebel', 'url': 'https://pokeapi.co/api/v2/pokemon/71/'},
     {'name': 'tentacool', 'url': 'https://pokeapi.co/api/v2/pokemon/72/'},
     {'name': 'tentacruel', 'url': 'https://pokeapi.co/api/v2/pokemon/73/'},
     {'name': 'geodude', 'url': 'https://pokeapi.co/api/v2/pokemon/74/'},
     {'name': 'graveler', 'url': 'https://pokeapi.co/api/v2/pokemon/75/'},
     {'name': 'golem', 'url': 'https://pokeapi.co/api/v2/pokemon/76/'},
     {'name': 'ponyta', 'url': 'https://pokeapi.co/api/v2/pokemon/77/'},
     {'name': 'rapidash', 'url': 'https://pokeapi.co/api/v2/pokemon/78/'},
     {'name': 'slowpoke', 'url': 'https://pokeapi.co/api/v2/pokemon/79/'},
     {'name': 'slowbro', 'url': 'https://pokeapi.co/api/v2/pokemon/80/'},
     {'name': 'magnemite', 'url': 'https://pokeapi.co/api/v2/pokemon/81/'},
     {'name': 'magneton', 'url': 'https://pokeapi.co/api/v2/pokemon/82/'},
     {'name': 'farfetchd', 'url': 'https://pokeapi.co/api/v2/pokemon/83/'},
     {'name': 'doduo', 'url': 'https://pokeapi.co/api/v2/pokemon/84/'},
     {'name': 'dodrio', 'url': 'https://pokeapi.co/api/v2/pokemon/85/'},
     {'name': 'seel', 'url': 'https://pokeapi.co/api/v2/pokemon/86/'},
     {'name': 'dewgong', 'url': 'https://pokeapi.co/api/v2/pokemon/87/'},
     {'name': 'grimer', 'url': 'https://pokeapi.co/api/v2/pokemon/88/'},
     {'name': 'muk', 'url': 'https://pokeapi.co/api/v2/pokemon/89/'},
     {'name': 'shellder', 'url': 'https://pokeapi.co/api/v2/pokemon/90/'},
     {'name': 'cloyster', 'url': 'https://pokeapi.co/api/v2/pokemon/91/'},
     {'name': 'gastly', 'url': 'https://pokeapi.co/api/v2/pokemon/92/'},
     {'name': 'haunter', 'url': 'https://pokeapi.co/api/v2/pokemon/93/'},
     {'name': 'gengar', 'url': 'https://pokeapi.co/api/v2/pokemon/94/'},
     {'name': 'onix', 'url': 'https://pokeapi.co/api/v2/pokemon/95/'},
     {'name': 'drowzee', 'url': 'https://pokeapi.co/api/v2/pokemon/96/'},
     {'name': 'hypno', 'url': 'https://pokeapi.co/api/v2/pokemon/97/'},
     {'name': 'krabby', 'url': 'https://pokeapi.co/api/v2/pokemon/98/'},
     {'name': 'kingler', 'url': 'https://pokeapi.co/api/v2/pokemon/99/'},
     {'name': 'voltorb', 'url': 'https://pokeapi.co/api/v2/pokemon/100/'},
     {'name': 'electrode', 'url': 'https://pokeapi.co/api/v2/pokemon/101/'},
     {'name': 'exeggcute', 'url': 'https://pokeapi.co/api/v2/pokemon/102/'},
     {'name': 'exeggutor', 'url': 'https://pokeapi.co/api/v2/pokemon/103/'},
     {'name': 'cubone', 'url': 'https://pokeapi.co/api/v2/pokemon/104/'},
     {'name': 'marowak', 'url': 'https://pokeapi.co/api/v2/pokemon/105/'},
     {'name': 'hitmonlee', 'url': 'https://pokeapi.co/api/v2/pokemon/106/'},
     {'name': 'hitmonchan', 'url': 'https://pokeapi.co/api/v2/pokemon/107/'},
     {'name': 'lickitung', 'url': 'https://pokeapi.co/api/v2/pokemon/108/'},
     {'name': 'koffing', 'url': 'https://pokeapi.co/api/v2/pokemon/109/'},
     {'name': 'weezing', 'url': 'https://pokeapi.co/api/v2/pokemon/110/'},
     {'name': 'rhyhorn', 'url': 'https://pokeapi.co/api/v2/pokemon/111/'},
     {'name': 'rhydon', 'url': 'https://pokeapi.co/api/v2/pokemon/112/'},
     {'name': 'chansey', 'url': 'https://pokeapi.co/api/v2/pokemon/113/'},
     {'name': 'tangela', 'url': 'https://pokeapi.co/api/v2/pokemon/114/'},
     {'name': 'kangaskhan', 'url': 'https://pokeapi.co/api/v2/pokemon/115/'},
     {'name': 'horsea', 'url': 'https://pokeapi.co/api/v2/pokemon/116/'},
     {'name': 'seadra', 'url': 'https://pokeapi.co/api/v2/pokemon/117/'},
     {'name': 'goldeen', 'url': 'https://pokeapi.co/api/v2/pokemon/118/'},
     {'name': 'seaking', 'url': 'https://pokeapi.co/api/v2/pokemon/119/'},
     {'name': 'staryu', 'url': 'https://pokeapi.co/api/v2/pokemon/120/'},
     {'name': 'starmie', 'url': 'https://pokeapi.co/api/v2/pokemon/121/'},
     {'name': 'mr-mime', 'url': 'https://pokeapi.co/api/v2/pokemon/122/'},
     {'name': 'scyther', 'url': 'https://pokeapi.co/api/v2/pokemon/123/'},
     {'name': 'jynx', 'url': 'https://pokeapi.co/api/v2/pokemon/124/'},
     {'name': 'electabuzz', 'url': 'https://pokeapi.co/api/v2/pokemon/125/'},
     {'name': 'magmar', 'url': 'https://pokeapi.co/api/v2/pokemon/126/'},
     {'name': 'pinsir', 'url': 'https://pokeapi.co/api/v2/pokemon/127/'},
     {'name': 'tauros', 'url': 'https://pokeapi.co/api/v2/pokemon/128/'},
     {'name': 'magikarp', 'url': 'https://pokeapi.co/api/v2/pokemon/129/'},
     {'name': 'gyarados', 'url': 'https://pokeapi.co/api/v2/pokemon/130/'},
     {'name': 'lapras', 'url': 'https://pokeapi.co/api/v2/pokemon/131/'},
     {'name': 'ditto', 'url': 'https://pokeapi.co/api/v2/pokemon/132/'},
     {'name': 'eevee', 'url': 'https://pokeapi.co/api/v2/pokemon/133/'},
     {'name': 'vaporeon', 'url': 'https://pokeapi.co/api/v2/pokemon/134/'},
     {'name': 'jolteon', 'url': 'https://pokeapi.co/api/v2/pokemon/135/'},
     {'name': 'flareon', 'url': 'https://pokeapi.co/api/v2/pokemon/136/'},
     {'name': 'porygon', 'url': 'https://pokeapi.co/api/v2/pokemon/137/'},
     {'name': 'omanyte', 'url': 'https://pokeapi.co/api/v2/pokemon/138/'},
     {'name': 'omastar', 'url': 'https://pokeapi.co/api/v2/pokemon/139/'},
     {'name': 'kabuto', 'url': 'https://pokeapi.co/api/v2/pokemon/140/'},
     {'name': 'kabutops', 'url': 'https://pokeapi.co/api/v2/pokemon/141/'},
     {'name': 'aerodactyl', 'url': 'https://pokeapi.co/api/v2/pokemon/142/'},
     {'name': 'snorlax', 'url': 'https://pokeapi.co/api/v2/pokemon/143/'},
     {'name': 'articuno', 'url': 'https://pokeapi.co/api/v2/pokemon/144/'},
     {'name': 'zapdos', 'url': 'https://pokeapi.co/api/v2/pokemon/145/'},
     {'name': 'moltres', 'url': 'https://pokeapi.co/api/v2/pokemon/146/'},
     {'name': 'dratini', 'url': 'https://pokeapi.co/api/v2/pokemon/147/'},
     {'name': 'dragonair', 'url': 'https://pokeapi.co/api/v2/pokemon/148/'},
     {'name': 'dragonite', 'url': 'https://pokeapi.co/api/v2/pokemon/149/'},
     {'name': 'mewtwo', 'url': 'https://pokeapi.co/api/v2/pokemon/150/'},
     {'name': 'mew', 'url': 'https://pokeapi.co/api/v2/pokemon/151/'}]



[Read the documentation here](https://pokeapi.co/) for information on navigating this API and use the API to obtain data to answer the following questions.

### Accessing Data

1. For any **one** Pokemon, retrive the following information in a dictionary format with the following keys:
    - ID
    - Name
    - Base experience
    - Weight
    - Height
    - Types
    - Abilities

For `Types` and `Abilities`, you might want to write helper functions to have each attribute just be a list of types and a list of abilities. Your output should look like this:

```
{'id': 1, 
'name': 'bulbasaur', 
'base_experience': 64, 
'weight': 69, 
'height': 7, 
'types': ['poison', 'grass'], 
'abilities': ['chlorophyll', 'overgrow']}

```
    



```python
""" SOLUTION: data for one Pokemon """

# helper functions for types and abilities

def typelist(types):
    result = []
    
    # iterating through the nested dict and appending to the empty list:
    
    for i in range(len(types)):
        result.append(types[i]['type']['name'])
    return result

def abilitylist(abilities):
    result = []
    
    # iterating through the nested dict and appending to the empty list:
    
    for i in range(len(abilities)):
        result.append(abilities[i]['ability']['name'])
    return result
```


```python
def get_pokedata(url):
    
    # getting full results for one pokemon
    info = requests.get(url).json() 
    
    # list of keys with values that don't need editing
    keys = ['id', 'name', 'base_experience', 'weight', 'height'] 
    data = {k: info[k] for k in keys} # dictionary comprehension
    
    # using the two helper functions to add types and abilities
    data['types'] = typelist(info['types'])
    data['abilities'] = abilitylist(info['abilities'])
    
    return data
```

### Pagination

2. Get the same information for the first **151** Pokemon as a list of dictionaries ordered by Pokemon ID. Print the first and last elements of the dictionary. (Hint: Use pagination) Your output should save the list to a variable and look like this:

```
[{'id': 1, 
'name': 'bulbasaur', 
'base_experience': 64, 
'weight': 69, 
'height': 7, 
'types': ['poison', 'grass'], 
'abilities': ['chlorophyll', 'overgrow']}, 
{'id': 2, 
'name': 'ivysaur', 
'base_experience': 142, 
'weight': 130, 
'height': 10, 
'types': ['poison', 'grass'], 
'abilities': ['chlorophyll', 'overgrow']}, ... ]

```




```python
""" SOLUTION: data for 151 Pokemon """

# list comprehension to get a list of just URLs
urls = [r['url'] for r in results]

# list comprehension with the previous function to get full data
pokedata = [get_pokedata(url) for url in urls]

```


```python
# printing first and last elements

print(pokedata[0], pokedata[-1])
```

    {'id': 1, 'name': 'bulbasaur', 'base_experience': 64, 'weight': 69, 'height': 7, 'types': ['poison', 'grass'], 'abilities': ['chlorophyll', 'overgrow']} {'id': 151, 'name': 'mew', 'base_experience': 270, 'weight': 40, 'height': 4, 'types': ['psychic'], 'abilities': ['synchronize']}


## Part 2: Object Oriented Programming

We're going to use the data gathered in the previous section on APIs for this section on Object Oriented Programming to instantiate Pokemon objects and write instance methods.

### Creating a Class

1. Create a class called `Pokemon` with an `__init__` method to instantiate the following attributes:
    - ID
    - Name
    - Base experience
    - Weight
    - Height
    - Types
    - Abilities
    
    
### Instantiating Objects

2. Using the data you obtained from the API, instantiate the first, fourth and seventh Pokemon. Assign them to the variables `bulbasaur`, `charmander` and `squirtle`.



```python
# if you were unable to get the data from the API in the right format,
# uncomment the code below to access a JSON file with the list of dictionaries

# with open('data/pokemon.json') as f:  
#     pokelist = json.load(f)
```


```python
class Pokemon:
    
    def __init__(self, ID, name, exp, weight, height, types, abilities):
        self.ID = ID
        self.name = name
        self.exp = exp
        self.weight = weight
        self.height = height
        self.types = types
        self.abilities = abilities
        
    def bmi(self):
        return (self.weight*0.1)/(self.height*0.1)**2
        

```


```python
""" SOLUTION: instantiating three Pokemon """

# function to instantiate a Pokemon
def instantiate_pokemon(info):
    pokemon = Pokemon(info['id'], 
                      info['name'], 
                      info['base_experience'], 
                      info['weight'], 
                      info['height'], 
                      info['types'],
                      info['abilities'])
    return pokemon

"""
can also be done manually:

bulbasaur = Pokemon(1, 'bulbasaur', 64, 69, 7, ['poison', 'grass'], ['chlorophyll', 'overgrow'])

etc.

"""

bulbasaur = instantiate_pokemon(pokedata[0])
charmander = instantiate_pokemon(pokedata[3])
squirtle = instantiate_pokemon(pokedata[6])
```


```python
# run this cell to test and check your code
# you may need to edit the attribute variable names if you named them differently!

def print_pokeinfo(pokemon_object):
    o = pokemon_object
    print('ID: ' + str(o.ID) + '\n' +
          'Name: ' + o.name.title() + '\n' +
          'Base experience: ' + str(o.exp) + '\n' +
          'Weight: ' + str(o.weight) + '\n' +
          'Height: ' + str(o.height) + '\n' +
          'Types: ' + str(o.types) + '\n' +
          'Abilities: ' + str(o.abilities) + '\n'
         )
    
print_pokeinfo(bulbasaur)
print_pokeinfo(ivysaur)
print_pokeinfo(venusaur)
```

    ID: 1
    Name: Bulbasaur
    Base experience: 64
    Weight: 69
    Height: 7
    Types: ['poison', 'grass']
    Abilities: ['chlorophyll', 'overgrow']
    
    ID: 4
    Name: Charmander
    Base experience: 62
    Weight: 85
    Height: 6
    Types: ['fire']
    Abilities: ['solar-power', 'blaze']
    
    ID: 7
    Name: Squirtle
    Base experience: 63
    Weight: 90
    Height: 5
    Types: ['water']
    Abilities: ['rain-dish', 'torrent']
    


### Instance Methods

3. Write an instance method within the class `Pokemon` to find the BMI of a Pokemon. BMI is defined by $\frac{weight}{height^{2}}$ with weight in **kilograms** and height in **meters**. The height and weight data of Pokemon from the API is in **decimeters** and **hectograms** respectively.


    1 decimeter = 0.1 meters
    1 hectogram = 0.1 kilograms


```python
# run this cell to test and check your code
# you probably have to rerun the code to instantiate your objects

print(bulbasaur.bmi()) # 14.08
print(charmander.bmi()) # 23.61
print(squirtle.bmi()) # 36
```

    14.081632653061222
    23.611111111111104
    36.0


## Part 3: SQL and Relational Databases

For this section, we've put the Pokemon data into SQL tables. You won't need to use your list of dictionaries or the JSON file for this section. The schema of `pokemon.db` is as follows:

<img src="data/pokemondb.png" alt="db schema" style="width:500px;"/>

Assign your SQL queries as strings to the variables `q1`, `q2`, etc. and run the cells at the end of this section to print your results as Pandas DataFrames.

- q1: query all columns from `Pokemon` the Pokemon that have base_experience above 200
- q2: query the id, name, type1 and type2 of Pokemon that have **water** types as either their first or second type
- q3: query the average weight of Pokemon by their first type in descending order
- q4: query the Pokemon name, Pokemon type2, and what **type2** has "2xdamage" to
- q5: query the top 5 most common type1s, the minimum height, maximum height, minimum weight and maximum weight of pokemon with those type1s, and what associated type they do "0.5xdamage" to


**Important note on syntax**: use `double quotes ""` when quoting strings **within** your query and wrap the entire query in `single quotes ''` For the column titles that begin with numbers, you need to wrap the column names in double quotes.


```python
cnx = sqlite3.connect('data/pokemon.db')
```


```python
q1 = 'select * from pokemon where base_experience > 150'
pd.read_sql(q1, cnx)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>name</th>
      <th>base_experience</th>
      <th>weight</th>
      <th>height</th>
      <th>type1</th>
      <th>type2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3</td>
      <td>venusaur</td>
      <td>236</td>
      <td>1000</td>
      <td>20</td>
      <td>grass</td>
      <td>poison</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6</td>
      <td>charizard</td>
      <td>240</td>
      <td>905</td>
      <td>17</td>
      <td>fire</td>
      <td>flying</td>
    </tr>
    <tr>
      <th>2</th>
      <td>9</td>
      <td>blastoise</td>
      <td>239</td>
      <td>855</td>
      <td>16</td>
      <td>water</td>
      <td>None</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12</td>
      <td>butterfree</td>
      <td>178</td>
      <td>320</td>
      <td>11</td>
      <td>bug</td>
      <td>flying</td>
    </tr>
    <tr>
      <th>4</th>
      <td>15</td>
      <td>beedrill</td>
      <td>178</td>
      <td>295</td>
      <td>10</td>
      <td>bug</td>
      <td>poison</td>
    </tr>
    <tr>
      <th>5</th>
      <td>18</td>
      <td>pidgeot</td>
      <td>216</td>
      <td>395</td>
      <td>15</td>
      <td>normal</td>
      <td>flying</td>
    </tr>
    <tr>
      <th>6</th>
      <td>22</td>
      <td>fearow</td>
      <td>155</td>
      <td>380</td>
      <td>12</td>
      <td>normal</td>
      <td>flying</td>
    </tr>
    <tr>
      <th>7</th>
      <td>24</td>
      <td>arbok</td>
      <td>157</td>
      <td>650</td>
      <td>35</td>
      <td>poison</td>
      <td>None</td>
    </tr>
    <tr>
      <th>8</th>
      <td>26</td>
      <td>raichu</td>
      <td>218</td>
      <td>300</td>
      <td>8</td>
      <td>electric</td>
      <td>None</td>
    </tr>
    <tr>
      <th>9</th>
      <td>28</td>
      <td>sandslash</td>
      <td>158</td>
      <td>295</td>
      <td>10</td>
      <td>ground</td>
      <td>None</td>
    </tr>
    <tr>
      <th>10</th>
      <td>31</td>
      <td>nidoqueen</td>
      <td>227</td>
      <td>600</td>
      <td>13</td>
      <td>poison</td>
      <td>ground</td>
    </tr>
    <tr>
      <th>11</th>
      <td>34</td>
      <td>nidoking</td>
      <td>227</td>
      <td>620</td>
      <td>14</td>
      <td>poison</td>
      <td>ground</td>
    </tr>
    <tr>
      <th>12</th>
      <td>36</td>
      <td>clefable</td>
      <td>217</td>
      <td>400</td>
      <td>13</td>
      <td>fairy</td>
      <td>None</td>
    </tr>
    <tr>
      <th>13</th>
      <td>38</td>
      <td>ninetales</td>
      <td>177</td>
      <td>199</td>
      <td>11</td>
      <td>fire</td>
      <td>None</td>
    </tr>
    <tr>
      <th>14</th>
      <td>40</td>
      <td>wigglytuff</td>
      <td>196</td>
      <td>120</td>
      <td>10</td>
      <td>normal</td>
      <td>fairy</td>
    </tr>
    <tr>
      <th>15</th>
      <td>42</td>
      <td>golbat</td>
      <td>159</td>
      <td>550</td>
      <td>16</td>
      <td>poison</td>
      <td>flying</td>
    </tr>
    <tr>
      <th>16</th>
      <td>45</td>
      <td>vileplume</td>
      <td>221</td>
      <td>186</td>
      <td>12</td>
      <td>grass</td>
      <td>poison</td>
    </tr>
    <tr>
      <th>17</th>
      <td>49</td>
      <td>venomoth</td>
      <td>158</td>
      <td>125</td>
      <td>15</td>
      <td>bug</td>
      <td>poison</td>
    </tr>
    <tr>
      <th>18</th>
      <td>53</td>
      <td>persian</td>
      <td>154</td>
      <td>320</td>
      <td>10</td>
      <td>normal</td>
      <td>None</td>
    </tr>
    <tr>
      <th>19</th>
      <td>55</td>
      <td>golduck</td>
      <td>175</td>
      <td>766</td>
      <td>17</td>
      <td>water</td>
      <td>None</td>
    </tr>
    <tr>
      <th>20</th>
      <td>57</td>
      <td>primeape</td>
      <td>159</td>
      <td>320</td>
      <td>10</td>
      <td>fighting</td>
      <td>None</td>
    </tr>
    <tr>
      <th>21</th>
      <td>59</td>
      <td>arcanine</td>
      <td>194</td>
      <td>1550</td>
      <td>19</td>
      <td>fire</td>
      <td>None</td>
    </tr>
    <tr>
      <th>22</th>
      <td>62</td>
      <td>poliwrath</td>
      <td>230</td>
      <td>540</td>
      <td>13</td>
      <td>water</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>23</th>
      <td>65</td>
      <td>alakazam</td>
      <td>225</td>
      <td>480</td>
      <td>15</td>
      <td>psychic</td>
      <td>None</td>
    </tr>
    <tr>
      <th>24</th>
      <td>68</td>
      <td>machamp</td>
      <td>227</td>
      <td>1300</td>
      <td>16</td>
      <td>fighting</td>
      <td>None</td>
    </tr>
    <tr>
      <th>25</th>
      <td>71</td>
      <td>victreebel</td>
      <td>221</td>
      <td>155</td>
      <td>17</td>
      <td>grass</td>
      <td>poison</td>
    </tr>
    <tr>
      <th>26</th>
      <td>73</td>
      <td>tentacruel</td>
      <td>180</td>
      <td>550</td>
      <td>16</td>
      <td>water</td>
      <td>poison</td>
    </tr>
    <tr>
      <th>27</th>
      <td>76</td>
      <td>golem</td>
      <td>223</td>
      <td>3000</td>
      <td>14</td>
      <td>rock</td>
      <td>ground</td>
    </tr>
    <tr>
      <th>28</th>
      <td>78</td>
      <td>rapidash</td>
      <td>175</td>
      <td>950</td>
      <td>17</td>
      <td>fire</td>
      <td>None</td>
    </tr>
    <tr>
      <th>29</th>
      <td>80</td>
      <td>slowbro</td>
      <td>172</td>
      <td>785</td>
      <td>16</td>
      <td>water</td>
      <td>psychic</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>40</th>
      <td>106</td>
      <td>hitmonlee</td>
      <td>159</td>
      <td>498</td>
      <td>15</td>
      <td>fighting</td>
      <td>None</td>
    </tr>
    <tr>
      <th>41</th>
      <td>107</td>
      <td>hitmonchan</td>
      <td>159</td>
      <td>502</td>
      <td>14</td>
      <td>fighting</td>
      <td>None</td>
    </tr>
    <tr>
      <th>42</th>
      <td>110</td>
      <td>weezing</td>
      <td>172</td>
      <td>95</td>
      <td>12</td>
      <td>poison</td>
      <td>None</td>
    </tr>
    <tr>
      <th>43</th>
      <td>112</td>
      <td>rhydon</td>
      <td>170</td>
      <td>1200</td>
      <td>19</td>
      <td>ground</td>
      <td>rock</td>
    </tr>
    <tr>
      <th>44</th>
      <td>113</td>
      <td>chansey</td>
      <td>395</td>
      <td>346</td>
      <td>11</td>
      <td>normal</td>
      <td>None</td>
    </tr>
    <tr>
      <th>45</th>
      <td>115</td>
      <td>kangaskhan</td>
      <td>172</td>
      <td>800</td>
      <td>22</td>
      <td>normal</td>
      <td>None</td>
    </tr>
    <tr>
      <th>46</th>
      <td>117</td>
      <td>seadra</td>
      <td>154</td>
      <td>250</td>
      <td>12</td>
      <td>water</td>
      <td>None</td>
    </tr>
    <tr>
      <th>47</th>
      <td>119</td>
      <td>seaking</td>
      <td>158</td>
      <td>390</td>
      <td>13</td>
      <td>water</td>
      <td>None</td>
    </tr>
    <tr>
      <th>48</th>
      <td>121</td>
      <td>starmie</td>
      <td>182</td>
      <td>800</td>
      <td>11</td>
      <td>water</td>
      <td>psychic</td>
    </tr>
    <tr>
      <th>49</th>
      <td>122</td>
      <td>mr-mime</td>
      <td>161</td>
      <td>545</td>
      <td>13</td>
      <td>psychic</td>
      <td>fairy</td>
    </tr>
    <tr>
      <th>50</th>
      <td>124</td>
      <td>jynx</td>
      <td>159</td>
      <td>406</td>
      <td>14</td>
      <td>ice</td>
      <td>psychic</td>
    </tr>
    <tr>
      <th>51</th>
      <td>125</td>
      <td>electabuzz</td>
      <td>172</td>
      <td>300</td>
      <td>11</td>
      <td>electric</td>
      <td>None</td>
    </tr>
    <tr>
      <th>52</th>
      <td>126</td>
      <td>magmar</td>
      <td>173</td>
      <td>445</td>
      <td>13</td>
      <td>fire</td>
      <td>None</td>
    </tr>
    <tr>
      <th>53</th>
      <td>127</td>
      <td>pinsir</td>
      <td>175</td>
      <td>550</td>
      <td>15</td>
      <td>bug</td>
      <td>None</td>
    </tr>
    <tr>
      <th>54</th>
      <td>128</td>
      <td>tauros</td>
      <td>172</td>
      <td>884</td>
      <td>14</td>
      <td>normal</td>
      <td>None</td>
    </tr>
    <tr>
      <th>55</th>
      <td>130</td>
      <td>gyarados</td>
      <td>189</td>
      <td>2350</td>
      <td>65</td>
      <td>water</td>
      <td>flying</td>
    </tr>
    <tr>
      <th>56</th>
      <td>131</td>
      <td>lapras</td>
      <td>187</td>
      <td>2200</td>
      <td>25</td>
      <td>water</td>
      <td>ice</td>
    </tr>
    <tr>
      <th>57</th>
      <td>134</td>
      <td>vaporeon</td>
      <td>184</td>
      <td>290</td>
      <td>10</td>
      <td>water</td>
      <td>None</td>
    </tr>
    <tr>
      <th>58</th>
      <td>135</td>
      <td>jolteon</td>
      <td>184</td>
      <td>245</td>
      <td>8</td>
      <td>electric</td>
      <td>None</td>
    </tr>
    <tr>
      <th>59</th>
      <td>136</td>
      <td>flareon</td>
      <td>184</td>
      <td>250</td>
      <td>9</td>
      <td>fire</td>
      <td>None</td>
    </tr>
    <tr>
      <th>60</th>
      <td>139</td>
      <td>omastar</td>
      <td>173</td>
      <td>350</td>
      <td>10</td>
      <td>rock</td>
      <td>water</td>
    </tr>
    <tr>
      <th>61</th>
      <td>141</td>
      <td>kabutops</td>
      <td>173</td>
      <td>405</td>
      <td>13</td>
      <td>rock</td>
      <td>water</td>
    </tr>
    <tr>
      <th>62</th>
      <td>142</td>
      <td>aerodactyl</td>
      <td>180</td>
      <td>590</td>
      <td>18</td>
      <td>rock</td>
      <td>flying</td>
    </tr>
    <tr>
      <th>63</th>
      <td>143</td>
      <td>snorlax</td>
      <td>189</td>
      <td>4600</td>
      <td>21</td>
      <td>normal</td>
      <td>None</td>
    </tr>
    <tr>
      <th>64</th>
      <td>144</td>
      <td>articuno</td>
      <td>261</td>
      <td>554</td>
      <td>17</td>
      <td>ice</td>
      <td>flying</td>
    </tr>
    <tr>
      <th>65</th>
      <td>145</td>
      <td>zapdos</td>
      <td>261</td>
      <td>526</td>
      <td>16</td>
      <td>electric</td>
      <td>flying</td>
    </tr>
    <tr>
      <th>66</th>
      <td>146</td>
      <td>moltres</td>
      <td>261</td>
      <td>600</td>
      <td>20</td>
      <td>fire</td>
      <td>flying</td>
    </tr>
    <tr>
      <th>67</th>
      <td>149</td>
      <td>dragonite</td>
      <td>270</td>
      <td>2100</td>
      <td>22</td>
      <td>dragon</td>
      <td>flying</td>
    </tr>
    <tr>
      <th>68</th>
      <td>150</td>
      <td>mewtwo</td>
      <td>306</td>
      <td>1220</td>
      <td>20</td>
      <td>psychic</td>
      <td>None</td>
    </tr>
    <tr>
      <th>69</th>
      <td>151</td>
      <td>mew</td>
      <td>270</td>
      <td>40</td>
      <td>4</td>
      <td>psychic</td>
      <td>None</td>
    </tr>
  </tbody>
</table>
<p>70 rows × 7 columns</p>
</div>




```python
q2 = 'select id, name, type1, type2 from pokemon where type1 == "water" or type2 == "water"'
pd.read_sql(q2, cnx)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>name</th>
      <th>type1</th>
      <th>type2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7</td>
      <td>squirtle</td>
      <td>water</td>
      <td>None</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8</td>
      <td>wartortle</td>
      <td>water</td>
      <td>None</td>
    </tr>
    <tr>
      <th>2</th>
      <td>9</td>
      <td>blastoise</td>
      <td>water</td>
      <td>None</td>
    </tr>
    <tr>
      <th>3</th>
      <td>54</td>
      <td>psyduck</td>
      <td>water</td>
      <td>None</td>
    </tr>
    <tr>
      <th>4</th>
      <td>55</td>
      <td>golduck</td>
      <td>water</td>
      <td>None</td>
    </tr>
    <tr>
      <th>5</th>
      <td>60</td>
      <td>poliwag</td>
      <td>water</td>
      <td>None</td>
    </tr>
    <tr>
      <th>6</th>
      <td>61</td>
      <td>poliwhirl</td>
      <td>water</td>
      <td>None</td>
    </tr>
    <tr>
      <th>7</th>
      <td>62</td>
      <td>poliwrath</td>
      <td>water</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>8</th>
      <td>72</td>
      <td>tentacool</td>
      <td>water</td>
      <td>poison</td>
    </tr>
    <tr>
      <th>9</th>
      <td>73</td>
      <td>tentacruel</td>
      <td>water</td>
      <td>poison</td>
    </tr>
    <tr>
      <th>10</th>
      <td>79</td>
      <td>slowpoke</td>
      <td>water</td>
      <td>psychic</td>
    </tr>
    <tr>
      <th>11</th>
      <td>80</td>
      <td>slowbro</td>
      <td>water</td>
      <td>psychic</td>
    </tr>
    <tr>
      <th>12</th>
      <td>86</td>
      <td>seel</td>
      <td>water</td>
      <td>None</td>
    </tr>
    <tr>
      <th>13</th>
      <td>87</td>
      <td>dewgong</td>
      <td>water</td>
      <td>ice</td>
    </tr>
    <tr>
      <th>14</th>
      <td>90</td>
      <td>shellder</td>
      <td>water</td>
      <td>None</td>
    </tr>
    <tr>
      <th>15</th>
      <td>91</td>
      <td>cloyster</td>
      <td>water</td>
      <td>ice</td>
    </tr>
    <tr>
      <th>16</th>
      <td>98</td>
      <td>krabby</td>
      <td>water</td>
      <td>None</td>
    </tr>
    <tr>
      <th>17</th>
      <td>99</td>
      <td>kingler</td>
      <td>water</td>
      <td>None</td>
    </tr>
    <tr>
      <th>18</th>
      <td>116</td>
      <td>horsea</td>
      <td>water</td>
      <td>None</td>
    </tr>
    <tr>
      <th>19</th>
      <td>117</td>
      <td>seadra</td>
      <td>water</td>
      <td>None</td>
    </tr>
    <tr>
      <th>20</th>
      <td>118</td>
      <td>goldeen</td>
      <td>water</td>
      <td>None</td>
    </tr>
    <tr>
      <th>21</th>
      <td>119</td>
      <td>seaking</td>
      <td>water</td>
      <td>None</td>
    </tr>
    <tr>
      <th>22</th>
      <td>120</td>
      <td>staryu</td>
      <td>water</td>
      <td>None</td>
    </tr>
    <tr>
      <th>23</th>
      <td>121</td>
      <td>starmie</td>
      <td>water</td>
      <td>psychic</td>
    </tr>
    <tr>
      <th>24</th>
      <td>129</td>
      <td>magikarp</td>
      <td>water</td>
      <td>None</td>
    </tr>
    <tr>
      <th>25</th>
      <td>130</td>
      <td>gyarados</td>
      <td>water</td>
      <td>flying</td>
    </tr>
    <tr>
      <th>26</th>
      <td>131</td>
      <td>lapras</td>
      <td>water</td>
      <td>ice</td>
    </tr>
    <tr>
      <th>27</th>
      <td>134</td>
      <td>vaporeon</td>
      <td>water</td>
      <td>None</td>
    </tr>
    <tr>
      <th>28</th>
      <td>138</td>
      <td>omanyte</td>
      <td>rock</td>
      <td>water</td>
    </tr>
    <tr>
      <th>29</th>
      <td>139</td>
      <td>omastar</td>
      <td>rock</td>
      <td>water</td>
    </tr>
    <tr>
      <th>30</th>
      <td>140</td>
      <td>kabuto</td>
      <td>rock</td>
      <td>water</td>
    </tr>
    <tr>
      <th>31</th>
      <td>141</td>
      <td>kabutops</td>
      <td>rock</td>
      <td>water</td>
    </tr>
  </tbody>
</table>
</div>




```python
q3 = 'select type1, avg(weight) from pokemon group by type1 order by avg(weight) desc'
pd.read_sql(q3, cnx)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>type1</th>
      <th>avg(weight)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>rock</td>
      <td>876.111111</td>
    </tr>
    <tr>
      <th>1</th>
      <td>dragon</td>
      <td>766.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>water</td>
      <td>579.678571</td>
    </tr>
    <tr>
      <th>3</th>
      <td>fighting</td>
      <td>542.857143</td>
    </tr>
    <tr>
      <th>4</th>
      <td>psychic</td>
      <td>515.625000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>normal</td>
      <td>500.863636</td>
    </tr>
    <tr>
      <th>6</th>
      <td>fire</td>
      <td>480.250000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>ice</td>
      <td>480.000000</td>
    </tr>
    <tr>
      <th>8</th>
      <td>ground</td>
      <td>452.625000</td>
    </tr>
    <tr>
      <th>9</th>
      <td>electric</td>
      <td>317.888889</td>
    </tr>
    <tr>
      <th>10</th>
      <td>grass</td>
      <td>279.916667</td>
    </tr>
    <tr>
      <th>11</th>
      <td>poison</td>
      <td>273.142857</td>
    </tr>
    <tr>
      <th>12</th>
      <td>fairy</td>
      <td>237.500000</td>
    </tr>
    <tr>
      <th>13</th>
      <td>bug</td>
      <td>229.916667</td>
    </tr>
    <tr>
      <th>14</th>
      <td>ghost</td>
      <td>135.666667</td>
    </tr>
  </tbody>
</table>
</div>




```python
q4 = 'select pokemon.name, type2, "2xdamage" from pokemon join types on pokemon.type2 = types.name'
pd.read_sql(q4, cnx)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>type2</th>
      <th>2xdamage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>bulbasaur</td>
      <td>poison</td>
      <td>grass</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ivysaur</td>
      <td>poison</td>
      <td>grass</td>
    </tr>
    <tr>
      <th>2</th>
      <td>venusaur</td>
      <td>poison</td>
      <td>grass</td>
    </tr>
    <tr>
      <th>3</th>
      <td>charizard</td>
      <td>flying</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>4</th>
      <td>butterfree</td>
      <td>flying</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>5</th>
      <td>weedle</td>
      <td>poison</td>
      <td>grass</td>
    </tr>
    <tr>
      <th>6</th>
      <td>kakuna</td>
      <td>poison</td>
      <td>grass</td>
    </tr>
    <tr>
      <th>7</th>
      <td>beedrill</td>
      <td>poison</td>
      <td>grass</td>
    </tr>
    <tr>
      <th>8</th>
      <td>pidgey</td>
      <td>flying</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>9</th>
      <td>pidgeotto</td>
      <td>flying</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>10</th>
      <td>pidgeot</td>
      <td>flying</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>11</th>
      <td>spearow</td>
      <td>flying</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>12</th>
      <td>fearow</td>
      <td>flying</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>13</th>
      <td>nidoqueen</td>
      <td>ground</td>
      <td>poison</td>
    </tr>
    <tr>
      <th>14</th>
      <td>nidoking</td>
      <td>ground</td>
      <td>poison</td>
    </tr>
    <tr>
      <th>15</th>
      <td>jigglypuff</td>
      <td>fairy</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>16</th>
      <td>wigglytuff</td>
      <td>fairy</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>17</th>
      <td>zubat</td>
      <td>flying</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>18</th>
      <td>golbat</td>
      <td>flying</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>19</th>
      <td>oddish</td>
      <td>poison</td>
      <td>grass</td>
    </tr>
    <tr>
      <th>20</th>
      <td>gloom</td>
      <td>poison</td>
      <td>grass</td>
    </tr>
    <tr>
      <th>21</th>
      <td>vileplume</td>
      <td>poison</td>
      <td>grass</td>
    </tr>
    <tr>
      <th>22</th>
      <td>paras</td>
      <td>grass</td>
      <td>ground</td>
    </tr>
    <tr>
      <th>23</th>
      <td>parasect</td>
      <td>grass</td>
      <td>ground</td>
    </tr>
    <tr>
      <th>24</th>
      <td>venonat</td>
      <td>poison</td>
      <td>grass</td>
    </tr>
    <tr>
      <th>25</th>
      <td>venomoth</td>
      <td>poison</td>
      <td>grass</td>
    </tr>
    <tr>
      <th>26</th>
      <td>poliwrath</td>
      <td>fighting</td>
      <td>normal</td>
    </tr>
    <tr>
      <th>27</th>
      <td>bellsprout</td>
      <td>poison</td>
      <td>grass</td>
    </tr>
    <tr>
      <th>28</th>
      <td>weepinbell</td>
      <td>poison</td>
      <td>grass</td>
    </tr>
    <tr>
      <th>29</th>
      <td>victreebel</td>
      <td>poison</td>
      <td>grass</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>37</th>
      <td>magnemite</td>
      <td>steel</td>
      <td>rock</td>
    </tr>
    <tr>
      <th>38</th>
      <td>magneton</td>
      <td>steel</td>
      <td>rock</td>
    </tr>
    <tr>
      <th>39</th>
      <td>farfetchd</td>
      <td>flying</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>40</th>
      <td>doduo</td>
      <td>flying</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>41</th>
      <td>dodrio</td>
      <td>flying</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>42</th>
      <td>dewgong</td>
      <td>ice</td>
      <td>flying</td>
    </tr>
    <tr>
      <th>43</th>
      <td>cloyster</td>
      <td>ice</td>
      <td>flying</td>
    </tr>
    <tr>
      <th>44</th>
      <td>gastly</td>
      <td>poison</td>
      <td>grass</td>
    </tr>
    <tr>
      <th>45</th>
      <td>haunter</td>
      <td>poison</td>
      <td>grass</td>
    </tr>
    <tr>
      <th>46</th>
      <td>gengar</td>
      <td>poison</td>
      <td>grass</td>
    </tr>
    <tr>
      <th>47</th>
      <td>onix</td>
      <td>ground</td>
      <td>poison</td>
    </tr>
    <tr>
      <th>48</th>
      <td>exeggcute</td>
      <td>psychic</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>49</th>
      <td>exeggutor</td>
      <td>psychic</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>50</th>
      <td>rhyhorn</td>
      <td>rock</td>
      <td>flying</td>
    </tr>
    <tr>
      <th>51</th>
      <td>rhydon</td>
      <td>rock</td>
      <td>flying</td>
    </tr>
    <tr>
      <th>52</th>
      <td>starmie</td>
      <td>psychic</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>53</th>
      <td>mr-mime</td>
      <td>fairy</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>54</th>
      <td>scyther</td>
      <td>flying</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>55</th>
      <td>jynx</td>
      <td>psychic</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>56</th>
      <td>gyarados</td>
      <td>flying</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>57</th>
      <td>lapras</td>
      <td>ice</td>
      <td>flying</td>
    </tr>
    <tr>
      <th>58</th>
      <td>omanyte</td>
      <td>water</td>
      <td>ground</td>
    </tr>
    <tr>
      <th>59</th>
      <td>omastar</td>
      <td>water</td>
      <td>ground</td>
    </tr>
    <tr>
      <th>60</th>
      <td>kabuto</td>
      <td>water</td>
      <td>ground</td>
    </tr>
    <tr>
      <th>61</th>
      <td>kabutops</td>
      <td>water</td>
      <td>ground</td>
    </tr>
    <tr>
      <th>62</th>
      <td>aerodactyl</td>
      <td>flying</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>63</th>
      <td>articuno</td>
      <td>flying</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>64</th>
      <td>zapdos</td>
      <td>flying</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>65</th>
      <td>moltres</td>
      <td>flying</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>66</th>
      <td>dragonite</td>
      <td>flying</td>
      <td>fighting</td>
    </tr>
  </tbody>
</table>
<p>67 rows × 3 columns</p>
</div>




```python
q5 = 'select type1, count(*), min(height), max(height), min(weight), max(weight), "0.5xdamage" from pokemon \
        join types on pokemon.type1 = types.name \
        group by type1 \
        order by count(*) desc limit 5'
pd.read_sql(q5, cnx)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>type1</th>
      <th>count(*)</th>
      <th>min(height)</th>
      <th>max(height)</th>
      <th>min(weight)</th>
      <th>max(weight)</th>
      <th>0.5xdamage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>water</td>
      <td>28</td>
      <td>3</td>
      <td>65</td>
      <td>40</td>
      <td>2350</td>
      <td>steel</td>
    </tr>
    <tr>
      <th>1</th>
      <td>normal</td>
      <td>22</td>
      <td>3</td>
      <td>22</td>
      <td>18</td>
      <td>4600</td>
      <td>None</td>
    </tr>
    <tr>
      <th>2</th>
      <td>poison</td>
      <td>14</td>
      <td>4</td>
      <td>35</td>
      <td>10</td>
      <td>650</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>3</th>
      <td>bug</td>
      <td>12</td>
      <td>3</td>
      <td>15</td>
      <td>29</td>
      <td>560</td>
      <td>fighting</td>
    </tr>
    <tr>
      <th>4</th>
      <td>fire</td>
      <td>12</td>
      <td>6</td>
      <td>20</td>
      <td>85</td>
      <td>1550</td>
      <td>bug</td>
    </tr>
  </tbody>
</table>
</div>



## Section 4: Web Scraping

### Accessing Data Using BeautifulSoup

Use BeautifulSoup to get quotes, authors, and tags from [Quotes to Read](http://quotes.toscrape.com/).

First go to the site and inspect the page, look at what links there are and how the entire site is structured.

1. Get the first author and the path for the author's page as a tuple from the [homepage](http://quotes.toscrape.com/).


```python
# Make a get request to retrieve the page
html_page = requests.get('http://quotes.toscrape.com/') 
# Pass the page contents to beautiful soup for parsing
soup = BeautifulSoup(html_page.content, 'html.parser')

# Your code here

```


```python
""" SOLUTION: data for one author """

author = soup.find('small')
author.find_next_siblings()[0].get('href')
(author.text, author.find_next_siblings()[0].get('href'))
```




    ('Albert Einstein', '/author/Albert-Einstein')



2. Write a function to get **all** the authors and href links for the authors from the [homepage](http://quotes.toscrape.com/)



```python
def authors(url):
    '''
    input: url
    
    return: a dictionary of of authors and their urls
            {'author_1':'url_of_author_1', 'author_2':'url_of_author_2' ...}
    '''
    pass
```


```python
""" SOLUTION: data for all the authors on a page """

def authors(url):
    # Make a get request to retrieve the page
    html_page = requests.get(url) 
    # Pass the page contents to beautiful soup for parsing
    soup = BeautifulSoup(html_page.content, 'html.parser')
    authors = soup.find_all('small')
    author_dictionary = {}
    for author in authors:
        author_dictionary[author.text] = author.find_next_siblings()[0].get('href')
    return author_dictionary
```


```python
# run this cell to test the function
print(authors('http://quotes.toscrape.com/'))
print('\n')
print(authors('http://quotes.toscrape.com/page/3'))
```

    {'Albert Einstein': '/author/Albert-Einstein', 'J.K. Rowling': '/author/J-K-Rowling', 'Jane Austen': '/author/Jane-Austen', 'Marilyn Monroe': '/author/Marilyn-Monroe', 'André Gide': '/author/Andre-Gide', 'Thomas A. Edison': '/author/Thomas-A-Edison', 'Eleanor Roosevelt': '/author/Eleanor-Roosevelt', 'Steve Martin': '/author/Steve-Martin'}
    
    
    {'Pablo Neruda': '/author/Pablo-Neruda', 'Ralph Waldo Emerson': '/author/Ralph-Waldo-Emerson', 'Mother Teresa': '/author/Mother-Teresa', 'Garrison Keillor': '/author/Garrison-Keillor', 'Jim Henson': '/author/Jim-Henson', 'Dr. Seuss': '/author/Dr-Seuss', 'Albert Einstein': '/author/Albert-Einstein', 'J.K. Rowling': '/author/J-K-Rowling', 'Bob Marley': '/author/Bob-Marley'}


### Pagination

3. Get the first author on each of the first 5 pages of quotes. You can get to the next page with the next button at the bottom of the homepage.



```python
# Your code here

```


```python
""" SOLUTION: get_some_quotes """

for i in range(1,6):
    html_page = requests.get(f'http://quotes.toscrape.com/page/{i}/')
    soup = BeautifulSoup(html_page.content, 'html.parser')
    author = soup.find('small')
    print(author.text)
```

    Albert Einstein
    Marilyn Monroe
    Pablo Neruda
    Dr. Seuss
    George R.R. Martin


4. Write a function to get all of the quotes from a page.


```python
def get_some_quotes(url):
    '''
    input: url, number of pages to scrap (just scrape the home page if no argument is passed in)
    
    return: a list of dictionaries of quotes with their attributes
            [{'quote':'quote_1_text', 'author':'url_of_author_1'}, 
            {'quote':'quote_2_text', 'author':'url_of_author_2', 'quote_tags':[list_of_quote_2_tags]}, ...]
    '''
    pass
```


```python
""" SOLUTION: get_some_quotes """

def get_some_quotes(url):
    # Make a get request to retrieve the page
    html_page = requests.get(url) 
    # Pass the page contents to beautiful soup for parsing
    soup = BeautifulSoup(html_page.content, 'html.parser')
        
    list_quotes = []
    for i in soup.find_all(class_="quote"):
        quotes = {}
        quote = (i.find(class_="text").text)
        quotes['quote'] = quote
        list_quotes.append(quotes)
        author = i.find(class_ = "author").text
        quotes['author'] = author
    return list_quotes
```


```python
# set the function to a variable to use later
quotes_for_mongo = get_some_quotes('http://quotes.toscrape.com/' )
quotes_for_mongo
```




    [{'quote': '“The world as we have created it is a process of our thinking. It cannot be changed without changing our thinking.”',
      'author': 'Albert Einstein'},
     {'quote': '“It is our choices, Harry, that show what we truly are, far more than our abilities.”',
      'author': 'J.K. Rowling'},
     {'quote': '“There are only two ways to live your life. One is as though nothing is a miracle. The other is as though everything is a miracle.”',
      'author': 'Albert Einstein'},
     {'quote': '“The person, be it gentleman or lady, who has not pleasure in a good novel, must be intolerably stupid.”',
      'author': 'Jane Austen'},
     {'quote': "“Imperfection is beauty, madness is genius and it's better to be absolutely ridiculous than absolutely boring.”",
      'author': 'Marilyn Monroe'},
     {'quote': '“Try not to become a man of success. Rather become a man of value.”',
      'author': 'Albert Einstein'},
     {'quote': '“It is better to be hated for what you are than to be loved for what you are not.”',
      'author': 'André Gide'},
     {'quote': "“I have not failed. I've just found 10,000 ways that won't work.”",
      'author': 'Thomas A. Edison'},
     {'quote': "“A woman is like a tea bag; you never know how strong it is until it's in hot water.”",
      'author': 'Eleanor Roosevelt'},
     {'quote': '“A day without sunshine is like, you know, night.”',
      'author': 'Steve Martin'}]



## Part 5: MongoDB

To do this section open a connection to a mongo database in the terminal, using `mongod` You will **create**, **update**, and **read** from a mongo database.

Create and connect to a mongo database.


```python
myclient = pymongo.MongoClient("mongodb://127.0.0.1:27017/")
mydb = myclient['quote_database']
```


```python
mycollection = mydb['quote_collection']
```

1. Add the quotes from `get_some_quotes` for the [homepage](http://quotes.toscrape.com/) or use the JSON file `quotes.json` for this section. To verify this get the resulting _ids back from the `results` variable.


```python
# if not using  the get_some_quotes function read in the JSON file and set it to variable data

with open(r"data/quotes.json", "r") as r:
    data = json.load(r)
```


```python
# results is variable th
results = None
```


```python
""" SOLUTION:  for adding data in the database"""

### add the data from the JSON file
results = mycollection.insert_many(data)

### add the data from the get_some_quotes function
# results = mycollection.insert_many(quotes_for_mongo)

# check they are in the database
results.inserted_ids
```

2. Query the database for all the quotes by `'Albert Einstein'`.


```python
q1 = None
```


```python
""" SOLUTION: data for Albert Einstein quotes """

q1 = mycollection.find({'author':'Albert Einstein'})
for x in q1:
    print(x)
```

    {'_id': ObjectId('5d278cb2b454d4cdb483e8b0'), 'quote': '“The world as we have created it is a process of our thinking. It cannot be changed without changing our thinking.”', 'author': 'Albert Einstein'}
    {'_id': ObjectId('5d278cb2b454d4cdb483e8b2'), 'quote': '“There are only two ways to live your life. One is as though nothing is a miracle. The other is as though everything is a miracle.”', 'author': 'Albert Einstein'}
    {'_id': ObjectId('5d278cb2b454d4cdb483e8b5'), 'quote': '“Try not to become a man of success. Rather become a man of value.”', 'author': 'Albert Einstein'}


3. Update Steve Martin's quote with the tags for the quote stored in the variable `steve_martin_tags`.


```python
steve_martin_tags = {'quote_tags': ['change', 'deep-thoughts', 'thinking', 'world']}
update_steve = None
first_quote_tags = None

```


```python
""" SOLUTION: data for Steve Martin tags """

update_steve = {'author': 'Steve Martin'}
steve_quote_tags = {'$set':steven_martin_tags}

mycollection.update_one(update_steve, steve_quote_tags)
```




    <pymongo.results.UpdateResult at 0x120852b88>



4. Query the database to confirm that  `'Steve Martin'` is updated with `steve_martin_tags`.


```python
q2 = None
```


```python
""" SOLUTION: data for Steve Martin tags query """

q2 = mycollection.find({'author': 'Steve Martin'})
for item in q2:
    print(item)
```

    {'_id': ObjectId('5d278cb2b454d4cdb483e8b9'), 'quote': '“A day without sunshine is like, you know, night.”', 'author': 'Steve Martin', 'quote_tags': ['change', 'deep-thoughts', 'thinking', 'world']}

