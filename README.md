# cmdfinder_catalog

Remote command catalog for [cmdfinder](https://github.com/JonaVicesar/cmdfinder). When you run `cf add` in the terminal, cmdfinder fetches programs from this repository so you can install them locally.

## Structure

```
.
├── index.json              # program name → description (used by the TUI browser)
└── catalog/
    ├── git.json            # actions, aliases, and commands for git
    ├── docker.json         # actions, aliases, and commands for docker
    ├── curl.json           # ...
    └── ...
```

Each catalog file is a self-contained JSON with the program's actions, natural-language aliases, and ready-to-copy commands.

## How it works

1. `cf add` opens a TUI that shows local programs + programs available in this catalog
2. Selecting a catalog program downloads its JSON into your local `~/.local/share/cmdfinder/commands.json`
3. After that, `cf <program> <action>` searches using fuzzy matching across the action names and aliases

## Available programs

33 programs in the catalog: adb, apt, bun, curl, docker, ffmpeg, flatpak, gcc, general, git, go, gradle, grep, java, journalctl, kubernetes, linux, mysql, nano, nginx, nmap, node, npm, pnpm, postgresql, python, redis, ssh, sudo, supabase, systemctl, tar, vim.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for the JSON format, naming rules, and how to add new programs or actions.

## License

[MIT](LICENSE)
