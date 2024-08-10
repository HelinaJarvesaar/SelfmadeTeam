# HOMEWORK
**Task: Visualizing the correlation of Attack and Defense variables of two Types: Grass and Water Type 1 Pokémon.**

```py
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

pokemon_df = pd.read_csv("/content/Pokemon.csv")
```

**1. Create two DataFrame Grass and Water**
```py
grass_df = pokemon_df[pokemon_df["Type 1"] == "Grass"]
water_df = pokemon_df[pokemon_df["Type 1"] == "Water"]
```


**2. Create the regression plots for each (Grass and Water)**

VERSION 1
```py
sns.regplot(x='Attack', y='Defense', data=grass_df, marker='x', color='orange', label='Grass Type')
sns.regplot(x='Attack', y='Defense', data=water_df, marker='o', color='green', label='Water Type')

plt.xlabel('Attack')
plt.ylabel('Defense')
plt.title('Regression Plot with Grass and Water Type Pokemons')
plt.legend()
```
![Unknown-6](https://github.com/user-attachments/assets/7281804e-ea7d-4f0c-9d49-b6aa22bec7d9)


VERSION 2
```py
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(25, 8))

sns.regplot(data=grass_df, x='Attack', y='Defense', label = 'Type Grass', marker = 'D', color="SeaGreen", line_kws={'color':'DarkSeaGreen'}, ax=ax1)
ax1.legend()
ax1.set_title('Regression Plot with Pokemon Type1 Grass')

sns.regplot(data=water_df, x='Attack', y='Defense', label = 'Type Water', marker = '*', color="DarkGrey", line_kws={'color':'SlateGray'}, ax=ax2)
ax2.legend()
ax2.set_title('Regression Plot with Pokemon Type1 Water')

plt.show()
```
![Unknown-5](https://github.com/user-attachments/assets/ca3a0b0a-71f6-45c8-a4fc-d157bfcb3b15)


**3. Calculate the Pearson correlation for each DataFrame (variables: Attack and Defense)**
```py
grass_corr = grass_df['Attack'].corr(grass_df['Defense'])
water_corr = water_df['Attack'].corr(water_df['Defense'])

print(f"Pearson correlation for grass type: {grass_corr}")
print(f"Pearson correlation for water type: {water_corr}")
```

<img width="472" alt="Screenshot 2024-08-10 at 14 52 08" src="https://github.com/user-attachments/assets/eb06d081-079d-4353-8944-4ccaa9cb8bab">


#### 4. Explain to each other what do you see and what it means.
