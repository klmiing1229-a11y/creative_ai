# Portable `think_out_of_the_box`

For an AI that cannot load skill files (ChatGPT, or any assistant with custom or project instructions).
Copy the text below into your custom or project instructions, then start a message with `box`.

```text
When a message starts with the word "box" (any casing; not "boxing" or "boxes"), I want you to think out of
the box about the problem I give you. If I write "box" alone, use my previous message. Ask at most ONE
question, only if the problem is too vague, and give a default. Reply in the language I used.
If the problem has one right answer (a lookup, maths), say so and just answer it.

1. Obvious answers. Imagine a thorough AI reply with ten ideas. List the 5 to 8 that matter most, one line
   each, with a short clause for when it is still the right call. KEEP them, labelled as obvious. The standard
   repertoire (measure, shrink, schedule, track, reward, review, simplify, discount, partner, refer, plan for
   the lapse) and anything with a famous name or a book behind it (Pomodoro, Feynman technique...) counts as obvious.
2. Hidden assumptions. List 3 to 5 assumptions inside how I stated the problem.
3. Break them. Make 8 to 10 candidates using at least five different moves: invert it; remove the biggest
   constraint; add an absurd constraint; borrow an exact mechanism from a distant field; solve a different
   problem; make the problem disappear; give it to the opposite person; subtract.
4. Filter. If a candidate has the same core mechanism as an obvious answer (a smaller, stricter, timed,
   scheduled, tracked or rewarded version counts as the same), move it to the obvious list. Drop what cannot
   be tested in under a week, needs more money, time or skill than I said, or fits any problem unchanged
   ("build a community", "gamify it"). For health, legal, safety or big money problems, keep tests small and
   tell me to ask a professional.
5. Reply in this shape and stop:
   Problem (one line) / Limits I used /
   "Obvious answers" (numbered, each with when it is still right) /
   "Hidden assumptions" (bullets) /
   "Answers out of the box": at most three, labelled Stretch, Leap, Weird but testable. Each has: Idea,
   Move used, Assumption broken, Nearest obvious answer (#n) and how this differs, Cheapest test (under one
   week, with a rough cost), Biggest risk. Three different moves, three different assumptions. Leap must
   change the goal, the buyer or the resource, not only the tactic. If you cannot state a different
   mechanism from the nearest obvious answer, replace the idea. /
   Filtered (how many dropped, how many moved to the obvious list) /
   Honesty: "these are not among the obvious answers above. That does not mean nobody has tried them." /
   "Next? (go deeper on 1 / 2 / 3, make a week plan from one, pair one with an obvious answer, new problem, done)"

Rules: never call an idea new, original or unheard of. Say what you do not know about my situation in the
risk line. Do not invent facts or studies. Plain words, short sentences, no lecture on creativity.
```
