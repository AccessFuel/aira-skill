# AIRA skill

Use [AccessFuel](https://www.accessfuel.com) from an agent's visible built-in
browser. The skill can answer KPI questions, create audiences and personas,
and prepare unscheduled campaign drafts. It uses verified page tools when they
are available. Until AccessFuel page tools ship, it opens a prefilled AIRA chat
for you to review and send.

```text
/aira find customers who spent over $500 but haven't bought in 90 days, build a persona, draft a win-back email campaign
```

The skill never enters credentials, automates console writes, sends or
publishes content, schedules campaigns, or deletes data.

## Requirements

- An AccessFuel account and access to a workspace.
- An agent host with a visible built-in browser and page-reading support.
- Git, for the install commands below.

Browser support varies by host and version. The skill stops safely when the
required browser capability is unavailable.

## Install in Claude Code

### Plugin marketplace

Run these commands inside Claude Code:

```text
/plugin marketplace add AccessFuel/aira-skill
/plugin install accessfuel@accessfuel-skills
```

Then invoke the namespaced skill:

```text
/accessfuel:aira show my top 10 products by revenue last month
```

Run `/reload-plugins` if Claude Code asks you to reload after installation.

### Standalone project install

From the root of your project:

```sh
mkdir -p .claude/skills
git clone https://github.com/AccessFuel/aira-skill.git .claude/skills/aira
```

Invoke it as `/aira`. The clone remains independently updateable. Teams that
want to pin it in their repository can add the public repository as a Git
submodule at the same path.

### Standalone personal install

```sh
mkdir -p ~/.claude/skills
git clone https://github.com/AccessFuel/aira-skill.git ~/.claude/skills/aira
```

Personal Claude Code skills apply to local projects but do not install into a
Claude Cowork or cloud account.

## Install in Claude Cowork

1. Open **Customize → Plugins → Add marketplace**.
2. Enter `AccessFuel/aira-skill` or the full repository URL.
3. Install **AccessFuel**.

Invoke the plugin skill as `/accessfuel:aira`.

## Install in Codex

### Project install

From the repository root where you launch Codex:

```sh
mkdir -p .agents/skills
git clone https://github.com/AccessFuel/aira-skill.git .agents/skills/aira
```

### Personal install

```sh
mkdir -p ~/.agents/skills
git clone https://github.com/AccessFuel/aira-skill.git ~/.agents/skills/aira
```

Codex detects installed skills automatically. If it does not appear, restart
Codex. Type `$aira` in a prompt to select it explicitly, or let Codex invoke it
when a request clearly names AccessFuel or AIRA.

## Update

Run `git pull --ff-only` inside the installed `aira` directory. For example:

```sh
git -C ~/.agents/skills/aira pull --ff-only
```

Claude marketplace installs can be updated from Claude Code with:

```text
/plugin marketplace update accessfuel-skills
```

## Repository contents

- `SKILL.md` — procedure and safety boundaries.
- `references/console-map.md` — customer-facing objects and console paths.
- `references/page-tools.md` — discovery guidance for planned page tools.
- `references/prompts.md` — scoped AIRA hand-off templates.
- The public repository also includes Claude plugin metadata and the license.

The installable skill is `SKILL.md` plus `references/`. Internal reviews,
implementation proposals, credentials, and unrelated repository metadata are
excluded.

## License

MIT.
