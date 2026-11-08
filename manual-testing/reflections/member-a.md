# Reflection — Member A

1. **What makes a test positive or negative?**
   It depends on the input. If I give valid input, like age 30 or the right password, it is a positive test and I expect it to be accepted. If I give invalid input, like age 10 or a wrong password, it is a negative test and I expect it to be rejected.

2. **Why can a negative test pass?**
   Because the goal of a negative test is to see the system reject bad input. In LOGIN-N01 the error message was exactly what should happen, so the test passed even though I got an error.

3. **How did equivalence partitioning help you select data?**
   It split age into three groups: below 18, 18 to 80, and above 80. I only needed one value from each group (10, 30, 90) instead of trying lots of random numbers from the same group.

4. **What did boundary testing help you investigate?**
   It made me test the edges (17/18 and 80/81, then 16/19/79/82), which is where off-by-one bugs usually are. The age edges all worked. I also noticed the browser blocks them with the HTML min and max, while the page's JavaScript uses a wider range of 16 to 100.

5. **What did you choose to test during the open-ended activity, and why?**
   I tested how long the first name and surname can be. The baseline name `Alex` got rejected even though the rules only say the first name must be filled, so I wanted to know the real limit.

6. **Did your observations lead to follow-up tests?**
   Yes. Because `Alex` failed, I tried names of 2, 3, 4, 5, 89 and 90 letters. I found the JavaScript needs at least 3 letters and the server needs at least 5. Now I want to know what the server does with very long names and how it counts spaces and accents.

7. **How does your Git history show your contribution?**
   I made a commit at each checkpoint on `testing/member-a`: getting ready, login, equivalence partitioning, 2-point, 3-point, my own test plan, my own test results and this reflection. Then I merged it all into `main` with a pull request. Since I did this alone, all the commits are mine.
