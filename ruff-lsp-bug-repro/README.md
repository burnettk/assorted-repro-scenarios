# ruff-lsp-bug-repro

## How to use this

Git clone the repo and fire up neovim with a minimal init file:

    cd /tmp && rm -rf assorted-repro-scenarios && git clone https://github.com/burnettk/assorted-repro-scenarios.git && cd assorted-repro-scenarios/ruff-lsp-bug-repro
    nvim -u minimal_init.lua hey.py

Neovim lsp via the ruff lsp server will show two issues with the file:

    │ File: hey.py
    ────┼─────────────────────────────────────────────────────────────────────────────────────────────────
    1   │ def sureEnough():        <--- Function name `sureEnough` should be lowercase
    2   │     a = 1                <--- Local variable `a` is assigned to but never used
    3   │     print("I'm sure")
    4   │
    5   │ sureEnough()
