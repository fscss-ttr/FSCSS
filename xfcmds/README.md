# xfcmds

IDE command scripts for FSCSS, written in the `.xfcmd` sentence format.

The [FSCSS IDE](https://fscss.devtem.org/ide) reads this folder from GitHub. It uses it to run commands you type in the terminal and to set up packages when you enable them.

- Full tutorial: https://fscss.devtem.org/xfcmds-guide
- IDE guide: https://fscss.devtem.org/ide-guide

## What is in this folder

```
xfcmds/
  cmd.json                 registry: maps names to scripts
  hello.xfcmd              command: xfcmd hello
  starter.xfcmd            command: xfcmd starter
  multipage.xfcmd          command: xfcmd multipage
  imports-demo.xfcmd       command: xfcmd imports-demo
  snippets-pack.xfcmd      command: xfcmd snippets-pack
  st-core.xfcmd            package hook: runs on libon st-core
  templates/
    command.template.xfcmd
    package-enable.template.xfcmd
    package-disable.template.xfcmd
```

## Quick start

Open the IDE, open the terminal with `Ctrl` + `` ` ``, then:

```
xfcmd list              show everything in this folder
xfcmd starter           create a small project and open the preview
xfcmd multipage         two page site with a shared partial
xfcmd imports-demo      workspace imports with a shared file
xfcmd snippets-pack     add editor snippets
xfcmd hello             print a greeting
libck st-core           check a package, then type yes to enable it
```

## Included scripts

| Name | Run with | What it does |
|---|---|---|
| `hello` | `xfcmd hello` | Prints a message, lists your files, shows a toast. |
| `starter` | `xfcmd starter` | Creates `starter/` with a theme, `index.html` and `app.js`. Sets the theme as the entry file, compiles, shows the preview. |
| `multipage` | `xfcmd multipage` | Creates `site/` with a partial (`_base.fscss`), a stylesheet that imports it, and two linked pages. Compiles, shows the preview, prints routes and dependencies. |
| `imports-demo` | `xfcmd imports-demo` | Creates `demo-imports/` where `main.fscss` imports two files that share a third. Shows that the shared file is included once. |
| `snippets-pack` | `xfcmd snippets-pack` | Adds the snippets `card`, `flexc` and `grid3`. |
| `st-core` | `libon st-core` | Package hook. Adds one snippet per `st-*` helper and creates `demos/st-core-demo.fscss`. |

Notes:

- Scripts that call `set entry` change your entry file. You can change it back in Settings.
- `create file` never overwrites. If a file exists it is kept.
- Snippets added by commands last until you reload the page. Snippets added by an enabled package are saved.

## The registry: cmd.json

```json
{
  "xfcmds": 1,
  "about": "IDE command scripts for FSCSS packages.",
  "packages": {
    "st-core": {
      "enable": "st-core.xfcmd",
      "disable": "st-core.disable.xfcmd",
      "about": "Adds st-* helper snippets and a demo file"
    }
  },
  "commands": {
    "hello": { "script": "hello.xfcmd", "about": "Prints a greeting" }
  }
}
```

| Key | Meaning |
|---|---|
| `packages.<name>.enable` | Script that runs on `libon <name>` (or `yes` after `libck`). |
| `packages.<name>.disable` | Optional. Runs on `liboff <name>`. |
| `commands.<name>.script` | Script that runs on `xfcmd <name>`. |
| `about` | One line shown by `xfcmd list`. |

Script paths are relative to this folder. A package name must match the `name` in that package's `package.json`.

The IDE loads `cmd.json` from:
`https://raw.githubusercontent.com/fscss-ttr/FSCSS/refs/heads/main/xfcmds/cmd.json`

If it cannot be loaded, the IDE falls back to a built-in copy of the scripts in this folder. `xfcmd list` tells you which one is active. After you push a change, run `xfcmd refresh` in the IDE.

## Which script runs when a package is enabled

1. The package's own `package.json`, if it has an `xfcmd` field:
   ```json
   { "xfcmd": "./xfcmds/enable.xfcmd" }
   ```
   or
   ```json
   { "xfcmd": { "enable": "./xfcmds/enable.xfcmd", "disable": "./xfcmds/disable.xfcmd" } }
   ```
2. `packages.<name>` in this folder's `cmd.json`.
3. A built-in default: a message, helper snippets, and the import line to use.

## The .xfcmd format

One sentence per line, run top to bottom. Lines starting with `#` or `//` are comments. Verbs are not case sensitive. Text goes in double quotes.

| Sentence | Effect |
|---|---|
| `say "text"` | Print a line. Also `print` and `info`. |
| `warn "text"` / `error "text"` | Print at warning or error level. |
| `toast "text" ok` | Show a toast. Last word is optional: `ok`, `warn`, `err`. |
| `add import <name>` | Insert `@import((*) from name)` at the top of the active FSCSS file. |
| `create file "<path>" with:` | Create a file from the lines that follow. The block ends at a line that says `end`. |
| `create file "<path>" with "text"` | Create a file from one quoted string. Use `\n` for new lines. |
| `open file <path>` | Open a file in the editor. |
| `set entry <path>` | Make a file the entry file. |
| `compile` / `compile all` / `preview` | Compile the active file (or entry), every root file, or compile and show the preview. |
| `show <view>` | `files`, `components`, `snippets`, `tools`, `terminal`, `problems`, `css`, `preview`. |
| `add snippet <key> "<title>" as "<body>"` | Add an editor snippet. |
| `add snippets for helpers` | One snippet per helper in the package. Package scripts only. |
| `run command "<command>"` | Run a terminal command from the allowed list below. |
| `wait <n> ms` | Pause, up to 3000 ms. |

Variables, filled in when the script runs:

| Variable | Value |
|---|---|
| `{name}` `{version}` `{author}` `{description}` `{license}` `{repo}` | From the package's `package.json`. |
| `{import}` | Import name, from the main module file name (`st-core@v2.fscss` gives `st-core@v2`). |
| `{helpers}` | Helper names, comma separated. |
| `{fscss}` | The `fscss_version` range. |
| `{file}` | The last file created or kept by `create file`. |

Only these names are replaced. Other text in braces is left alone, so FSCSS like `.card{ ... }` inside a `create file` block is safe. In commands (not package scripts) the package variables are empty.

Escapes inside quotes: `\n` new line, `\t` tab, `\"` quote, `\\` backslash. In a snippet body, write `\\$name` for a literal `$name`, and use `${1:default}` for tab stops.

## Limits and safety

- Scripts are parsed completely before anything runs. One bad sentence means nothing runs and you get the line number.
- A runtime error stops the script at that line. During enable, snippets added so far are removed and the package is not marked enabled. Files already created stay.
- Maximum 200 sentences per script and 3000 ms per `wait`.
- Scripts are never evaluated as JavaScript. They can only do what the table above allows.
- `run command` allows only: `compile`, `run`, `all`, `preview`, `ls`, `open`, `new`, `libs`, `clear`, `theme`, `routes`, `deps`, `resolve`.
- Remote scripts are fetched from `raw.githubusercontent.com` only.
- `liboff` never deletes files.

## Templates

Copy a template, rename it, register it in `cmd.json`.

| Template | Use it for |
|---|---|
| `templates/command.template.xfcmd` | A standalone command run with `xfcmd <name>`. |
| `templates/package-enable.template.xfcmd` | The enable script of a package. Uses package variables. |
| `templates/package-disable.template.xfcmd` | The disable script of a package. |

A package enable script, as a starting point:

```
say "Setting up {name}@{version} by {author}"
add snippets for helpers
create file "demos/{name}-demo.fscss" with:
  /* {name} demo */
  @import((*) from {import})
end
open file {file}
compile
show terminal
```

Order matters. Create the file, open it, then compile, because `compile` works on the active file.

## Adding your own

1. Write `my-script.xfcmd` in this folder (or in `templates/` if it is only a template).
2. Register it in `cmd.json` under `commands` or `packages`.
3. Test in the IDE before opening a pull request:
   ```
   xfcmd check my-script.xfcmd     parse it and list problems
   xfcmd eval say "hi"             run one sentence
   xfcmd run my-script.xfcmd       run a workspace copy
   xfcmd refresh                   reload cmd.json after you push
   ```
   To test a package script end to end, run `libck <package>` and answer `yes`.
4. Checklist:
   - Put created files in their own folder (`my-demo/`) so they never collide with user files.
   - Do not rely on `set entry` unless the script is about a project setup.
   - End with a `say` that tells the user what to do next.
   - Keep it under 200 sentences.
   - Keep `cmd.json` valid JSON.

`xfcmd check` on a package script shows empty variables (for example `demos/-demo.fscss`). That is expected. The real values are filled in during `libon`.

## Troubleshooting

| Message | Fix |
|---|---|
| `Unknown sentence: ...` | The line matches no sentence. Check the verb and that text is in double quotes. |
| `create file block is missing "end"` | Add a line that says `end` after the block. |
| `"x" is not allowed in scripts` | `run command` only accepts the allowed list above. |
| `xfcmd line N: no such file` | `open file` or `set entry` named a file that does not exist yet. Create it first. |
| `xfcmd list` says built-in fallback | The GitHub `cmd.json` was not found. Check the path and branch, then `xfcmd refresh`. |
| `Nothing to confirm.` | The `yes` or `no` prompt expired after 2 minutes. Run `libck` again. |

## License

MIT, same as the rest of the FSCSS repository.
