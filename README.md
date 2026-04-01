# Assignment 1 — Simulated Annealing: Exam Timetable Scheduling
## Observation Report

**Student Name  :** K. Sheshi Kumar  
**Student ID    :** 2310040075  
**Date Submitted:** 01-04-2026

---

## How to Submit

1. Run each experiment following the instructions below
2. Fill in every answer box — do not leave placeholders
3. Make sure the `plots/` folder contains all required images
4. Commit this README and the `plots/` folder to your GitHub repo

---

## Before You Begin — Read the Code

Open `sa_timetable.py` and read through it. Then answer these questions.

**Q1. What does `count_clashes()` measure? What value means a perfect timetable?**

```
count_clashes() measures the number of conflicts in the timetable, such as overlapping exams for the same student or resource conflicts. It evaluates how good or bad the current timetable is. A value of 0 clashes means a perfect timetable with no conflicts.
```

**Q2. What does `generate_neighbor()` do? How is the new timetable different from the current one?**

```
creates a slightly modified version of the current timetable by randomly changing one or more exam time slots. This helps explore nearby solutions in the search space. The new timetable differs only slightly from the current one to allow gradual improvement.
```

**Q3. In `run_sa()`, there is this line:**
```python
if delta < 0 or random.random() < math.exp(-delta / T):
```
**What does this line decide? Why does SA sometimes accept a worse solution?**

```
This condition decides whether to accept the new timetable. If the new solution is better (delta < 0), it is always accepted. If it is worse, it may still be accepted with a probability based on temperature T, allowing SA to escape local minima and explore better global solutions.
```

---

## Experiment 1 — Baseline Run

**Instructions:** Run the program without changing anything.
```bash
python sa_timetable.py
```

**Fill in this table:**

| Metric | Your result |
|--------|-------------|
| Number of iterations completed | 1379|
| Clashes at iteration 1 |12 |
| Final best clashes |3 |
| Did SA reach 0 clashes? (Yes / No) |No |

**Copy the printed timetable output here:**
```
  Final Timetable
------------------------------------------
  Slot 1:  Geography
  Slot 2:  Chemistry, English
  Slot 3:  History, Computer Science, Economics
  Slot 4:  Biology, Statistics
  Slot 5:  Mathematics, Physics
------------------------------------------
  Total clashes : 3

  Iterations     : 1379
  Start clashes  : 12
  Final clashes  : 3
```

**Look at `plots/experiment_1.png` and describe what you see (2–3 sentences).**  
*Where does the biggest drop in clashes happen? Does the curve flatten out?*
```
The graph shows a rapid decrease in the number of clashes during the early iterations as the algorithm quickly improves the timetable. The biggest drop in clashes happens at the beginning when the algorithm explores many possible schedules. As the temperature decreases, the improvements slow down and the curve gradually flattens, indicating that the algorithm is converging to a stable solution.
```

---

## Experiment 2 — Effect of Cooling Rate

**Instructions:** In `sa_timetable.py`, find the `# EXPERIMENT 2` block in `__main__`.  
Copy it three times and run with `cooling_rate` = **0.80**, **0.95**, and **0.995**.  
Save plots as `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`.

**Results table:**

| cooling_rate | Final clashes | Iterations completed | Reached 0 clashes? |
|-------------|---------------|----------------------|--------------------|
| 0.80        |     8          |          low          |          No          |
| 0.95        |     3          |          medium           |          No          |
| 0.995       |     3          |          high           |          No          |

**Compare the three plots. What do you notice about how fast vs slow cooling affects the result? (3–4 sentences)**  
*Hint: Fast cooling = temperature drops quickly. Does it have time to explore well?*
```
With a fast cooling rate (0.80), the algorithm cooled too quickly and resulted in a poor solution with 8 clashes, indicating it got stuck in a local minimum. With a moderate cooling rate (0.95), the solution improved significantly to 3 clashes, showing better exploration. With slow cooling (0.995), the algorithm maintained consistent performance and also achieved 3 clashes, indicating more stable and effective optimization.
```

**Which cooling_rate gave the best result? Why do you think that is?**
```
The best cooling rate is 0.995, because it allows gradual cooling and better exploration of the solution space, leading to more stable and optimal results compared to faster cooling rates.
```

---

## Summary

**Complete this table with your best result from each experiment:**

| Experiment | Key setting | Final clashes | Main finding in one sentence |
|------------|-------------|---------------|------------------------------|
| 1 — Baseline | cooling_rate = 0.995 |3 |Slow cooling helps reduce clashes effectively but may not always reach zero |
| 2 — Cooling rate | cooling_rate = 0.995|3 |Slower cooling gives better and more stable sloutions than fast cooling |

**In your own words — what is the most important thing you learned about Simulated Annealing from these experiments? (3–5 sentences)**
```
From these experiments, I learned that the cooling rate is a critical parameter in Simulated Annealing. A fast cooling rate reduces computation time but often leads to poor solutions due to limited exploration. Slower cooling allows the algorithm to explore more possibilities and find better solutions, though it takes more time. I also observed that even with good parameters, reaching a perfect solution (0 clashes) is not guaranteed. Overall, proper balance between speed and exploration is essential for achieving good results.
```

---

## Submission Checklist

- [x] Student name and ID filled in
- [x] Q1, Q2, Q3 answered
- [x] Experiment 1: table filled, timetable pasted, plot observation written
- [x] Experiment 2: results table filled (3 rows), observation and answer written
- [x] Summary table completed and reflection written
- [x] `plots/` contains: `experiment_1.png`, `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`
