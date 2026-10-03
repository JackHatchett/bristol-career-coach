---
name: voice-lint
description: Checks a draft written in the user's own voice against his banned-phrase list, the dash constraint and period emphasis, and says whether it may be delivered. Use before anything in his voice leaves the session — a cover letter, a resume, a profile section, a post.
license: MIT
compatibility: Runs inside a Bristol installation; needs python3. Reads the blacklist from career_coach's data root.
metadata:
  bristol.kind: tool
  bristol.maintainer: career_coach
  bristol.scripts: scripts/voice_lint.py
  bristol.subtitle: Check a draft in the user's voice
---
# voice-lint

Input: a draft, as `.txt` or `.docx`. Operation: `scripts/voice_lint.py`, in
this skill's own folder. Output: every banned phrase, dash construct and
period-emphasis run in the draft, and an exit code saying whether it may go out.

```
python3 <this skill's folder>/scripts/voice_lint.py <draft.txt | draft.docx> [--fiction] [--blacklist PATH]
```

`python3 src/tools/skill_tools/skills.py list --json` gives the folder as the
skill's `path`.

- **The gate covers everything written in the user's own voice**, not a cover
  letter alone: a resume, a profile section, a post. A skill that produces such
  a draft runs this.
- **Run it on the draft text before packing, and again on the packed file.**
  Fix every HARD, DASH and PERIOD_EMPHASIS hit; review every FLAG hit.
- **Exit 0 is clean, 1 is a violation and the draft is not delivered, 2 is a
  usage or file error.**
- **The phrase lists bind every form; the two coded patterns do not.**
  `--fiction` drops the dash constraint and period emphasis, which the voice
  profile scopes to business writing and to non-fiction, and checks the phrase
  lists alone.
- **A bullet marker at the head of a line is markup, not a dash construct.** A
  resume writes its bullets `-- like this`, and a dash later in the same line is
  still reported.
- **The blacklist is the user's own content.** It resolves from
  `agents.career_coach.key_data_paths` plus `foundation/*_Voice_Blacklist.txt`;
  `--blacklist` overrides that. More than one match under that glob is an error
  naming the flag.
