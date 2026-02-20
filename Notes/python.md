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








