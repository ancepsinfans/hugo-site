---
title: "Guided Case Study: Basic Python"
date: 2023-11-16T06:00:23+06:00
description: Mini-project for the end of the first unit of the Data Science program
theme: Toha
---

## Datasets

[gaming_consoles.csv](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/90f1bbbf-e3a9-4a77-b562-c998d5dd2d1d/gaming_consoles.csv)

---

Welcome to the culminating challenge of the sprint! You’ve mastered an array of essential concepts and learned basic Python syntax, and now it’s time to work on a Guided Case Study that will bridge theory and practice, transforming your knowledge into tangible problem-solving abilities.

You’ll work on a set of tasks and quizzes aimed at analyzing data designed in a way so that you can get hands-on experience and solve real-world problems like those you’ll be handling in your future career. Start when you’re ready, feel free to take breaks and work at your own tempo, and remember, each challenge you overcome is a stepping stone toward becoming a proficient Python programmer!

## Scenario

A local shop buys, repairs, and sells discontinued electronics. One of their biggest earners is old gaming consoles. The shop has collected historical sales data about these discontinued consoles in order to set prices and help prioritize which ones to repair. Let's take a look at the dataset:

| console          | company          | release_year | discontinued_year | release_price | units_sold |
| ---------------- | ---------------- | ------------ | ----------------- | ------------- | ---------- |
| NES              | Nintendo         | 1985         | 1995              | 179           | 61910000   |
| Game Boy         | Nintendo         | 1989         | 2003              | 89.99         | 118690000  |
| SNES             | Nintendo         | 1990         | 2003              | 199           | 49100000   |
| Virtual Boy      | Nintendo         | 1995         | 1996              | 179.95        | 770000     |
| Game Boy Advance | Nintendo         | 2001         | 2010              | 99.99         | 81510000   |
| Atari 2600       | Atari            | 1977         | 1992              | 199           | 30000000   |
| Sega Genesis     | Sega             | 1988         | 1997              | 189           | 30750000   |
| Game Gear        | Sega             | 1990         | 1997              | 149.99        | 10620000   |
| Sega CD          | Sega             | 1991         | 1996              | 299           | 2240000    |
| 3DO              | The 3DO Company  | 1993         | 1996              | 699.99        | 2000000    |
| PlayStation      | Sony Electronics | 1994         | 2006              | 299           | 102490000  |
| PlayStation 2    | Sony Electronics | 2000         | 2013              | 299           | 155000000  |

This table contains six columns:

- console — the type of gaming console
- company — the company that manufactured it
- release_year — the year it was first introduced to the market
- discontinued_year — the year the company stopped manufacturing it
- release_price — the cost of the console at its release
- units_sold — the number of consoles sold over its product run

This dataset is a great opportunity to practice working with complex lists in Python while analyzing the relative success of these old gaming consoles.

## Task 1

Here, the dataset is presented to you as a nested list saved in the variable `console_data`. In future lessons, you'll learn how to load large datasets from files in one line of code. But for now, we're giving you the data in the precode already saved into a variable.

Let's start out by printing our data to the screen in a nice-looking table format. We can do this by printing each row on its own line and each element at a consistent spacing. This requires using a nested for loop and an f-string in our `print()` function.

Print the output so that each element is left-aligned and has a fixed string length of 20 characters.

**Hint**

Your code needs to have two for loops, with one loop nested inside the body of the other. The body of the inner loop should contain one line of code with a `print()` function that prints an f-string (`f'{...}'`) where the `...` is replaced with your loop variable and the correct formatting parameters. After the inner loop, print a new line in the body of the outer loop using `print()` with no arguments.

**Success text**

Look how beautiful that data is. And so much of it! There are other ways to neatly display data on your screen in Python — you'll learn more about those in the future as you start to work with larger datasets.

**Precode**

