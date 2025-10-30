# dot.config

This repository tracks the handful of configuration directories that are
safe to share across hosts. Everything else under `~/.config` stays out
of Git by default.

## Workflow

1. Add a new directory or file to the whitelist in `.gitignore`:

   ```gitignore
   !/atuin/
   !/atuin/**
   ```

   The first rule unignores the directory itself, the second brings its
   contents back in scope. Repeat this pattern for each directory you
   want to version. Use `!/filename` for standalone files.

2. Stage the whitelist updates and the actual files you care about:

   ```sh
   git add .gitignore atuin/
   ```

3. Commit and push as usual.

Keep nested Git repositories (e.g. `fish/.git`) ignored unless you plan
to convert them into submodules.
