# ruff-lsp-bug-repro

The ruff-lsp server provides code actions for some linting issues, but not others. At a
minimum, I think it would be cool if they all provided a code action to disable the ruff rule for the
current line. This repro is referenced in a [github issue
comment](https://github.com/astral-sh/ruff-lsp/issues/94#issuecomment-1568646285).

## How to use this

Git clone the repo and fire up neovim with a minimal init file:

    cd /tmp && rm -rf assorted-repro-scenarios && git clone https://github.com/burnettk/assorted-repro-scenarios.git && cd assorted-repro-scenarios/ruff-lsp-bug-repro
    nvim -u minimal_init.lua hey.py

Neovim lsp (via the ruff lsp server) will show two issues with the file:

    │ File: hey.py
    ────┼─────────────────────────────────────────────────────────────────────────────────────────────────
    1   │ def sureEnough():        <--- Function name `sureEnough` should be lowercase
    2   │     a = 1                <--- Local variable `a` is assigned to but never used
    3   │     print("I'm sure")
    4   │
    5   │ sureEnough()

If you move the cursor to line 2 and invoke the "code action" shortcut with
`<space>ca`, it will give you code action options including "Ruff: Disable F841
for this line" BUT if you move to the cursor to line 1, where the other issue
is, and do the same `<space>ca`, it will say "No code actions available" (there
were four code action options for line 2). There
is a case where I'd love to add a line-specific Ruff-ignore comment with a code
action because we are overriding functions in the logging.Formatter class like
`usesTime` and `formatMessage`, so yeah, they are named wrong (should be
snake_case), but they are in
stdlib, and so there isn't much that can be done about it in my codebase other
than ignoring the lines.
