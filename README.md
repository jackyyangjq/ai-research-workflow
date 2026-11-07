# AI research workflow

These are the habits that have saved me the most time when using Claude Code for research and for building software, with templates you can copy. The same content is on my website: [How I work with AI](https://jackyyangjq.github.io/ai-workflow/).

I am Jiaqi (Jacky) Yang, a dual PhD candidate at The Hong Kong Polytechnic University and the University of Surrey. I work on tourism and hospitality economics with causal inference and LLM text measurement. [Website](https://jackyyangjq.github.io) · [GitHub](https://github.com/jackyyangjq)

**Contents:** [Let it ask the questions first](#let-it-ask-the-questions-first) · [Four commands worth learning](#four-commands-worth-learning) · [One paper, many sessions](#one-paper-many-sessions) · [Errors that give no warning](#errors-that-give-no-warning) · [Ground rules](#ground-rules) · [Further reading](#further-reading) · [Templates](#templates)

The website version has animated demos of each habit.

## Let it ask the questions first

Most of the time I lose with an AI agent comes from letting it start too early. Before any code or text is written, have it interview you, then choose from a short list of options.

- **Ask to be interviewed.** Start with: “Don't write anything yet. First ask me the questions you need answered.” Save the answers in a spec file, then build in a new session.
- **Pick from a list.** Ask for three ways to do it and what each one costs. Choosing from a list is quicker than correcting a draft.
- **Look at the result.** After each change, run the app or open the table, because code that reads well can still give a wrong answer.

Small tools I built this way:

- [Calorie tracker](https://jackyyangjq.github.io/caltrk/): a web app that reads food photos with a vision model.
- [Call tracker](https://github.com/jackyyangjq/catfolio): scores stock calls against later prices, inside an open-source portfolio dashboard.
- [Filings Q&A agent](https://github.com/jackyyangjq/filings-qa-agent): answers questions about SEC filings and cites a source for every sentence.

## Four commands worth learning

Beyond ordinary chat, these are the commands I use most. All four work in the terminal, and /btw, /doctor and /effort also work in the desktop app.

| Command | Use it when | How | Watch out |
|---|---|---|---|
| `/btw` | You want to ask something quick while Claude is still working. | Type /btw and your question. It can see the conversation so far and answers in a small window while the main task continues. The question is not added to the conversation. It answers from what it already knows, so ask about what has already happened, for example “which file did you just change, and why?” If the answer needs a search, press f to hand it to a background agent. In the desktop app it is called side chat, and on a Mac you open it with Cmd+;. | If a permission prompt appears while the window is open, look before you press a key. Esc can reject the edit. |
| `/doctor` | Claude starts ignoring one of your rules, or you have installed many plugins and skills. | It checks your installation, unused extensions and your rules files, and reports before changing anything. Newer versions add /doctor prompt-audit, which looks for instructions that contradict each other or are out of date. The first time I ran it, it found 17 problems, several of them pairs of rules that contradicted each other. Read the report, decide which of the conflicting rules to keep, and only then let it make the changes. | Its first suggestion may be to fix everything at once. Review the items one at a time. |
| `/effort` | The work moves from planning to checking. | It sets how much work the model does before it answers, including how much it reads and checks. My rule is low effort while deciding what to do, and high effort or above when the result has to be right, such as tracing why two runs of a model disagree or reviewing code that handles passwords and keys. If the plan is wrong, more effort will not correct it, so return to the questions. | Max lasts only for the current session, and the app warns that it can overthink. Keep it for the hardest tasks. |
| `/rewind` | Claude has taken the wrong direction and you want to return to an earlier point. | With the prompt box empty, press Esc twice, or type /rewind, and choose an earlier message. You can restore the code, the conversation, or both. Returning to an earlier point is often better than correcting, because the failed attempt is removed from the conversation. Rewinding does not undo changes to files that only shell commands touched, so keep using Git for anything that matters. | Most edits made by subagents are not restored either, so commit before you split work across agents. |

## One paper, many sessions

A paper takes months, which is too long for one chat. I organise it the way a small team would: one session plans, other sessions do the work, and a fresh one checks it. Progress is kept in files, so nothing is lost when a session ends.

| Step | Who | What happens |
|---|---|---|
| Plan | Planning session | The planning session splits the work into cards. Each card states the goal and how we will know it is done. |
| Do | Worker sessions | Each card runs in its own session: the strongest model for judgement calls, a cheaper one for routine work. |
| Check | Fresh session | A new session checks each result against its card. The session that did the work should not be the only one to check it. |
| Record | Task board | One file lists every card and its status. Each new session reads it before starting. |

Do not start too many sessions at once. When parallel work exhausted my usage quota, I asked the planning session for the prompts and the order to run them, ran them myself, and had it check the results at the end.

## Errors that give no warning

The worst mistakes I have made with AI produced no error message, only a number or a file that looked fine. Here is what each one looked like and how to catch it.

| Error | What happened | What to do |
|---|---|---|
| A log that said it worked | A script that turned my manuscript into a Word file skipped the formatting rules it could not match and still reported success. The headings appeared in the wrong font. | Open the output and look at it, whatever the log says. |
| A sign stored the other way round | Capital spending was stored as negative numbers, as is usual in cash-flow statements. Used without correcting the sign, it reversed one of my conclusions. | Compare units and signs with the data documentation. |
| Groups merged without warning | An ID built from two other columns was not unique, so groups that should have stayed separate were combined. Nothing failed, but the results changed. | Count unique IDs before and after every merge. |
| A helper that kept running | A file search started by an AI helper continued to run after its task had ended. It used the processor for hours and made the cloud-sync service download every file it touched. | Give agents narrow folder paths, and look for leftover processes after long jobs. |

## Ground rules

These rules apply however fast AI makes the drafting.

In research:

- The research question, the design and every claim in print are my responsibility.
- Check every reference against its DOI before citing it. Models produce convincing references that do not exist.
- Declare AI use as each journal requires.

In code:

- Public code runs on simulated or public data. Confidential data stays out of public repositories.
- Keep API keys out of Git, and read every repository before making it public.
- When a language model labels text for measurement, have a second model check the labels.

## Further reading

- Anthropic, [Session management and 1M context](https://claude.com/blog/using-claude-code-session-management-and-1m-context): when to rewind, compact, start afresh or use a subagent, with a clear diagram.
- Anthropic, [Spending your effort](https://claude.dev/blog/spending-your-effort/): the loop of being interviewed first, implementing at low effort and verifying at high effort.
- Anthropic, [Model and effort level](https://claude.com/blog/claude-model-and-effort-level-in-claude-code): how to decide between a stronger model and more effort.
- Anthropic, [Explore the context window](https://code.claude.com/docs/en/context-window): an interactive simulation of what fills the context during a session.
- Chris Blattman, [AI for professionals who don't code](https://github.com/chrisblattman/claudeblattman): a University of Chicago economist's guides, written partly for academics, with skills and diagrams you can reuse.
- Benjamin Lira, [Claude Code for researchers](https://github.com/lirabenjamin/claude-code-for-researchers): slides and skills from a Wharton demo, with a good picture of how memory files fit together.
- Alexander Quispe, [Claude Code research course](https://github.com/alexanderquispe/claude-code-research): course materials with figures of the plan workflow and the memory stack.
- YK Sugi, [Claude Code tips](https://github.com/ykdojo/claude-code-tips): a long list of practical tips, including sketches of working with Git worktrees.

Claude Code is a product of Anthropic. Anthropic has not reviewed or endorsed this page.

## Templates

Copy them into your own project and delete what you do not need.

| File | Use it for |
|---|---|
| [templates/project-instructions.md](templates/project-instructions.md) | The rules file an agent reads at the start of every session (`CLAUDE.md` for Claude Code, `AGENTS.md` for Codex) |
| [templates/task-card.md](templates/task-card.md) | One unit of work, handed to its own AI session |
| [templates/task-board.md](templates/task-board.md) | The single record of progress across sessions |
| [checklists/before-you-trust-a-number.md](checklists/before-you-trust-a-number.md) | Checks for errors that produce no error message |

## Licence

MIT. See [LICENSE](LICENSE).
