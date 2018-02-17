
Snippets and hacks for JetBrains products


# Pycharm polish spellchecking
## Generate polish dict with aspell
### Install aspell
    sudo apt install apsell aspell-pl
### Generate dict in proper format
    aspell --lang pl dump master | aspell --lang pl expand | tr ' ' '\n' > pl.dic

## Configure Pycharm

### Copy file to desired location
Move the `pl.dic` to the desired location eg. `~/.dicts/pl`

### Select location in Pycharm settings
    settings>editor>spelling>dictionaries>+(green plus in right top)
and add chosen before path



# Shortcuts

- `crel+e` - recent files
- `alt+insert` - create new file
- `shft+ctrl+<arrow>` - resize window
- `alt+enter -> inject language` - inject piece of code eg. json
- `alt+slash` - cyclic expand word
- `alt+home` - focus nav bar 
- `alt+9` - open version control window

- `ctrl+ pageUp/PageDown` (chrome) switch tab
