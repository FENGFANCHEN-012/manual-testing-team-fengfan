# Reflection — Member A

1. **What makes a test positive or negative?**
   It depends on the input, not the outcome. A positive test uses valid input (e.g. age 30, `standard_user` / `secret_sauce`) and expects acceptance; a negative test uses invalid input (e.g. age 10, a wrong password) and expects rejection.

2. **Why can a negative test pass?**
   A negative test passes when the system rejects the invalid input as expected. In LOGIN-N01 the "Username and password do not match" error was the correct behaviour, so the test passed even though an error appeared.

3. **How did equivalence partitioning help you select data?**
   It split age into three groups (below 18, 18–80, above 80), so one value from each group (10, 30, 90) covered all three behaviours. Three values from inside 18–80 would only have tested one group.

4. **What did boundary testing help you investigate?**
   It focused on the edges, where off-by-one mistakes happen (17/18 and 80/81, then 16/19/79/82). All age boundaries behaved correctly. It also showed that the browser's HTML5 `min`/`max` blocks these values, while the page's JavaScript uses a wider 16–100 range.

5. **What did you choose to test during the open-ended activity, and why?**
   First name and surname length limits. The brief's baseline name `Alex` was rejected by the server, even though the rule only says the first name must be filled, so I wanted to find the real limits.

6. **Did your observations lead to follow-up tests?**
   Yes. The baseline failure led to testing first names of 2–5, 89 and 90 characters. Those showed that the JavaScript requires at least 3 characters and the server at least 5. That raised further questions about the server's upper limit and how spaces and accented letters are counted.

7. **How does your Git history show your contribution?**
   Each checkpoint is a separate commit on `testing/member-a`: preparation, then login, equivalence, 2-point, 3-point, the planned self-designed cases, their results, and this reflection. The pull request then merges them into `main`. Because this is a solo submission, every commit is mine.
