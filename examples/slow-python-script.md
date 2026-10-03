# Example: a technical problem

**User:** box My Python script that processes about 10,000 CSV files takes four hours to run overnight and sometimes crashes halfway through. I can't buy more hardware and I'm not an expert programmer.

**think_out_of_the_box:**

**Problem:** A script that processes about 10,000 CSV files takes 4 hours overnight and sometimes crashes partway through.
**Limits I used:** no new hardware, and you're not an expert programmer.

## Obvious answers
What most AI replies would say. They're listed on purpose, and some may be exactly right.
1. **Use all your CPU cores** (`multiprocessing` or `concurrent.futures`). Still the right call when each file is independent, which is likely here and is usually the biggest speed-up.
2. **Profile first** by timing each step. Still the right call when you don't know what's slow.
3. **Read the files faster** by loading only the columns you need, setting column types, or switching from pandas to polars or pyarrow. Still the right call when most of the time goes on reading.
4. **Wrap each file in try/except**, log the bad ones and keep going. Still the right call when a few malformed files cause the crashes.
5. **Checkpoint and resume**: save results per file and skip finished files on restart. Still the right call when a crash costs you the whole night.
6. **Log the filename and time for every file**, so you know where it died. Still the right call, because you can't fix a crash you can't locate.
7. **Convert the CSVs to Parquet once.** Still the right call when the same files are read again and again.

...and more of the same kind.

## Hidden assumptions
- All 10,000 files must be processed from scratch every run.
- Every output is needed, and all of it by morning.
- The crash is a random script bug you have to guess at.
- The slow job is the problem, rather than how the output is used.

## Answers out of the box
### 1. Stretch: Only process what changed
**Idea:** Keep a small record (a text file) of each input file's last-modified time. Next run, skip any file that hasn't changed since the last successful run. If only 5% of files change nightly, a 4-hour job becomes about 12 minutes.
**Move used:** Subtract. It removes work instead of speeding it up.
**Assumption broken:** All 10,000 files must be processed from scratch every run.
**Nearest obvious answer:** #5, and **how this differs:** a checkpoint only resumes after a crash within one run, while this shrinks every night's work list permanently.
**Cheapest test (under one week):** Count how many files changed in the last day, with `find . -name "*.csv" -mtime -1 | wc -l` on Mac or Linux. It takes one minute and costs nothing.
**Biggest risk:** If your processing depends on other files or settings that change, skipping unchanged inputs gives stale results.

### 2. Leap: Find out who reads the output, and make only that
**Idea:** Ask whoever uses the results (a person, a report, another script) which outputs they open, and how fresh they need to be. Then process only those files, or process the rest on request.
**Move used:** Solve a different problem. The goal becomes "the results someone uses are ready", not "everything runs fast".
**Assumption broken:** Every output is needed, and all of it by morning.
**Nearest obvious answer:** #1, and **how this differs:** parallelism does the same total work faster, while this does less total work because most of it may never be read.
**Cheapest test (under one week):** Ask the consumer one question today. Or check the "last opened" dates on last week's output files. It costs nothing.
**Biggest risk:** If the outputs feed a total or report that needs every file, this does nothing for you.

### 3. Weird but testable: Run the file list backwards tonight
**Idea:** Change `for f in files:` to `for f in reversed(files):`, and print each filename as it starts. If it crashes on the same file as before, that file is bad. If it crashes after the same amount of time, the cause is memory or the computer sleeping. Each result points to a different fix.
**Move used:** Invert. Flipping the order turns a random crash into an experiment.
**Assumption broken:** The crash is a random script bug you have to guess at.
**Nearest obvious answer:** #6, and **how this differs:** logging tells you where one crash happened, while reversing tells you whether the crash belongs to a file or to the clock.
**Cheapest test (under one week):** Make the one-line change and run it overnight. If you're on a laptop, also keep it awake, for example with `caffeinate -i python yourscript.py` on a Mac.
**Biggest risk:** The crash is only "sometimes", so one night may not crash at all and tell you nothing. Repeat it if so.

**Filtered:** 3 candidates dropped (they needed facts about your files I don't have, or another machine), 3 moved to the obvious list (auto-restart loop, one output file per input, restarting every N files).
**Honesty:** these are not among the obvious answers above. That does not mean nobody has tried them.

Next? (go deeper on 1 / 2 / 3, make a week plan from one, pair one with an obvious answer, new problem, done)

*(Real output from a fresh Claude Code session with the skill installed. Obvious answers: multiprocessing, profiling, checkpoints. Out of the box: skip files that did not change, find who reads the output, and run the list backwards to learn why it crashes.)*