```python
console_data = [['NES', 'Nintendo', 1985, 1995, 179.0, 61910000],
 ['Game Boy', 'Nintendo', 1989, 2003, 89.99, 118690000],
 ['SNES', 'Nintendo', 1990, 2003, 199.0, 49100000],
 ['Virtual Boy', 'Nintendo', 1995, 1996, 179.95, 770000],
 ['Game Boy Advance', 'Nintendo', 2001, 2010, 99.99, 81510000],
 ['Atari 2600', 'Atari', 1977, 1992, 199.0, 30000000],
 ['Sega Genesis', 'Sega', 1988, 1997, 189.0, 30750000],
 ['Game Gear', 'Sega', 1990, 1997, 149.99, 10620000],
 ['Sega CD', 'Sega', 1991, 1996, 299.0, 2240000],
 ['3DO', 'The 3DO Company', 1993, 1996, 699.99, 2000000],
 ['PlayStation', 'Sony Electronics', 1994, 2006, 299.0, 102490000],
 ['PlayStation 2', 'Sony Electronics', 2000, 2013, 299.0, 155000000]]

# write your code here
```

**Solution**

```python
console_data = [['NES', 'Nintendo', 1985, 1995, 179.0, 61910000],
 ['Game Boy', 'Nintendo', 1989, 2003, 89.99, 118690000],
 ['SNES', 'Nintendo', 1990, 2003, 199.0, 49100000],
 ['Virtual Boy', 'Nintendo', 1995, 1996, 179.95, 770000],
 ['Game Boy Advance', 'Nintendo', 2001, 2010, 99.99, 81510000],
 ['Atari 2600', 'Atari', 1977, 1992, 199.0, 30000000],
 ['Sega Genesis', 'Sega', 1988, 1997, 189.0, 30750000],
 ['Game Gear', 'Sega', 1990, 1997, 149.99, 10620000],
 ['Sega CD', 'Sega', 1991, 1996, 299.0, 2240000],
 ['3DO', 'The 3DO Company', 1993, 1996, 699.99, 2000000],
 ['PlayStation', 'Sony Electronics', 1994, 2006, 299.0, 102490000],
 ['PlayStation 2', 'Sony Electronics', 2000, 2013, 299.0, 155000000]]

for row in console_data:
    for elem in row:
        print(f'{elem:<20}', end='')
    print()
```

## Task 2

Now let's go about retrieving specific pieces of data from the table. Use list indexing to print out the row containing data about the Sega CD. Don't worry about formatting the output, just print the whole sublist. Then, on another line, use indexing again to print out the number of Game Boy consoles that were sold over its lifetime.

**Hint**

To print the Sega CD row, use single square brackets to select the correct index in `console_data`. To print the number of Game Boy consoles sold, use double square brackets to select the correct element from the sublist containing Game Boy data. The number of units sold is the last element in each sublist.

**Success text**

Good job. You can find any piece of information you need from this data structure of nested lists. There sure were a lot of Game Boys out there.

**Precode**

```python
console_data = [['NES', 'Nintendo', 1985, 1995, 179.0, 61910000],
 ['Game Boy', 'Nintendo', 1989, 2003, 89.99, 118690000],
 ['SNES', 'Nintendo', 1990, 2003, 199.0, 49100000],
 ['Virtual Boy', 'Nintendo', 1995, 1996, 179.95, 770000],
 ['Game Boy Advance', 'Nintendo', 2001, 2010, 99.99, 81510000],
 ['Atari 2600', 'Atari', 1977, 1992, 199.0, 30000000],
 ['Sega Genesis', 'Sega', 1988, 1997, 189.0, 30750000],
 ['Game Gear', 'Sega', 1990, 1997, 149.99, 10620000],
 ['Sega CD', 'Sega', 1991, 1996, 299.0, 2240000],
 ['3DO', 'The 3DO Company', 1993, 1996, 699.99, 2000000],
 ['PlayStation', 'Sony Electronics', 1994, 2006, 299.0, 102490000],
 ['PlayStation 2', 'Sony Electronics', 2000, 2013, 299.0, 155000000]]

# write your code here
```

**Solution**

