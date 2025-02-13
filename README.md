# CodeChalllenge


Problem 1: Loop method (sum_to_n_a)

- Imagine you’re counting money, adding one bill at a time until you reach the total. That’s what this loop does—starts at 1 and keeps adding until it hits n.
- It’s simple and gets the job done, but if n is really big, it takes longer.

Problem 2: Formula method (sum_to_n_b)

- This is like a life hack. Instead of counting one by one, you just use a trick: n * (n + 1) / 2.
-Imagine you have a bunch of stacked boxes, and instead of lifting each one, you just use a shortcut to get the total weight. Boom! Instant answer.

Problem 3: Recursive method (sum_to_n_c)

- This one is kinda like a domino effect. The function keeps calling itself, breaking the problem down into smaller and smaller pieces until it reaches the last one (1), then stacks everything back up.
- It’s a cool and elegant approach, but if n is too big, it could cause a mess (stack overflow).