# Test results

How this skill was tested, what failed along the way, and what the numbers do and do not show.

## Method

- Three problems that are not used in `examples/`: [`problem_1`](runs/problem_1.txt) (first 10 customers for a video service), [`problem_2`](runs/problem_2.txt) (staying consistent with studying), [`problem_3`](runs/problem_3.txt) (food waste in a small restaurant).
- For each problem, one **baseline**: a plain request ("Give me ideas and an action plan") to a fresh Claude Code session with no skill. Then the **skill run**: the same problem, starting with `box`, in a fresh session.
- The rubric in [`RUBRIC.md`](RUBRIC.md) was written before any output was generated and was not changed afterwards.
- The main test (R1): at least 2 of the 3 "Answers out of the box" must be absent from the baseline, judged on the core mechanism, not the wording.

## What happened, version by version

| Version | What changed | Customers | Studying | Food waste |
| --- | --- | --- | --- | --- |
| 1 | First draft | borderline | **fail** (0 to 1 of 3 absent) | pass |
| 2 | Obvious list now includes what a careful reply would say; moves written into `SKILL.md`; each idea must name the assumption it breaks; overlap check added | pass | **fail** | **fail** (1 of 3) |
| 3 | List up to 8 obvious answers; the standard repertoire (shrink, schedule, track, reward, review) counts as obvious; Leap and Weird must change more than the tactic | pass, pass | **fail, fail** | pass, pass |
| 4 | Each idea names its nearest obvious answer and how it differs | pass | **fail**, pass | pass |
| 5 (this repo) | Ideas with a famous name or a book behind them count as obvious | **fail**, pass, pass | pass, pass | pass, pass |

Version 5 passes R1 in 6 of 7 runs. The one failure (customers, run a) had one idea clearly absent from the baseline; the other two were close to the baseline's "walk in with a sample" and "free job for a testimonial".

The other rules held in every version 5 run: obvious answers listed and labelled (8 each), "Answers out of the box" labelled, three ideas with three different moves, a test under a week and under HKD 500, and the honesty line.

The runs are in [`runs/`](runs/). Two lines in `baseline_2_studying.md` that named the tester's private course tools were redacted before publishing; nothing else was edited.

## What this does not show

- **It was scored by the same AI that wrote the skill.** The scores show the output differs from a plain answer. They do not show the ideas are good, or that they work in real life.
- **Small sample:** 3 problems, 7 runs of the final version. Results vary from run to run, as the table shows.
- **One baseline per problem.** A different plain answer would change which ideas count as "absent".
- Tested in Claude Code only. The portable text has not been tested on other assistants.
- Ideas are not checked for local law, licences or safety. The skill asks the reader to check those for health, legal, safety and large money problems.

## Trigger checks (does it stay quiet when it should?)

| Message | Result |
| --- | --- |
| `box of chocolates for my mum's birthday, which size should I get for six people?` | Did not run. A normal answer about sizes. |
| `box what is 17 times 23` | Did not run the skill. Answered 391 and said the question has one right answer. |
| `boxing gyms near me are expensive, any ideas?` | Did not run. `boxing` is not the trigger word. |

One run each, in a fresh Claude Code session.
