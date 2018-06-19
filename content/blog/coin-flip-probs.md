---
title: "Coin Flip Probability with Python"
date: 2018-06-18T23:30:12-05:00
draft: false
---

I'm writing up my dissertation...but occasionally I need a distraction. Don't get me wrong, I find studying hate speech very fascinating, but in all honesty, it gets to be a bit much sometimes. The world can be a depressing place. Plus, it's a dissertation; distractions are welcome in any flavor.

Today my distraction came in the form of a Tweet by David Robinson demonstrating how flipping a coin and getting a heads and then another heads takes 6 flips on average while a heads then a tails only takes 4.

{{< tweet 1008409373423611904 >}}

He did this using `tidyverse` functions and then using base-`R` matrix operations. Well, I wanted to create the `Python` version because of said dissertation. I did so by creating a set of functions. 

The first is simply a function to simulate flipping a fair coin...

```python
import numpy as np

def flip_coin():
    """Simulate flipping a coin.
    
    Returns
    -------
    str
        "H" for heads/ "T" for tails.
    """
    flip = np.random.binomial(1, .5, 1)
    if flip[0] == 1:
        side = "H"
    else:
        side = "T"
    return side
```

Then I need a function to flip the coin multiple times and to stop only when a certain sequence of sides were met. In other words, stop when two heads were flipped in a row. From this, I want the number of times it took to achieve this sequence to be returned.

```python
def flip_condition(stop_condition=['H', 'T'], print_opt=False):
    """Flip coin until flip pattern is met.
    
    Parameters
    ----------
    stop_condition: list
        The sequence of flips to be matched before flipping stops.
    
    print_opt: bool
        Option to print the sequence of flips.
        
    Returns
    -------
    int
        The number of flips it took to match the pattern.
    """
    flip_list = []
    
    current_index = 0
    current_condition = None
    while current_condition != stop_condition:
        flip_list.append(flip_coin())
        if len(flip_list) >= len(stop_condition):
            current_condition = [flip_list[i] for i in range(current_index - len(stop_condition) +1 , current_index + 1)]
        else:
            pass
        current_index +=1
        
    if print_opt:
        print(flip_list)
    return current_index 
```

This also includes an option to print the sequence (in case you want to check my programming...I would 😜). And then I just run it many times and take the average for both conditions.

```python
mean_ht = np.mean([flip_condition(['H', 'T']) for i in range(10000)])
mean_hh = np.mean([flip_condition(['H','H']) for i in range(10000)])

print("Average # of flips to achieve heads and then heads again: {}".format(mean_hh))
print("Average # of flips to achieve heads and then tails: {}".format(mean_ht))

# Average # of flips to achieve heads and then heads again: 6.0081
# Average # of flips to achieve heads and then tails: 3.9829
```

Looks like probability holds up in `Python`! Oh, but I also created the function to capture any pattern. How about heads, tails, heads?

```python
np.mean([flip_condition(['H', 'T', 'H']) for i in range(10000)])

# 9.9231
```

or heads, heads, heads

```python
np.mean([flip_condition(['H', 'H', 'H']) for i in range(10000)])

# 14.1544
```

Well that was neat! 🦖🦕

If you want to play around with the code, I've posted in this notebook [here](https://github.com/jcbain/fun_side_projects/blob/master/hh_probs/coin_flip_props.ipynb)

