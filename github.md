# GitHub

Applies when filing, refining, labelling, or closing an issue, grooming a backlog, or scoping a milestone.

## Where work is tracked

- **Work is tracked in issues.** An issue holds its own state: open or closed, its milestone, its relations.
- **A trivial fix is made, not filed.** Small nits are collected in one sweep issue.
- **An issue holds work someone can start now.** Something that waits on an event is written where it will be read when the event happens, or is dropped.
- **What the scope document lists as a non-goal is not filed.**

## What an issue says

- **The title names the thing and the gap,** specific enough to triage from the list alone.
- **The body lets someone start cold.** A bug gives the steps, what was expected, and what happened. Anything else gives the goal, the current state with paths, the scope, and when it is done.
- **A decision nobody has made is listed under "Open questions",** each with a recommended answer, never buried in prose.
- **The body reads as currently true.** A fact that drifted is corrected in place, with no comment and no dated note: the edit history keeps the old text. A judgement or a question is a comment.

## Labels

- **Every issue carries exactly one type label:** `bug` for observed wrong behaviour, `enhancement` for a new capability, `foundation` for enabler work — developer experience, code quality, de-risking other work — and `question` for a decision to make or something to work out, with nothing to implement yet.

## Relations

- **A dependency is recorded as a blocked-by relation, never as prose.** It is a dependency only where it can be said which issue cannot start until the other is done. Anything weaker is a "Related" line in the body.
- **A duplicate is closed as a duplicate of the survivor,** and the scope only it had moves into the survivor's body.

## Milestones

- **A milestone is release scope and nothing else:** one per numbered version, holding the issues that release is blocked on.
- **Its description states what the version promises.** An issue belongs in it only if the release would break that promise without it.

## Closing

- **Age alone never closes an issue.**
- **An issue that someone other than the maintainer opened or commented on is never closed or edited without the maintainer's word.**

## Not settled — raise the trade-off, leave the call to the maintainer

- **Projects.** Left out for now: a status field there would be a second home for what the issue already holds. A board to open without starting a session, or other people working in the repositories, would be reasons to bring them in.
- **Ranking.** No label or field marks priority. Whether one should is open.
