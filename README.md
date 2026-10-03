# Bristol Career Coach

`career_coach`, an add-on agent for [Bristol Tickets](https://github.com/JackHatchett/bristol-tickets):
a job search in any field and at any seniority. It triages job descriptions
against your history, tailors a resume to one posting, drafts cover letters in
a voice distilled from writing you have already done, builds interview-prep
material, and tracks applications in Bristol's local database. An optional
harvest turns job-alert email into a feed of postings.

## Adding it to Bristol

1. Download `career_coach.agent.json` from this repository.
2. In Bristol Tickets, open Agents, press Import Agent and choose the file.
3. Read the agent's mandate and guardrails in the window that opens, then press
   Accept.
4. Fill in the values the import lists as yours to supply: the absolute paths
   in `env`, which point into your own `data/<instance>/` folder.

The same from a terminal, in your Bristol folder:

```
python3 src/tools/agent_tools/import_agent.py career_coach.agent.json
python3 src/tools/agent_tools/import_agent.py career_coach.agent.json --accept
```

The first run fetches each skill from this repository and scans it, and writes
no agent. The second adopts it.

## What is here

| Path | What it is |
| --- | --- |
| `career_coach.md` | The charter: what the agent is for, and the guardrails that halt it |
| `career_coach.agent.json` | The charter, its config entry with every local value taken out, and the address of each skill |
| `skills/` | One folder per skill, each importable on its own |
| `requirements.txt` | The packages the job-alert harvest needs |

Two of the skills the agent file names, `briefing-the-board` and
`working-a-contact`, ship with Bristol and are not in this repository.

## One skill at a time

Any folder under `skills/` can be imported alone: in Bristol's Skills tab press
New Skill, choose Import From GitHub, and paste the address of the folder as
GitHub shows it, for example
`https://github.com/JackHatchett/bristol-career-coach/tree/main/skills/jd-evaluation`.

## Needs

- A `data/<instance>/career/` folder holding your resume, employment history,
  voice samples and context files. The agent builds it up with you over the
  first few sessions.
- For the job-alert harvest only: `pip install -r requirements.txt`,
  `playwright install chromium`, and a Gmail API credential in the keychain, as
  `skills/harvesting-job-alerts/SKILL.md` describes.

## Licence

MIT, as `LICENSE` states.
