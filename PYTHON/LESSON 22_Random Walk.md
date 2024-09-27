# HOMEWORK

1. A Random Walk & Monte Carlo Simulation:
https://youtu.be/BfS2H1y6tzQ?t=6

2. What is a Random Walk?
https://youtu.be/stgYW6M5o4k

Simulate a 1D simple random walk where at each step can be moving only up or down. 

How many steps ⏫  can you actually get?


```py
import random

steps = 1000
steps_up = 0
location = 0
locations = [location]

for i in range (steps):
  step = random.choice([-1,1])
  location += step
  locations.append(location)

  if step == 1:
    steps_up += 1

print(f"Location after {steps} steps: {location}")
print(f"Number of steps-up: {steps_up}")
```
<img width="355" alt="Screenshot 2024-09-27 at 23 32 30" src="https://github.com/user-attachments/assets/71ae7faa-bed6-43ed-81e5-2938fb4e3781">

```py
pylab.figure(figsize=(10, 6))
pylab.plot(locations, label="1D Random Walk", color='navy')
pylab.title(f"1D Random Walk - {steps} Steps")
pylab.xlabel("Steps")
pylab.ylabel("Location")
pylab.grid(True)
pylab.legend()

pylab.show()
```

<img width="847" alt="Screenshot 2024-09-27 at 23 33 30" src="https://github.com/user-attachments/assets/27c9e9a1-d750-4703-8538-d86d82961e94">



