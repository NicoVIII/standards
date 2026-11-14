---
status: accepted
date: 2026-11-14
---

# CI runs natively by default, not inside the devcontainer

## Context and Problem Statement

The devcontainer is the toolchain definition: every tool version is pinned in `devcontainer.json` and nowhere else. CI has to run the checks with those versions. It can install the tools on the runner and read the versions from that file, or it can build the devcontainer and run the checks inside it.

The standard said "natively" before either route had been measured. One repository of mine then ran all of CI inside the devcontainer, first building it on every run, later with the built image published to a registry and read back as a layer cache. A second repository ran natively throughout. Their numbers are what this decision rests on. The repositories and their suites differ, so the comparison is of overhead, not like for like.

Where does CI run by default?

## Considered Options

- Natively, with a further job that runs the checks inside the devcontainer when it changes and once a week
- Inside the devcontainer, built on every run
- Inside the devcontainer, with the built image published and used as a layer cache

## Decision Outcome

Chosen option: natively. A further job runs `just check` inside the devcontainer whenever `.devcontainer/` changes and once a week. All of CI moves into the devcontainer only where a native install would be hand-rolled.

Building the devcontainer on every run lost on time alone: the container step took 169 seconds in the repository that tried it, before any check ran.

The cached image is the option that could have won. It gives one install path, makes CI the devcontainer by construction, and needs neither the weekly job nor a step that reads versions out of `devcontainer.json`. It lost on what a run costs. With a warm cache the container step took 93 to 102 seconds, about 40 of them spent building and starting the container. A whole pull-request run in the native repository took 54 to 72 seconds, 6 of them on the toolchain. That is 30 to 90 seconds more per run, spent only to avoid the version-reading step.

The cache also does not hold on the repository's own terms. When the base image's tag moved to a new digest, every run built from nothing, 147 to 183 seconds, until a push to the default branch had published an image on the new base. Pinning the base by digest would stop that and leave the warm figure, which is still more than a whole native run.

Three things were not measured: a change to one feature alone, a private repository, where pull requests need a login to read the image, and a suite that needs a service such as a database. None of them can make the container route faster.

### Consequences

- Good, because the toolchain is ready in seconds and a run costs about a minute where it was measured.
- Good, because a repository needs no registry package and no job that holds write permission to publish one.
- Bad, because native CI needs a step that reads tool versions out of `devcontainer.json`, and nobody has built it. The native repository measured here states its versions in the workflow instead, which the standard rules out. What the step costs is unknown.
- Bad, because CI and the devcontainer are two install paths that can drift apart. The further job is what catches that, up to a week late.
- Bad, because a published image could also shorten the first start of a devcontainer on a developer's machine. With native CI nothing publishes one, so that use needs a reason of its own. It was not measured.