```python
console_data = [['NES', 'Nintendo', 1985, 1995, 179.0, 61910000],
 ['Game Boy', 'Nintendo', 1989, 2003, 89.99, 118690000],
 ['SNES', 'Nintendo', 1990, 2003, 199.0, 49100000],
 ['Virtual Boy', 'Nintendo', 1995, 1996, 179.95, 770000],
 ['Game Boy Advance', 'Nintendo', 2001, 2010, 99.99, 81510000],
 ['Atari 2600', 'Atari', 1977, 1992, 199.0, 30000000],
 ['Sega Genesis', 'Sega', 1988, 1997, 189.0, 30750000],
 ['Game Gear', 'Sega', 1990, 1997, 149.99, 10620000],
 ['Sega CD', 'Sega', 1991, 1996, 299.0, 2240000],
 ['3DO', 'The 3DO Company', 1993, 1996, 699.99, 2000000],
 ['PlayStation', 'Sony Electronics', 1994, 2006, 299.0, 102490000],
 ['PlayStation 2', 'Sony Electronics', 2000, 2013, 299.0, 155000000]]

print(console_data[8])
print(console_data[1][5])
```

## **Quiz 1**

In the last two tasks, you printed out the full dataset as well as a single row and a single value. With our dataset stored as a nested list, can we also print out a single column? If so, how would we do that?

- No, because we decided to store the rows as sublists rather than the columns.
  Printing a column is not as straightforward as printing a row, but we can definitely still do it! We just need to use a for loop.
- Yes, by using a for loop to print one element from each sublist.
  That's right! Let's put this into practice in the next task.
- Yes, by using a for loop to print a sublist at each iteration.
  It's true that we can use a for loop to print a single column, but printing a whole sublist in each loop iteration will display values from every column.

## Task 3

Use a for loop to print the first column of the table — the names of the consoles.

**Hint**

Loop over the rows of the table (i.e. the sublists in `console_data`) and print the value at the index that corresponds to the console name in each row. The console names are stored in the first column.

**Success text**

You've got the Python skills to get anything you need from a list of lists!

**Precode**

```python
console_data = [['NES', 'Nintendo', 1985, 1995, 179.0, 61910000],
 ['Game Boy', 'Nintendo', 1989, 2003, 89.99, 118690000],
 ['SNES', 'Nintendo', 1990, 2003, 199.0, 49100000],
 ['Virtual Boy', 'Nintendo', 1995, 1996, 179.95, 770000],
 ['Game Boy Advance', 'Nintendo', 2001, 2010, 99.99, 81510000],
 ['Atari 2600', 'Atari', 1977, 1992, 199.0, 30000000],
 ['Sega Genesis', 'Sega', 1988, 1997, 189.0, 30750000],
 ['Game Gear', 'Sega', 1990, 1997, 149.99, 10620000],
 ['Sega CD', 'Sega', 1991, 1996, 299.0, 2240000],
 ['3DO', 'The 3DO Company', 1993, 1996, 699.99, 2000000],
 ['PlayStation', 'Sony Electronics', 1994, 2006, 299.0, 102490000],
 ['PlayStation 2', 'Sony Electronics', 2000, 2013, 299.0, 155000000]]

# write your code here
```

**Solution**

```python
console_data = [['NES', 'Nintendo', 1985, 1995, 179.0, 61910000],
 ['Game Boy', 'Nintendo', 1989, 2003, 89.99, 118690000],
 ['SNES', 'Nintendo', 1990, 2003, 199.0, 49100000],
 ['Virtual Boy', 'Nintendo', 1995, 1996, 179.95, 770000],
 ['Game Boy Advance', 'Nintendo', 2001, 2010, 99.99, 81510000],
 ['Atari 2600', 'Atari', 1977, 1992, 199.0, 30000000],
 ['Sega Genesis', 'Sega', 1988, 1997, 189.0, 30750000],
 ['Game Gear', 'Sega', 1990, 1997, 149.99, 10620000],
 ['Sega CD', 'Sega', 1991, 1996, 299.0, 2240000],
 ['3DO', 'The 3DO Company', 1993, 1996, 699.99, 2000000],
 ['PlayStation', 'Sony Electronics', 1994, 2006, 299.0, 102490000],
 ['PlayStation 2', 'Sony Electronics', 2000, 2013, 299.0, 155000000]]

for row in console_data:
    print(row[0])
```

