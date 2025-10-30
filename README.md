# dot.config

This repository tracks the handful of configuration directories that are
safe to share across hosts. Everything else under `~/.config` stays out
of Git by default.

## Tracked items

- `rio/config.toml` and the `rio/themes` symlink pointing to the local
  `tinted-terminal` theme library.
- `tinted-theming/tinty/config.toml`, which keeps the Tinty hook pointed
  at the Rio template.

If you add more directories, remember to whitelist both the directory
and anything the application loads indirectly (for example, symlinks to
dotfile checkouts).

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

## Optional: custom Tinty schemes

Tinty will pick up custom Base16/Base24 schemes placed under
`~/.config/tinted-theming/schemes/` after running `tinty sync`. With the
Rio hook already wired, applying your scheme via `tinty apply <name>`
updates `rio/config.toml` and keeps `rio/themes` in sync.
