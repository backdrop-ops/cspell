# Backdrop cspell Dictionary

This project holds the `cspell` dictionary and configuration for use by Backdrop projects (both core and contrib).

It is intended to be used with the [cspell Library](https://github.com/streetsidesoftware/cspell) and [cspell GitHub Action](https://github.com/streetsidesoftware/cspell-action).

## Enable Spell-Checking on Your Backdrop Project

Create a `.github/workflows/cspell.yml` file with the following content:

```
name: Coding standards
on:
  pull_request:
    branches: [*]

jobs:
  spellcheck:
    name: Check spelling
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v6
      name: Checkout code
    - uses: actions/checkout@v6
      name: Checkout cspell config
      with:
        repository: backdrop-ops/cspell
        path: .cspell
    - uses: streetsidesoftware/cspell-action@v8
      name: Run CSpell
      with:
        incremental_files_only: true
        config: '.cspell/cspell.json'
```

## Adding New Words to the Dictionary

File a pull request against this repository to add a word to `dictionary.txt`. Put the word in alphabetical order

This repository does not currently use tags. So upon changing `dictionary.txt` in the `main` branch, re-run the action on your pull request.

## Advanced Usage

If needing to modify the options in `cspell.json`, your project can specify its own `cspell.json` file by changing the `config` option in the GitHub action. For a full list of configuration options for `cspell`, see the [cspell documentation](https://cspell.org/docs/Configuration/properties).
