# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- When i opened it, it looked like a normal number guessing game but when i started testing the game, i found few things off. 

- List at least two concrete bugs you noticed at the start  
  (for example: "the secret number kept changing" or "the hints were backwards").
- 1. The hints are reversed. It shows higher when the number is lower and lower when the number is supposed to be higher.

- 2. When we click newgame, a new secret number is generated but it wont actually start a new game because we cannot submit our guesses.
---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Copilot

- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
-  The AI suggested "when the guess is too high it says "Go HIGHER!" and when it's too low it says "Go LOWER!", which is backwards
Let's fix that in the check_guess function. The messages on the "Too High" and "Too Low" branches need to be swapped:
app.py+2-2
Now when your guess is too high, it correctly tells you to go lower, and when it's too low, it tells you to go higher."


i found the line where there were bugs and fixed it and verified by rerunning the code

- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).
- When I said the game ended one attempt too early, the AI pointed me to the wrong bug (string comparison on even attempts) and gave a long explanation. I tested the game again and the problem was still there. The real fix was changing `>=` to `>` in the attempt limit check.



---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
I ran the app again after fixing the bug to check it myself if the bug is fixed or not.

- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- I manually tested the hints by guessing a number I knew was too high and checking if it said "Go LOWER". After fixing the reversed messages in `check_guess`, the hints showed correctly, which told me the fix worked.

- Did AI help you design or understand any tests? How?
- Yes, Copilot explained what the three tests in `test_game_logic.py` were checking a correct guess, a too-high guess, and a too-low guess. It helped me understand that the tests import from `logic_utils.py`, not `app.py`, which is why they were fail.

---

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
when a neww game is started the value of secret is kept as a random.randint which assignes it a random number in the range of the level.

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
- Every time you click a button or type something in Streamlit, the whole script runs again from the top like refreshing the page. Session state is like a notebook that remembers values between those reruns, so things like your score or the secret number don't reset every time the page refreshes.

- What change did you make that finally gave the game a stable secret number?
- The secret is only generated using `if "secret" not in st.session_state`, which means it only runs when the game first starts. After that, the value stays saved in session state and doesn't change on every rerun.

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
  trying to look for errors and edge cases so i can pinpoint the bugs better and check manually myself if the AI suggestion is correct or not.


- What is one thing you would do differently next time you work with AI on a coding task?
Not trusting it completely and see if the suggestion makes sense or not and provide a better prompt.

- In one or two sentences, describe how this project changed the way you think about AI generated code.
- I used to think AI generated code was mostly correct and just needed small changes, but this project showed me it can have multiple hidden bugs that look ok and the programs also runs. Now I know I need to actually test and question the code instead of just trusting it.
