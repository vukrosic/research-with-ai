# Research with AI

Copy-paste prompts that take an AI agent from an empty folder to a full ICML paper: literature review, ideas, baselines, experiments and the finished paper in the official ICML LaTeX format.

You do not need to know what to do next. Copy each prompt into your agent (Claude Code, Codex or any coding agent), replace only the lines in `< >`, and make the decisions in the "Your turn" sections.

- Video walkthrough: https://youtu.be/yX1puxdtYoo
- Each prompt as a plain text file: [prompts/](prompts/)
- AI Research School (ready papers, set-up research environments, help with your own paper): https://www.skool.com/become-ai-researcher-2669

## Contents

- [Part 1: What makes a good ICML paper](#part-1-what-makes-a-good-icml-paper)
- [Part 2: The pipeline](#part-2-the-pipeline)
- [Step 1 prompt: literature research and ideas](#step-1-prompt-literature-research-and-ideas)
- [Step 2 prompt: baselines and benchmarks](#step-2-prompt-baselines-and-benchmarks)
- [Step 3 prompt: search for a finding](#step-3-prompt-search-for-a-finding)
- [Step 3b prompt: scale check on a bigger computer (optional)](#step-3b-prompt-scale-check-on-a-bigger-computer-optional)
- [Step 4 prompt: write the paper](#step-4-prompt-write-the-paper)

## Part 1: What makes a good ICML paper

A good ICML paper teaches the field something true that it did not know, and shows it convincingly enough that other researchers change what they do or believe.

Reviewers judge four things. A paper does not need to be the best at all four, but it must not fail any of them.

### 1. Novelty: is there new knowledge?

Novelty means the reader learns something they could not have learned from earlier work. It is not the same as "nobody has written this exact sentence before".

Kinds of novelty that count:
- A new method that does something better, cheaper or more simply than the current best methods.
- A new finding: a measured effect, rule or failure that people did not know about, even if it uses only known methods.
- A new explanation: why something that people already use works or fails, shown by experiments that rule out the other explanations.
- A new problem, benchmark or way to measure something, when it exposes what current methods cannot do.
- New theory that predicts something checkable, or that explains results people already see.
- A surprising negative result: a popular belief or method that does not hold up when tested carefully.
- Known pieces combined in a way that gives a result neither piece gives alone.

What does not count:
- Applying a known trick to a new setting when the outcome is what everyone would predict.
- Renaming or repackaging an existing method.
- A small gain from tuning, with no insight into why.

Test: write the one sentence the reader should remember. If a strong researcher in the area would already have guessed it, the novelty is weak.

### 2. Significance: does it matter?

The result should matter beyond this one paper. Ask: who would use it, and what would they do differently?

Signs of significance:
- It touches something many people work on (pretraining, post-training, optimizers, world models, robot learning, and so on).
- The effect is large, or small but on something that is used everywhere.
- It points to a general rule, not just one setting.
- It opens new questions that others can follow up.

A paper at small scale can be significant if the question is general and the paper argues clearly why the rule should carry over to larger settings, or honestly states where it might not.

### 3. Soundness: is the evidence strong enough for the claims?

Every claim must be backed by evidence, and the paper must not claim more than the evidence shows.

What sound evidence looks like:
- It is compared against the current best methods, run fairly with the same budget and tuning effort, not only against weak or old baselines.
- Controls rule out the obvious other explanations.
- Ablations show which part of the method or setup causes the effect.
- It is tested on more than one setting (tasks, model sizes, data sizes), so the rule is not a coincidence of one setup.
- Uncertainty is reported where it matters, and differences that are smaller than the noise are not claimed as wins.
- Negative and mixed results are reported honestly, not hidden.
- The predictions and the win rule are written down before the results come in.

### 4. Clarity: can a reader understand it and repeat it?

- The main finding is in the title, the abstract and the first page.
- Terms are defined before they are used, and the paper skips no steps.
- Figures show the main result at a glance.
- The setup is described well enough that someone else could repeat it, and the code is shared.
- The paper says plainly what is not known and where the result might not hold.

### Short version

A good ICML paper has:
- one clear finding that a strong researcher would not have guessed;
- a reason why it matters to many people;
- evidence against the current best methods that rules out the other explanations;
- writing clear enough that a reader can repeat the work.

## Part 2: The pipeline

The agent does the work and you make the decisions. There are four prompts, plus an optional scale check. After each one comes your turn: you ask the agent to explain what it did in simple sentences until you understand it, and then you decide what happens next.

- Step 1: Literature research and ideas (agent, a few hours)
  - Then you: understand the ideas and pick one
- Step 2: Baselines and benchmarks in code (agent, a few hours to a day)
  - Then you: check the baselines and choose the compute
- Step 3: Search for a finding (agent, can take several days)
  - Then you: look in when you want and give advice
- Step 3b: Scale check on a bigger computer (agent, optional, a few hours to a day)
  - Then you: decide how much GPU time to spend
- Step 4: Write the paper (agent, a few hours)
  - Then you: read the paper and decide if it is ready

Search small, scale later. Do steps 2 and 3 on a laptop or one small GPU, where one run takes minutes and you can run hundreds of them. Rent a bigger GPU only in step 3b, to check that a result that already works on small models still holds on bigger ones. That way you pay only for results that already work.

Rule for beginners: decide, don't ask. Beginners ask many questions and make few decisions, and that is what stops most first projects. When you don't know which option to pick, pick one at random and keep going. A wrong choice teaches you more than waiting, and you can change it later.

Copy each prompt into your agent. Replace only the lines in < > at the top.

Use one agent chat for the whole project, so it remembers what it did and why. If the chat gets too long or breaks, start a new one: every prompt first reads the files in the project folder, so nothing is lost.

### Step 1 prompt: literature research and ideas

```text
What I want to work on: <write your topic, research area, paper links, PDF paths, repo links or a short explanation. If you don't know what you want to work on, write: "I don't know what I want to work on, discover something for me.">
Topics to avoid: <optional: topics that are already taken, for example by other projects or people you work with, or "none">

You are starting an ICML research project. This first step is literature research and idea generation. Do not run experiments yet. Work through these steps in order and fix problems yourself. Only ask me if you are truly blocked.

If I did not give a topic, pick one yourself: choose an active area of machine learning (for example LLM pretraining, post-training, optimizers, world models or robot learning) where small experiments on my computer can show something new (for example, a model of 1-10M parameters trained on a few million tokens), and explain why you picked it. If I gave an area but not a topic, pick a sub-topic inside it with the same rules. Either way, first do 3-5 quick searches to choose the sub-topic, write it and the reason in LOG.md, and only then map the field inside it.

Create a new folder for this project with a short name that says what it is about, and keep everything you make inside it: notes, code and results. If I gave you my own notes or earlier projects, read them so the topic is new to me. Keep a short LOG.md in it, starting today as Day 1: add a line or two with the date only when you make a decision or find something important.

A good ICML paper teaches the field something true it did not know: a new method, a new finding, a new explanation of why something works or fails, a new benchmark that exposes a weakness, or a surprising negative result. It must matter to many researchers and be provable with experiments that compare against the current best methods.

1. Understand the topic.
   Explain in plain words what problem it is about, how progress is measured, and give one concrete example.

2. Map the field.
   Search arXiv, OpenReview, Semantic Scholar, GitHub and the web, with whatever search tools you have, with a focus on the last 2 years. Find the 15-30 most relevant papers for the main map; papers you find later, during the novelty check, go in a separate "also checked" list. For each: link, year, one sentence on what it does, its main result, and whether code exists (a project page or "code released" on the paper is enough; mark links you did not open). Group them by approach. Name the 3-5 current best methods with code and the benchmarks they report on. If the topic is a finding or an explanation rather than a new method (for example a scaling or data question), name instead the 3-5 papers whose results the finding must explain or overturn. For each famous result, check whether a newer paper beat it or overturned it; the most cited paper is often not the current best.

3. Find the gaps.
   List what is not done or not understood. Look for:
   - tricks everyone uses that nobody explains;
   - known failures of the best methods that nobody fixed;
   - results that disagree between papers;
   - claims tested only in one setting, size or task;
   - two lines of work that never met;
   - assumptions everyone makes that nobody tested.
   For each gap, cite the papers that show it is a gap.

4. Generate ideas.
   Write 10-20 candidate ideas that fill those gaps. For each, write:
   - the idea in one sentence;
   - what type of contribution it is (method, finding, explanation, benchmark, negative result);
   - the result we expect, and the experiment that would kill it;
   - if it fails, whether the negative result is still worth reporting (yes or no, and why);
   - which current best method it must beat or explain.

5. Check novelty.
   For every idea, do a quick search for papers that already did it. For the 5 most promising, search deeply and name the 3 closest papers and say exactly what differs. Drop any idea where a paper already does the same thing, and any idea that overlaps a topic to avoid. Write "the closest work I found is X", never "nobody has done this".

6. Rank the survivors.
   Score each surviving idea from 1 to 5 on:
   - novelty: would a strong researcher in this area be surprised?
   - significance: who would change what they do if it works?
   - testability: can a small-scale experiment on my computer show it in minutes per run, with memory under about 2 GB?
   - simplicity: can the finding be said in one sentence?
   Use these anchors: 5 = excellent (for novelty: a strong researcher would bet on the opposite result), 3 = fair (half-expected), 1 = poor (already known). Add up the scores, keep the top 3-5 and explain the ranking. Then describe in 3-5 lines the small-scale testbed the top ideas would share: what data or simulator, the model sizes, and the time and memory of one run.

7. Write two files.
   - LITERATURE.md: the paper map, the current best methods and benchmarks, and a table of what is done and what is not.
   - IDEAS.md: the ranked ideas, each with its closest papers, its expected result and its kill experiment, plus the dropped ideas with the paper that killed each one.

Never invent a paper, a citation or a number. Link every paper you mention. If you are not sure a paper exists, say so. Label every number by where it came from: (paper) if you read it in the paper, (abstract), (search summary), or (training data, not re-checked). Ideas are guesses until experiments test them, so keep several, not one.
```

### Your turn 1: understand the ideas and pick one

Ask the agent until you can explain the project in simple sentences. For example:
- Explain the topic in one simple sentence, with one example.
- Explain each of the top ideas in one simple sentence.
- If this idea works, what would the result look like? And if it fails?
- What exactly is different from the closest paper?

Then pick one idea. If two look equally good, pick either one.

Also decide your compute for the search: a laptop (small models, runs of a few minutes) or a GPU (bigger models). Either way, fast experiments are better, because you will run many of them. A bigger GPU for the scale check can be decided later, in step 3b.

### Step 2 prompt: baselines and benchmarks

```text
Project folder: <path to the folder from step 1>
Chosen idea: <the idea you picked from IDEAS.md, in your own words>
Compute: <for example "MacBook, runs of a few minutes, under 2 GB of memory" or "one GPU with 24 GB">

You are continuing an ICML research project. First read LOG.md, LITERATURE.md and IDEAS.md in the project folder. This step sets up the baselines and benchmarks that the chosen idea will be compared against. Do not try the idea yet. Fix problems yourself and only ask me if you are truly blocked.

1. Pick the baselines.
   Choose 3-5 current best methods for this problem. Start from LITERATURE.md and search again for anything newer. For each, write the paper and its year, what it does in one sentence, and why it is a strong, fair competitor. Simple older methods can be added as extra rows, but they do not count as the 3-5. If the idea is a finding or an explanation rather than a new method, the baselines are the recipes, models and measurement methods of the 3-5 papers whose results the finding must explain or overturn, run in your setting.

2. Pick the benchmarks.
   Use the tasks, datasets and metrics that the baseline papers use. If you replace one with a smaller dataset to fit the compute, write which paper's benchmark it stands in for. Make them diverse: at least 2-3 different kinds of data or task (for example prose and code, not three sets of the same kind of text), and at least 2 model sizes, so that a win cannot come from one lucky setup. Skip benchmarks where every method at your scale scores near chance, because they cannot tell methods apart, and write why you skipped them. Keep a test set that is never used for tuning.

3. Fit the scale to the compute.
   Choose model size, data size and training length so one run fits the compute I gave. Keep a modern architecture and keep the conditions that matter at large scale. Write down what you scaled down and why the result should still carry over to larger models.
   Before running anything at full size, do one test run and measure its peak memory and wall time. If it goes over the memory limit or takes much longer than the run time I gave, make it smaller and measure again. Only then launch the rest, and never run more at once than the memory allows.

4. Get the code.
   Search for the official code of every baseline. If it exists and fits the compute, use it. If the full repo is too big for the compute, copy the method's core (loss, schedule, settings) from the official code, not from the paper text, and check yours against it line by line. Write the repo link, commit and file for each. If no official code exists, implement the method from the paper, following its equations and settings, and write down every detail you had to guess. Put all methods behind one shared training and evaluation script, so they all get the same data, the same budget and the same tuning effort. Make the script run unchanged on a GPU as well (one device setting), so a scale check later needs no rewrite.

5. Check the setup before trusting any number.
   - Each baseline shows the behavior its paper reports, at least in direction (for example, it beats the simple baseline). If not, find out why.
   - A broken run (shuffled labels, random weights or no training) scores badly, so the benchmark can tell good from bad.
   - The test data never appears in training, and tuning uses only the validation data.
   - Every method got the same budget and the same tuning effort.
   If a check fails, fix it before moving on and write what was wrong.

6. Run every baseline on every benchmark and write BASELINES.md.
   It holds the results table, what each check showed, which code is official and which is our own implementation, the guesses we made, a table of each paper's setup (model size, data, training length) next to ours, and the measured time and peak memory of one run.

Add a short entry to LOG.md. Never report a number you did not measure.
```

### Your turn 2: check the baselines and the compute

Ask the agent:
- Explain each baseline in one simple sentence.
- Why these baselines and not others? Is any newer method missing?
- Does the order of the baselines in our table match what their papers report? If not, why?
- How are the benchmarks different from each other? Could a method win on all of them by one trick?
- Was the test data ever used to choose settings?
- How far is our setup from the papers' setups (model size, data, training length)?
- Which baselines use official code, and which did the agent write itself?

Then decide: keep this scale, make it smaller so runs are faster, or make it bigger if the baselines do not behave like in their papers.

### Step 3 prompt: search for a finding

```text
Project folder: <path to the project folder>
How long to search: <for example "until a result survives every check, or 3 days">
Advice: <optional: anything you want the agent to try or avoid>

You are continuing an ICML research project. First read LOG.md, IDEAS.md and BASELINES.md in the project folder. Now search for a result worth an ICML paper: a new method that beats the baselines, or a new finding or explanation that the field does not know. The chosen idea is the starting point, not a limit. If you see something surprising, follow it. Work on your own and do not stop to ask me.

Before the first round, measure the noise: rerun one baseline setting a few times, and use the spread as the tie line. A gap smaller than that is a tie, or at most weak evidence. Run every grid through one resumable job runner (a job file in, one result row per run out, finished jobs skipped on a rerun).

Work in rounds. In each round:
1. Before running, write down what you will try, what you predict, and the rule that counts as a win (for example: beats the best baseline on most benchmarks, by more than the noise).
2. Run many small, fast experiments with the shared script and the same budget as the baselines.
3. Add a short takeaway to RESULTS.md: what happened, what it means, and what you will try next.
4. Drop an idea once it fails on 2 benchmarks, and try new ones. Keep failed ideas in RESULTS.md with their numbers. When something works, try hard to break it: use controls and ablations that rule out the other explanations.

When a result looks real:
- check that it holds at several sizes (bigger model, more data, longer training, within the compute) and on every benchmark, and write where it fails;
- compare it against every baseline with the same tuning effort, and give the strongest baseline every extra the method gets (warm start, more steps, a schedule) in a matched run before saying "beats";
- if a formula explains the result, test it on runs it was not fitted to and report how many runs it fits out of all of them;
- search again for papers that already found it;
- write the one sentence a reader should remember.

Stop when a result survives all of this, or when the time is up. Then write FINDING.md: the claim, the main results table, the controls, the ideas that failed, where it fails and the closest work. If nothing survived, write what we learned instead; a carefully tested negative result can also be a paper.

Then write SCALE-PLAN.md: the exact runs for a scale check on bigger models (the main comparison and the most important control, at 2-3 sizes bigger than you could run here), with the commands and the expected run time and memory of each, measured from a short local run. Also write, before anything runs, which outcomes would confirm the finding and which would break it. The plan must run on a GPU without changes; at least check that it runs on this machine with the same device flag. If no GPU is available, stop after this file; the paper will say small scale only.

Keep LOG.md short: a line or two when you make a big decision or find something.
```

### Your turn 3 (optional): look in during the search

You don't have to do anything during the search. When you want, read the latest takeaways in RESULTS.md and ask:
- Explain the last round in one simple sentence.
- What is the best result so far, and how sure are you of it?
- What are you trying next, and why?

If you have advice, give it. If not, let it run.

### Step 3b prompt: scale check on a bigger computer (optional)

Use this when the search ran on small models and you can get a bigger GPU. Decide the GPU time first, for example "one rented GPU with 24 GB, at most 10 hours". Skip this step if you have no bigger computer; the paper will then say plainly that everything was tested at small scale.

```text
Project folder: <path to the project folder>
Compute: <for example "one rented GPU with 24 GB, at most 10 hours in total">

You are continuing an ICML research project on a bigger computer. First read LOG.md, FINDING.md, BASELINES.md and SCALE-PLAN.md in the project folder. The finding was found on small models. Now check whether it still holds on bigger ones. Work on your own and do not stop to ask me.

1. Check the setup. Make sure the shared script runs here, then rerun one small run from RESULTS.md and confirm you get the same number. If not, find out why before anything else.
2. Fit the plan to the compute. Time one short run of each size in SCALE-PLAN.md, estimate the total, and cut the plan to fit the compute I gave. Keep the main comparison (the finding against the best baseline) at the biggest size first; drop extras before you drop sizes.
3. Run the plan, most important runs first. Save every result as soon as it finishes, so a stopped machine loses nothing.
4. Add a scale section to FINDING.md: does the effect grow, stay or shrink as the model gets bigger? Show a table or plot by size and write where it fails. Do not change the claim to fit the new numbers; if it does not hold at scale, say so.

Add a short entry to LOG.md. When everything is saved, tell me, so I can stop the rented machine (it costs money while idle). Never report a number you did not measure.
```

### Step 4 prompt: write the paper

```text
Project folder: <path to the project folder>

You are finishing an ICML research project. Read every file in the project folder, especially FINDING.md, RESULTS.md and BASELINES.md. Write the paper in the official ICML format, as a LaTeX paper and its PDF, not as a web page. Download the official ICML style files (the author kit linked from the ICML author instructions page, for example icml2026.sty). Write paper-conf/main-icml.tex with \usepackage[preprint]{icml2026}, save every figure as a PDF in paper-conf/figures/, and build paper-conf/main-icml.pdf with pdflatex (run it twice).

Structure: title, abstract (150-200 words, saying the work is small scale), introduction (the problem, the finding, the contributions), related work, setup, results (main table and figures against the baselines), analysis (ablations, controls, sizes), limitations, conclusion, references, and an appendix with the settings and how to rerun the experiments (one example command, the list of flags, and the run file behind each table and figure). Main text 3,000-4,500 words and within the ICML limit of 8 pages, at most 6 figures; references and appendix come after.

Rules:
- Put the main finding in the title, the abstract and the first page.
- Back every claim with a table or figure made from results in this folder. Do not claim more than the evidence shows.
- Make every figure, table and number in the text with a script in the folder that reads the run files. Before the review, rerun those scripts and fix any number that does not match.
- Define every term before using it and skip no steps, so a reader new to the area can follow. Check each key word for a second meaning in ML (for example "hidden" also means hidden layers) and pick another word if it has one.
- Say plainly what was done at small scale and where the result might not hold.
- Every reference must be real and linked. Never invent a paper or a number. If a close paper cannot be opened, list it as unread, never describe it from its title, and tell me to open it.
- Look at every page of main-icml.pdf: every figure and table must be readable, with no overlapping labels, broken numbers or text running into the margin, and the LaTeX log must show no errors.

Then read the paper as a strict ICML reviewer. Write REVIEW.md with the 5 biggest weaknesses. Fix wording and scope now. If a comparison is unfair, run the matched baseline and change the claim to what the new runs show. List what needs more compute in the limitations. Last, re-read the title, abstract and contributions and check each claim against the final tables.
```

### Your turn 4: read the paper and decide

Ask the agent:
- Explain the paper in one simple sentence.
- What is the weakest claim, and what evidence supports it?
- What would a reviewer attack first?
- Does the finding hold on the biggest models we ran, or only on small ones?

Then decide: the paper is ready, or the agent goes back to step 3 to fix the weakest part.

## Updates

The prompts improve after every project: each run writes what went wrong, and the fix goes into the prompts. Watch or star this repo to get the newest version.

## License

MIT. Use the prompts for anything.