## The Big Picture So Far

You have a dataset stored in a nested list. Each sublist represents a row from the table and each element of a sublist corresponds to a column value from the table. You were able to access specific values from the table using single and double indexing, as well as print a row, a column, or even the entire table. Now you can use these skills to perform table calculations and even add new columns to the table!

## Task 4

The last column in the table stores the number of consoles that were sold over the lifetime of the console. How many consoles of all types were sold in total? Calculate this by using a for loop to sum all the values in the units sold column, saving the result in a variable called `total_sold`. Then print `total_sold` to the screen.

**Hint**

Assign the value of 0 to `total_sold` before your for loop. Then write a single for loop to loop over each row in `console_data`. In each loop iteration, use the correct row index to add the number of units sold to `total_sold`. After the for loop, call the `print()` function to print the result stored in `total_sold`.

**Success text**

Over half a billion consoles sold, and that's just for the ones in this dataset! Video games sure are popular. Good job summing a table column. In future courses, you'll learn more advanced techniques to find sums with specific conditions, such as finding the total consoles sold for just Nintendo or just Sega and then comparing them!

**Precode**

```python
console_data = [['NES', 'Nintendo', 1985, 1995, 179.0, 61910000],
 ['Game Boy', 'Nintendo', 1989, 2003, 89.99, 118690000],
 ['SNES', 'Nintendo', 1990, 2003, 199.0, 49100000],
 ['Virtual Boy', 'Nintendo', 1995, 1996, 179.95, 770000],
 ['Game Boy Advance', 'Nintendo', 2001, 2010, 99.99, 81510000],
 ['Atari 2600', 'Atari', 1977, 1992, 199.0, 30000000],
 ['Sega Genesis', 'Sega', 1988, 1997, 189.0, 30750000],
 ['Game Gear', 'Sega', 1990, 1997, 149.99, 10620000],
 ['Sega CD', 'Sega', 1991, 1996, 299.0, 2240000],
 ['3DO', 'The 3DO Company', 1993, 1996, 699.99, 2000000],
 ['PlayStation', 'Sony Electronics', 1994, 2006, 299.0, 102490000],
 ['PlayStation 2', 'Sony Electronics', 2000, 2013, 299.0, 155000000]]

# write your code here
```

**Solution**

```python
console_data = [['NES', 'Nintendo', 1985, 1995, 179.0, 61910000],
 ['Game Boy', 'Nintendo', 1989, 2003, 89.99, 118690000],
 ['SNES', 'Nintendo', 1990, 2003, 199.0, 49100000],
 ['Virtual Boy', 'Nintendo', 1995, 1996, 179.95, 770000],
 ['Game Boy Advance', 'Nintendo', 2001, 2010, 99.99, 81510000],
 ['Atari 2600', 'Atari', 1977, 1992, 199.0, 30000000],
 ['Sega Genesis', 'Sega', 1988, 1997, 189.0, 30750000],
 ['Game Gear', 'Sega', 1990, 1997, 149.99, 10620000],
 ['Sega CD', 'Sega', 1991, 1996, 299.0, 2240000],
 ['3DO', 'The 3DO Company', 1993, 1996, 699.99, 2000000],
 ['PlayStation', 'Sony Electronics', 1994, 2006, 299.0, 102490000],
 ['PlayStation 2', 'Sony Electronics', 2000, 2013, 299.0, 155000000]]

total_sold = 0
for row in console_data:
    total_sold = total_sold + row[5]
print(total_sold)
```



## **Quiz 2**

We want to use this console dataset to compare the popularity and success of each gaming console. But there isn't a particular column that we can use right off the bat, which makes sense because popularity can be subjective. As analysts, we need to create our own metric to represent popularity. Which of the following metrics do you think may be good indicators of console popularity? Check any and all that apply.

- Console lifespan
- Total revenue
- Consoles sold per year

Feedback:

