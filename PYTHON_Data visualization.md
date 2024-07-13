```py
import pandas as pd
import matplotlib.pyplot as plt

dataset = pd.read_csv('/content/transaction_dataset.csv')

gender_counts = dataset["Gender"].value_counts(dropna=False)
df_gender_counts = pd.DataFrame({'Gender': gender_counts.index.astype(str), 'Count': gender_counts.values})

plt.bar(df_gender_counts["Gender"], df_gender_counts["Count"], color=["pink", "skyblue", "gray"])

plt.title("Count of Customers by Gender")
plt.xlabel("Gender")
plt.ylabel("Count of Customers")

plt.show()
```

![Unknown](https://github.com/user-attachments/assets/e7d3e5e1-14b4-4777-92db-1d8d5f53b27c)
