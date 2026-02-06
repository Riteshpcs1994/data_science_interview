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




