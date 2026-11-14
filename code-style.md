# Code style

Applies when writing or reviewing code — in any language.

## Rules

- **Reuse before writing, in this order:** an existing helper or pattern in the codebase, the standard library, a native platform feature, a dependency already installed. Only then write it, and keep it minimal.
- **A bug fix targets the root cause, not the reported symptom.** Check the other callers of the function being touched: one fix in the shared function beats a guard per caller.
- **An expected failure is never clamped, defaulted, or silently ignored.** It reaches the caller as an explicit error: the error value [`architecture.md`](architecture.md) asks for in code, an explicit error in an API.
- **A user-input error may stay untyped,** a message with a bad-request status. The client either prevents the request or handles the rejection in a way the user can act on.
- **Functions are small, composable, and single-purpose.** A comment that announces what the next block does is the trigger to extract that block as a named function. Skip the extraction only where it would reduce clarity: a helper that needs many parameters threaded through, or a one-shot block that adds pure indirection.
- **A file reads top-down: every definition references only what is defined above it.** Circular dependencies are the only exception.
- **A comment explains why, never what.** What a reader could infer from types and names is cut. Prose is warranted in three places: doc comments on public APIs, seams where the signature cannot express the contract, and short orientation labels in a long function.
