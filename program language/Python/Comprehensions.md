
## list 
```
output_list = [output_exp for var in input_list if (var satisfies this condition)]
```

## Dictionary

迭代dict
```
output_dict = {key:value for (key, value) in iterable if (key, value satisfy this condition)}
```

迭代 list
```
{row['id']:row for row in list}

```


# set 
```
output_list = {output_exp for var in input_list if (var satisfies this condition)}
```

# Generator comprehensions

```

input_list = [1, 2, 3, 4, 4, 5, 6, 7, 7]
  
output_gen = (var for var in input_list if var % 2 == 0)
  
print("Output values using generator comprehensions:", end = ' ')
  
for var in output_gen:
    print(var, end = ' ')
```