All of these ideas could be decent metrics. Notice how all of them require us to perform calculations between columns in our dataset? Ultimately, the metric we choose will depend on the problem we are trying to solve. And if we aren't sure which metric will be the most useful, we can calculate different metrics and compare them, or use them in tandem.



## Task 5

It makes sense that more popular consoles would tend to have a longer lifespan before being discontinued, so let's calculate the lifespan metric and add it as a new column at the end of the dataset.

To do this, loop over each row in `console_data` and calculate the lifespan in years using the released year and discontinued year columns. Don't forget to append the result to each row in order to create the new column.

We've included a separate for loop in the precode to print your results, but the for loop that calculates the lifespan should come before this one.

**Hint**

Write a single for loop to iterate over each row in `console_data`. In the body of the loop, calculate the lifespan by using the correct row indices to subtract the released year from the discontinued year. Also in the body of the loop, use the `append()` method to append the lifespan to the row sublist. Don't change the for loop already given in the precode.

**Success text**

Great! You've expanded your dataset by creating a column that contains one of your analysis metrics. That last column is the lifespan of each console in years.

**Precode**

```python
console_data = [['NES', 'Nintendo', 1985, 1995, 179.0, 61910000],
 ['Game Boy', 'Nintendo', 1989, 2003, 89.99, 118690000],
 ['SNES', 'Nintendo', 1990, 2003, 199.0, 49100000],
 ['Virtual Boy', 'Nintendo', 1995, 1996, 179.95, 770000],
 ['Game Boy Advance', 'Nintendo', 2001, 2010, 99.99, 81510000],
 ['Atari 2600', 'Atari', 1977, 1992, 199.0, 30000000],
 ['Sega Genesis', 'Sega', 1988, 1997, 189.0, 30750000],
 ['Game Gear', 'Sega', 1990, 1997, 149.99, 10620000],
 ['Sega CD', 'Sega', 1991, 1996, 299.0, 2240000],
 ['3DO', 'The 3DO Company', 1993, 1996, 699.99, 2000000],
 ['PlayStation', 'Sony Electronics', 1994, 2006, 299.0, 102490000],
 ['PlayStation 2', 'Sony Electronics', 2000, 2013, 299.0, 155000000]]

# write your code here

# this code will print your result table
for row in console_data:
    for elem in row:
        print(f'{elem:<20}', end='')
    print()
```


**Solution**

```python
console_data = [['NES', 'Nintendo', 1985, 1995, 179.0, 61910000],
 ['Game Boy', 'Nintendo', 1989, 2003, 89.99, 118690000],
 ['SNES', 'Nintendo', 1990, 2003, 199.0, 49100000],
 ['Virtual Boy', 'Nintendo', 1995, 1996, 179.95, 770000],
 ['Game Boy Advance', 'Nintendo', 2001, 2010, 99.99, 81510000],
 ['Atari 2600', 'Atari', 1977, 1992, 199.0, 30000000],
 ['Sega Genesis', 'Sega', 1988, 1997, 189.0, 30750000],
 ['Game Gear', 'Sega', 1990, 1997, 149.99, 10620000],
 ['Sega CD', 'Sega', 1991, 1996, 299.0, 2240000],
 ['3DO', 'The 3DO Company', 1993, 1996, 699.99, 2000000],
 ['PlayStation', 'Sony Electronics', 1994, 2006, 299.0, 102490000],
 ['PlayStation 2', 'Sony Electronics', 2000, 2013, 299.0, 155000000]]

for row in console_data:
    lifespan = row[3] - row[2]
    row.append(lifespan)

for row in console_data:
    for elem in row:
        print(f'{elem:<20}', end='')
    print()
```

## Task 6

We've successfully calculated our first metric and added it to our dataset as a new column. But the values are all over the place, which makes it cumbersome to compare between consoles. We can fix this by sorting our data!

The code to create the lifespan column from the last task is provided for you here in the precode, as is the code to print your result. Add a line of code to sort `console_data` by the new lifespan column in order from longest to shortest, and save the result in a variable called `sorted_lifespan_data`. We’ve created the `key()` function for you to help you sort the values according to the correct element. Include this in your sorting function like so: `key=key`.

