# Repository Instructions

- After changing marketplace or plugin files, run `claude plugin validate .`.
- After changing `plugins/immersion-day-topic-selection-plugin`, also run `claude plugin validate ./plugins/immersion-day-topic-selection-plugin`.
- Keep `SKILL.md` focused on the core workflow. Put detailed scoring rules, source rules, output formats, and templates in `references/`, `data/`, or `assets/`.
- Use AWS Knowledge MCP (`aws-knowledge`) first for AWS official evidence when available.
- If AWS Knowledge MCP is unavailable, use AWS official web sources as fallback and state `AWS official web fallback` in outputs.
- Do not treat last-year or older FitCloud Immersion Day topics as automatic exclusions unless the user explicitly asks to exclude them.
