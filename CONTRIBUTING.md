# Contributing

What changing a standard takes beyond writing it. How a rule is written is in [README § Writing a standard](README.md#writing-a-standard). The reasons behind each rule are in its commit message, and in `docs/decisions/` where one earned a record.

## Checking a change

A change to a standard, to an index line naming one, or to a skill that points at one is checked by watching sessions use it. No tool can check it.

- **Run fresh headless sessions on a weaker model, each in a throwaway clone of another repository, with a task that names no standard.** Then read each transcript for what it opened. The closing comment of [#8](https://github.com/NicoVIII/standards/issues/8) has the commands. Those of [#2](https://github.com/NicoVIII/standards/issues/2), [#3](https://github.com/NicoVIII/standards/issues/3) and [#5](https://github.com/NicoVIII/standards/issues/5) have more results.
- **Run a baseline on the same task first.** One run proves little: a baseline once opened no standard at all.
- **Sessions read standards with `cat`,** often as `cd …/standards && cat a.md b.md`, so a filter for full paths misses them.
- **Headless mode denies most shell commands.** Judge what was read and drafted, not whether the task finished.
- **Deny issue writes explicitly** before a run that might file one.
- **In a repository that does not conform yet, a session follows the repository** ([#9](https://github.com/NicoVIII/standards/issues/9)). Pick the clone with that in mind.

## How a session meets a standard

- **It reads the standard its task names most narrowly, and may stop there.** The index line and the standard's opening condition decide whether it opens one at all, so a condition names every kind of work it covers: writing and changing, not only designing.
- **A skill outranks the index.** A session running a skill opens only the standards the skill names, so a new standard that overlaps a skill needs that skill edited too.
- **This `AGENTS.md` reaches a project session only through the `Read` tool.** A standard read with `cat` does not bring it along, so the read-only rule cannot be relied on to load.

## Where a rule goes

- **The schema and migration rules sit in `server-backend.md`** because only backends have had databases so far. The day a project without a backend gets a database, they become a standard of their own.
- **Rules are harvested from practice that held:** tcg-card-collector's `AGENTS.md` files, `.claude/skills/` and `docs/decisions/`, and the other repositories under [NicoVIII](https://github.com/NicoVIII?tab=repositories).
