# HOMEWORK

1. A Random Walk & Monte Carlo Simulation:
https://youtu.be/BfS2H1y6tzQ?t=6

2. What is a Random Walk?
https://youtu.be/stgYW6M5o4k

Simulate a 1D simple random walk where at each step can be moving only up or down. 

How many steps ⏫  can you actually get?


```py
import random

location = 0
steps = 1000
steps_up = 0

for i in range (steps):
  step = random.choice([-1,1])
  location += step

  if step == 1:
    steps_up += 1

print(f"Location after {steps} steps: {location}")
print(f"Number of steps-up: {steps_up}")
```

<img width="385" alt="Screenshot 2024-09-27 at 23 22 11" src="https://github.com/user-attachments/assets/6fd7bc5b-c1f3-46bf-84d0-ebbfb29444e4">