**Hint**

Use the `sorted()` function with three arguments to sort your data: `console_data`, `key=`, and `reverse=`. Use the `key` function in the precode: `key=key`. By default, `sorted()` sorts numerical values from least to greatest, so make sure to use the correct argument to sort in reverse order.

**Success text**

That's quite a range of lifespans. It looks like the Atari is the wise sage of the group and the Virtual Boy is... well, we don't talk about the Virtual Boy.

**Precode**

```python
console_data = [['NES', 'Nintendo', 1985, 1995, 179.0, 61910000],
 ['Game Boy', 'Nintendo', 1989, 2003, 89.99, 118690000],
 ['SNES', 'Nintendo', 1990, 2003, 199.0, 49100000],
 ['Virtual Boy', 'Nintendo', 1995, 1996, 179.95, 770000],
 ['Game Boy Advance', 'Nintendo', 2001, 2010, 99.99, 81510000],
 ['Atari 2600', 'Atari', 1977, 1992, 199.0, 30000000],
 ['Sega Genesis', 'Sega', 1988, 1997, 189.0, 30750000],
 ['Game Gear', 'Sega', 1990, 1997, 149.99, 10620000],
 ['Sega CD', 'Sega', 1991, 1996, 299.0, 2240000],
 ['3DO', 'The 3DO Company', 1993, 1996, 699.99, 2000000],
 ['PlayStation', 'Sony Electronics', 1994, 2006, 299.0, 102490000],
 ['PlayStation 2', 'Sony Electronics', 2000, 2013, 299.0, 155000000]]

for row in console_data:
    lifespan = row[3] - row[2]
    row.append(lifespan)

def key(row):
    return row[-1]

# write your code here

# this code will print your result table
for row in sorted_lifespan_data:
    for elem in row:
        print(f'{elem:<20}', end='')
    print()
```

**Solution**

```python
console_data = [['NES', 'Nintendo', 1985, 1995, 179.0, 61910000],
 ['Game Boy', 'Nintendo', 1989, 2003, 89.99, 118690000],
 ['SNES', 'Nintendo', 1990, 2003, 199.0, 49100000],
 ['Virtual Boy', 'Nintendo', 1995, 1996, 179.95, 770000],
 ['Game Boy Advance', 'Nintendo', 2001, 2010, 99.99, 81510000],
 ['Atari 2600', 'Atari', 1977, 1992, 199.0, 30000000],
 ['Sega Genesis', 'Sega', 1988, 1997, 189.0, 30750000],
 ['Game Gear', 'Sega', 1990, 1997, 149.99, 10620000],
 ['Sega CD', 'Sega', 1991, 1996, 299.0, 2240000],
 ['3DO', 'The 3DO Company', 1993, 1996, 699.99, 2000000],
 ['PlayStation', 'Sony Electronics', 1994, 2006, 299.0, 102490000],
 ['PlayStation 2', 'Sony Electronics', 2000, 2013, 299.0, 155000000]]

for row in console_data:
    lifespan = row[3] - row[2]
    row.append(lifespan)

def key(row):
    return row[-1]

sorted_lifespan_data = sorted(console_data, key=key, reverse=True)

# this code will print your result table
for row in sorted_lifespan_data:
    for elem in row:
        print(f'{elem:<20}', end='')
    print()
```


## The Big Picture So Far

Not only have you shown that you can display your data and select pieces of it using nested list indexing, you've also successfully performed calculations using columns in your dataset. You performed a single-column calculation when you summed the values in the units sold column to determine the total number of all consoles that were sold. And you performed a multi-column calculation when you subtracted the release year column from the discontinued year column to determine the lifespan metric for each console. Finally, you displayed your metric in an easy-to-understand way by sorting the data before printing it out. Now let's put it all together by calculating another metric: adding the result as a column in our table, and sorting the result all in one go!



## Task 7

