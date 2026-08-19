# claude-code-ste

A Claude Code skill that applies Simplified Technical English (a working
distillation of ASD-STE100) to English technical prose: code comments,
docblocks, commit messages, pull and merge request descriptions, `README`
and `CLAUDE.md` prose, architecture and decision notes, runbooks, and error
text an engineer reads. It does not apply to product UI copy, marketing
copy, or any non-English text.

## Install

A personal skill applies across every project. Clone the repository and
symlink the skill directory into `~/.claude/skills/`:

```bash
git clone https://github.com/moghaddas/claude-code-ste.git
mkdir -p ~/.claude/skills
ln -s "$(pwd)/claude-code-ste/ste" ~/.claude/skills/ste
```

A project skill applies only to one repository. Symlink it into that
repository's `.claude/skills/` directory instead:

```bash
mkdir -p /path/to/your/project/.claude/skills
ln -s "$(pwd)/claude-code-ste/ste" /path/to/your/project/.claude/skills/ste
```

Claude Code follows the symlink and reads `ste/SKILL.md` from this checkout,
so a `git pull` here updates the skill everywhere it is linked.

## Use

Claude loads the skill automatically when a task matches its description —
writing or reviewing a comment, a commit message, an MR description, or
similar English technical prose. Invoke it directly with `/ste` when you
want it to run on demand.

## What it covers

`ste/SKILL.md` holds the rules that bite in practice: one instruction per
sentence, active voice and present tense, one word per meaning, no noun
cluster over three words, the condition before the instruction, and no
`-ing` form where a finite verb works. `ste/reference.md` holds the
term-list template, three worked before/after rewrites, and the two cases
where a rule is meant to yield: a term of art, and a sentence with real
ambiguity.

## License

MIT. See `LICENSE`.
