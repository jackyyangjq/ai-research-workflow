# AI research workflow

How I use Claude Code for empirical research and for building software, in outline, with templates you can copy. The same content is on my website: [How I work with AI](https://jackyyangjq.github.io/ai-workflow/).

I am Jiaqi (Jacky) Yang, a dual PhD candidate at The Hong Kong Polytechnic University and the University of Surrey. I work on tourism and hospitality economics with causal inference and LLM text measurement. [Website](https://jackyyangjq.github.io) · [GitHub](https://github.com/jackyyangjq)

**Contents:** [Vibe coding](#vibe-coding) · [A paper from question to submission](#a-paper-from-question-to-submission) · [Matching effort to the task](#matching-effort-to-the-task) · [Running a project with AI sessions](#running-a-project-with-a-team-of-ai-sessions) · [Quiet errors](#errors-that-dont-announce-themselves) · [Tools and limits](#tools-and-limits) · [Templates](#templates)

## Vibe coding

Vibe coding means describing software in plain language and letting an AI coding agent write the code. I decide what gets built and how to check it.

- Spec first: the agent interviews me before any code, and my answers become the spec.
- Check every step: after each change I run the app or the numbers, rather than trusting code that reads well.
- Known answers: methods are tested on simulated data with a known effect, and LLM labels against a second model.
- Secrets stay local: API keys stay out of git, and I read every public repository before it goes out.

Built this way:

- [Calorie tracker](https://jackyyangjq.github.io/caltrk/): single-file web app that reads food photos with a vision model. 20 versions in seven weeks.
- [Finfluencer digest](https://github.com/jackyyangjq/finfluencer-digest): runs every morning on GitHub Actions and sums up the stock calls made on finance channels.
- [Filings Q&A agent](https://github.com/jackyyangjq/filings-qa-agent): answers questions about SEC filings with a checkable source for every sentence, tested on 50 questions.
- Open-source fixes: a merged [pull request to ClaudeCodeUsage](https://github.com/ClaudeCodeUsage/ClaudeCodeUsage/pull/115), a VS Code extension that tracks Claude Code and Codex usage, and [four pull requests](https://github.com/irrwood/catfolio/pulls?q=author%3Ajackyyangjq) to an open-source portfolio dashboard.

## A paper from question to submission

A working paper on generative AI and tourism jobs. Claude Code worked on every stage and I kept the decisions. Results and data details stay out of this repository until the paper is published.

| Stage | What the AI does | What I decide |
|---|---|---|
| Question and literature | Searches the literature, summarises papers and checks whether a term I plan to use already means something else in the field | The question and what the paper adds |
| Design | Drafts alternative designs and lists the threats to each | The identification strategy |
| Data and code | Writes the scripts and re-estimates the main results a second, independent way | Definitions, the sample, and what a result must survive before I trust it |
| Writing | Drafts sections from my outline, following a style guide and a fixed glossary | The argument and every claim |
| Revision | Turns supervisor comments into task cards; a fresh session audits each change | Which comments to act on, and how |
| Submission | Builds the journal's Word files and traces every number back to a script | The final read and the AI-use statement |

The AI shock arrived while in-person services were still recovering from the pandemic. Comparing tourism with other service industries keeps the two apart.

## Matching effort to the task

With Claude Opus 5.5, Claude Code lets me set how hard the model thinks and checks before it answers. I switch it several times on one task: low while we work out what to do, high when the result needs checking. More effort catches edge cases; it does not fix a wrong approach.

Interview (low effort) → Build (low or medium) → Review (by me) → Verify (high effort)

| Effort | In research | In web coding |
|---|---|---|
| Low | Brainstorming questions; reformatting tables and references | Copy and style changes, small fixes |
| Medium | Drafting a section from my outline; a cleaning script or figure built to a clear spec | A feature built to a clear spec |
| High | Debugging an estimate that looks wrong; the pre-submission audit that traces every number to code | Debugging and code review; anything that touches keys or user data |
| Max | Long unattended jobs with a clear finish line, such as replicating a full analysis with checks | Building and testing an app end to end; a security review |

Adapted for research and web work from Thariq Shihipar, ["Using Claude Code: Spending your effort"](https://claude.dev/blog/spending-your-effort/) (September 2026).

## Running a project with a team of AI sessions

A paper outgrows a single chat, so I run it like a small team.

| Step | Who | What happens |
|---|---|---|
| Plan | Coordinator | Splits the work into task cards and sends me short briefings. It never does the tasks itself. |
| Do | Worker sessions | Each card runs in its own session: the strongest model for judgement, a faster one for mechanical work. |
| Check | Fresh reviewer | A new session checks the result against the card's acceptance criteria. |
| Record | Task board | One file holds every card's status, so progress survives across sessions and devices. |

Some decisions never leave me: the research design, how the main results are defined, the hypotheses and the structure of the paper.

## Errors that don't announce themselves

The costliest mistakes in my AI-assisted work showed no error message. Most produced a plausible number that was wrong. The usual fix: the session that wrote something is never the only one that checks it.

| Error | What happened | What I do now |
|---|---|---|
| An ID that overflowed | Two small-integer columns were multiplied to build a group ID. The product overflowed and quietly merged thousands of groups, which moved the main estimate by about a fifth. A separate verification session caught it. | Cast types before building keys, and have a separate session re-check the main results. |
| A weight left out | One step of a weighted fixed-effects model ran without the weights. The estimate matched neither valid version of the model, yet it reached early figures before a re-estimate with explicit dummy variables exposed it. | Headline estimates must agree with a second, independent implementation. |
| A gap in the wrong place | Salary data were almost empty for the five quarters covering the AI shock and the year after it, so a before-and-after comparison was really comparing two years far apart. | Plot each variable's coverage over time before using it. |
| A sign that flipped a finding | Capital spending was stored as negative numbers, following cash-flow convention. Used as it was, it reversed a conclusion. | Check units and signs against the data documentation for every variable. |
| A build that said it worked | The script that turns a manuscript into a Word file skipped formatting rules that did not match and still reported success. The headings came out in the wrong font. | Open the output file and check it, whatever the log says. |
| An agent that kept running | A file search started by an AI helper kept going after its task had ended. For almost three hours it ran at high CPU and swamped the cloud-sync service, which tried to download every file the search touched. | Give agents narrow folder paths, and check for leftover processes after long jobs. |

## Tools and limits

Tools:

- Claude Code is my main tool. Each project has a rules file and a memory that syncs across my devices; a few custom skills handle recurring research tasks, and connected tools search the literature and check citations.
- I have tried OpenAI's Codex on side tasks, for comparison.
- In measurement work, one model labels the text and a second model checks the labels.

Where I draw the line:

- The research question and the design are mine, and so is every claim in print.
- I check every reference against its DOI before it goes into a paper.
- Public code runs on simulated or public data. Confidential research data stays out of public repositories.
- I declare AI use as each journal requires.

## Templates

Starting points, not rules. Copy them into your own project and cut what you do not need.

| File | Use it for |
|---|---|
| [templates/project-instructions.md](templates/project-instructions.md) | The rules file an agent reads at the start of every session (`CLAUDE.md` for Claude Code, `AGENTS.md` for Codex) |
| [templates/task-card.md](templates/task-card.md) | One unit of work, handed to its own AI session |
| [templates/task-board.md](templates/task-board.md) | The single record of progress across sessions |
| [checklists/before-you-trust-a-number.md](checklists/before-you-trust-a-number.md) | Checks for errors that produce no error message |

## Licence

MIT. See [LICENSE](LICENSE).
