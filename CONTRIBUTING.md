# Contributing to cmdfinder_catalog

Thanks for helping build the command catalog! Every contribution makes `cf` more useful.

## What is this repo?

This is the **remote catalog** that `cmdfinder` fetches when you run `cf add`. Each JSON file in `catalog/` contains commands, aliases, and descriptions for a single program. The `index.json` file maps program names to short descriptions so the TUI can show a browseable list.

## Adding a new program

1. Create a new file in `catalog/` named after the program: `catalog/myprogram.json`
2. Add the program to `index.json`
3. Submit a pull request

### File naming

- Use **lowercase**, no spaces or special characters: `docker.json`, not `Docker.json`
- Use the common CLI name: `git.json`, not `git-version-control.json`

### JSON structure

Each file wraps everything under the program name:

```json
{
  "myprogram": {
    "program_description": "myprogram - short description of what it does",
    "actions": {
      "action-name": {
        "aliases": ["synonym 1", "synonym 2", "common phrase"],
        "description": "What this action does",
        "commands": [
          "myprogram <flag> <arg>  # inline comment explaining the flag"
        ]
      }
    }
  }
}
```

### Action naming

- Use **kebab-case**: `remove-container`, not `removeContainer` or `Remove Container`
- Name by **what it does**, not by the flag: `remove-container`, not `-rm`
- Keep it short but clear

### Aliases

Aliases are what users actually search for. Think about how someone would **describe** the action in natural language:

```json
"aliases": [
  "remove container",
  "delete container",
  "kill container",
  "stop and remove"
]
```

Rules:
- **Lowercase** always
- Include **multiple synonyms** different people think of different words
- Include **phrases**, not just single words: `"stop and remove container"` is better than just `"stop"`
- No need to repeat the action name if it's already clear
- Include the common flag as an alias if people think in flags: `"-rm"`, `"ps"`

### Commands

- One command per line
- Use `<placeholder>` for arguments: `<file>`, `<url>`, `<container>`
- Add an **inline comment** after `#` explaining flags and variations
- Include common variations (force, verbose, etc.)
- Don't include the program name if it's obvious from context but do include it for clarity:

```json
"commands": [
  "docker rm <id_or_name>",
  "docker rm -f <id_or_name>  # force remove even if running",
  "docker container prune  # removes all stopped containers"
]
```

### Descriptions

- Start with a **verb**: "Removes", "Lists", "Shows", "Creates"
- Keep it **one sentence**
- Be specific about scope: "Removes one or more containers" > "Removes containers"

## Adding actions to an existing program

Open the program's JSON file and add a new entry under `actions`:

```json
"my-new-action": {
  "aliases": ["what users search for"],
  "description": "What it does",
  "commands": ["myprogram --flag <arg>"]
}
```

## Updating `index.json`

When you add a new program, add a line to `index.json`:

```json
"myprogram": "myprogram - short description"
```

Keep the list **alphabetically sorted** by key.

## Rules

- Aliases and action names in **lowercase**
- JSON must be **valid** run `python3 -m json.tool catalog/myprogram.json` to check
- One program per file
- Don't duplicate commands that already exist in the file
- Keep aliases diverse the whole point is that different people search differently
