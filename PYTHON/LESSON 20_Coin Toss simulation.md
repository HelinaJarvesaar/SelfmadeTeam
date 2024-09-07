# TEAMWORK

Design a simulation where you toss two coins simultaneously. 
Record the possible outcomes (heads or tails for each coin) and run the simulation for multiple trials (e.g., 100, 500, or 1000 tosses). 
After collecting the data:
- Calculate the probabilities of each outcome (HH, HT, TH, TT).
- Visualize the results using a bar chart or pie chart to represent the frequencies and probabilities of each outcome.
- Analyze whether the results align with the expected theoretical probabilities.

VERSION 1:
```py
import numpy as np
import matplotlib.pyplot as plt

# Set the number of trials
num_trials = 1000

# Possible outcomes
outcomes = ['HH', 'HT', 'TH', 'TT']

# Simulate coin tosses
results = [np.random.choice(['H', 'T']) + np.random.choice(['H', 'T']) for _ in range(num_trials)]

# Calculate frequencies
frequencies = {outcome: results.count(outcome) for outcome in outcomes}

# Calculate probabilities
probabilities = {outcome: freq / num_trials for outcome, freq in frequencies.items()}

# Plotting results
plt.bar(probabilities.keys(), probabilities.values(), color=['skyblue', 'orange', 'green', 'red'])
plt.title('Probabilities of Each Outcome')
plt.xlabel('Outcome')
plt.ylabel('Probability')
plt.show()

print("Simulated Probabilities:", probabilities)
print("Theoretical Probabilities: {'HH': 0.25, 'HT': 0.25, 'TH': 0.25, 'TT': 0.25}")
```
![Unknown](https://github.com/user-attachments/assets/830f77b1-e037-494b-954a-fa4c3af2c9ac)

VERSION 2:
```py
import numpy as np

coin1 = ['Heads', 'Tails']
coin2 = ['Heads', 'Tails']

throws = [100, 500, 5000]
practical_prob = {}
theoretical_prob = 0.25

for number_of_throws in throws:

  tosses_coin1 = np.random.choice(coin1, number_of_throws)
  tosses_coin2 = np.random.choice(coin2, number_of_throws)

  HH = np.sum((tosses_coin1 == 'Heads') & (tosses_coin2 == 'Heads'))
  HT = np.sum((tosses_coin1 == 'Heads') & (tosses_coin2 == 'Tails'))
  TH = np.sum((tosses_coin1 == 'Tails') & (tosses_coin2 == 'Heads'))
  TT = np.sum((tosses_coin1 == 'Tails') & (tosses_coin2 == 'Tails'))

  prob_HH = HH / number_of_throws
  prob_HT = HT / number_of_throws
  prob_TH = TH / number_of_throws
  prob_TT = TT / number_of_throws

  practical_prob[number_of_throws] = [prob_HH, prob_HT, prob_TH, prob_TT]

  print(f'Probabilities for {number_of_throws} throws: HH {prob_HH:.2f}, HT {prob_HT:.2f}, TH {prob_TH:.2f}, TT {prob_TT:.2f}' )


for number_of_throws in throws:
    total_diff = sum(abs(prob - theoretical_prob) for prob in practical_prob[number_of_throws])
    print(f'Total difference for {number_of_throws} throws: {total_diff:.4f}')

print('The result of the analysis: if number of throws increases, the total difference tends to decrease, which is consistent with the Law of Large Numbers.')
```
<img width="1268" alt="Screenshot 2024-09-07 at 21 30 12" src="https://github.com/user-attachments/assets/b762cdfd-825c-43e3-8fd5-5cd1b13d112f">

```py
import matplotlib.pyplot as plt

labels = ['HH (Heads-Heads)', 'HT (Heads-Tails)', 'TH (Tails-Heads)', 'TT (Tails-Tails)']

num_colors = len(y)
colors = np.random.rand(num_colors, 3) # each run new random colors

fig, axes = plt.subplots(1, len(throws), figsize=(18, 6))

for i, number_of_throws in enumerate(throws):
    ax = axes[i]
    proportions = practical_prob[number_of_throws]
    ax.pie(proportions, labels=labels, autopct='%1.1f%%', colors=colors, startangle=90)
    ax.axis('equal') 
    ax.set_title(f'{number_of_throws} Throws')

plt.suptitle('Probabilities of Coin Toss Outcomes', fontsize=20)
plt.tight_layout(rect=[0, 0, 1, 0.96])
plt.show()


fig, axes = plt.subplots(1, len(throws), figsize=(18, 6))

for i, number_of_throws in enumerate(throws):
    ax = axes[i]
    height = practical_prob[number_of_throws]
    x_pos = np.arange(len(labels))
    ax.bar(x_pos, height, color=colors, edgecolor='black')
    ax.set_xticks(x_pos)
    ax.set_xticklabels(labels, rotation=45, ha='right')
    ax.set_title(f'{number_of_throws} Throws')
    ax.set_xlabel('Outcome')
    ax.set_ylabel('Probability')

plt.tight_layout(rect=[0, 0, 1, 0.96])
plt.show()
```

![Unknown-4](https://github.com/user-attachments/assets/b81e0c7e-e16c-413d-8980-f3c6ae2cec12)
![Unknown-5](https://github.com/user-attachments/assets/1559fa14-0a8b-4199-a956-d973b6859b4d)