Calculate a new metric, total revenue, which we will estimate as the product of release price and the total number of units sold (the last two values in each row). Use a for loop over the rows of `console_data` to calculate the total revenue and append the result to the end of each row.

The precode already contains code to sort and print your final result, so leave that as is.

**Hint**

This task is bringing together what you did in the previous two tasks, but with a different metric — so use those two tasks as a template if you get stuck. Your code should have a single for loop that calculates total revenue as the multiplication of the release price and units sold columns for each row in `console_data` and then appends that result to the end of the row.

**Success text**

You have successfully calculated another metric and included the result in your dataset! So, which is a better metric, console lifetime or total revenue? It depends on the problem at hand, but it's always good to have options.

**Precode**

```python
console_data = [['NES', 'Nintendo', 1985, 1995, 179.0, 61910000],
 ['Game Boy', 'Nintendo', 1989, 2003, 89.99, 118690000],
 ['SNES', 'Nintendo', 1990, 2003, 199.0, 49100000],
 ['Virtual Boy', 'Nintendo', 1995, 1996, 179.95, 770000],
 ['Game Boy Advance', 'Nintendo', 2001, 2010, 99.99, 81510000],
 ['Atari 2600', 'Atari', 1977, 1992, 199.0, 30000000],
 ['Sega Genesis', 'Sega', 1988, 1997, 189.0, 30750000],
 ['Game Gear', 'Sega', 1990, 1997, 149.99, 10620000],
 ['Sega CD', 'Sega', 1991, 1996, 299.0, 2240000],
 ['3DO', 'The 3DO Company', 1993, 1996, 699.99, 2000000],
 ['PlayStation', 'Sony Electronics', 1994, 2006, 299.0, 102490000],
 ['PlayStation 2', 'Sony Electronics', 2000, 2013, 299.0, 155000000]]

# write your code here
console_data =

# this code will sort your results
sorted_revenue_data = sorted(console_data, key=lambda row: row[-1], reverse=True)

# this code will print your result table
for row in sorted_revenue_data:
    for elem in row:
        print(f'{elem:<20}', end='')
    print()
```


**Solution**

```python
console_data = [['NES', 'Nintendo', 1985, 1995, 179.0, 61910000],
 ['Game Boy', 'Nintendo', 1989, 2003, 89.99, 118690000],
 ['SNES', 'Nintendo', 1990, 2003, 199.0, 49100000],
 ['Virtual Boy', 'Nintendo', 1995, 1996, 179.95, 770000],
 ['Game Boy Advance', 'Nintendo', 2001, 2010, 99.99, 81510000],
 ['Atari 2600', 'Atari', 1977, 1992, 199.0, 30000000],
 ['Sega Genesis', 'Sega', 1988, 1997, 189.0, 30750000],
 ['Game Gear', 'Sega', 1990, 1997, 149.99, 10620000],
 ['Sega CD', 'Sega', 1991, 1996, 299.0, 2240000],
 ['3DO', 'The 3DO Company', 1993, 1996, 699.99, 2000000],
 ['PlayStation', 'Sony Electronics', 1994, 2006, 299.0, 102490000],
 ['PlayStation 2', 'Sony Electronics', 2000, 2013, 299.0, 155000000]]

for row in console_data:
    total_revenue = row[4] * row[5]
    row.append(total_revenue)

sorted_revenue_data = sorted(console_data, key=lambda row: row[-1], reverse=True)

# this code will print your result table
for row in sorted_revenue_data:
    for elem in row:
        print(f'{elem:<20}', end='')
    print()
```

## Summary

Nested lists are complex data structures that can take some getting used to, but you're getting the hang of it. In future lessons, you'll learn about more sophisticated data structures in Python to store and work with tables, but the skills you learned here will go a long way in helping you work with them effectively. Writing for loops and nested for loops, performing nested list indexing, formatted printing, and column calculations are just some of the skills you used in this guided case study.

You were also introduced to the concept of metrics, which are essential in evaluating your analysis and making informed business decisions. As an analyst, you have to be creative in deciding on your metrics because a good metric depends both on the data you have available and the problem that you're trying to solve.
