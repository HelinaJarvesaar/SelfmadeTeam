# HOMEWORK

1. How many Pokémons are with 'Type 1' == Water as a % of total?

```py
import pandas as pd #analysis
import matplotlib.pyplot as plt

pokemon_df = pd.read_csv('/content/Pokemon.csv')
pokemon_df.head(n=10)

total_number_of_Pokemons = pokemon_df['Type 1'].count()
print(f'Total number of Pokemons: {total_number_of_Pokemons}')

number_of_Type1_Water_Pokemons = pokemon_df[pokemon_df['Type 1'] == 'Water']
print(f'Pokemons with Type1 = Water: {len(number_of_Type1_Water_Pokemons)}')

percentage = (len(number_of_Type1_Water_Pokemons) / total_number_of_Pokemons) * 100
print(f'Pokemons with Type 1 = Water as a % of total: {percentage:.2f}%')
```
<img width="386" alt="Screenshot 2024-08-03 at 16 05 03" src="https://github.com/user-attachments/assets/64dc3eff-415c-4ac1-9ca0-169d476bc925">


2. What is the maximum 'Speed' value? What is the minimum 'Speed' value? What is the difference between max and min 'Speed'?

```py
max_speed_value = pokemon_df['Speed'].max()
print(f'Max "Speed" value: {max_speed_value}')
min_speed_value = pokemon_df['Speed'].min()
print(f'Min "Speed" value: {min_speed_value}')
difference = pokemon_df['Speed'].max() - pokemon_df['Speed'].min()
print(f'Difference between max and min "Speed": {difference}')
```
<img width="350" alt="Screenshot 2024-08-03 at 16 13 00" src="https://github.com/user-attachments/assets/241cb90c-f064-4937-a1ca-59e1cf6de069">

3. Filter the DataFrame to include only the Pokémon with 'Speed' >= 80. How many Pokémon meet this criterion? Display this DataFrame using your preferred visualization method.

```py
speed_greater_than_80 = pokemon_df[pokemon_df['Speed']>80]
print(f'Pokemon with Speed>= 80: {len(speed_greater_than_80)}')

n, bins, patches = plt.hist(pokemon_df['Speed'], color='darkblue', edgecolor='grey', bins = 6)
specific_speeds = sorted(set(bins).union([80]))
plt.axvline(x=80, linestyle='dashdot', color='#dc143c')
plt.xticks(specific_speeds)
plt.xlabel('Speed')
plt.ylabel('Number of pokemons (Frequency)')
```
<img width="478" alt="Screenshot 2024-08-03 at 16 12 01" src="https://github.com/user-attachments/assets/34731b3a-0ac0-46f4-a05c-7bc5b9467eb7">

4. (DIFFICULT) Find Pokémon with the longest name (excluding spaces)? What is this pokemons name?

```py
pokemon_df['Names_wihtout_spaces'] = pokemon_df['Name'].str.replace(' ', '', regex=False) 
longest_name = pokemon_df.loc[pokemon_df['Names_wihtout_spaces'].str.len().idxmax(), 'Name']
print(f'The longist Pokemon name: {longest_name}')
```
<img width="362" alt="Screenshot 2024-08-03 at 16 14 50" src="https://github.com/user-attachments/assets/afa42376-dd80-42f5-8423-125eb02caf65">





