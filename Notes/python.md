``` 
transactions["approved_amount"] = np.where(
    transactions["state"] == "approved",
    transactions["amount"],
    0
)
```
```
transactions["approved_amount"] = transactions["amount"].where(
    transactions["state"] == "approved",
    0
)
```

```
df[["class"]][df["student"] >=5] --> Return dataframe

df["class"][df["student"] >=5] --> Return Series

```

```
'str' object does not support item assignment

s[i]= 5 . not possible

```

## What does s.split() do?
s = string
s = "  a good   example "
result_s = "a good example"

```
s.split()
```
- Removes leading spaces
- Removes trailing spaces
- Treats multiple spaces as one separator
- Splits words into a list

👉 Notice:
- No empty strings
- Extra spaces automatically removed
- That’s the magic of split() without arguments.















