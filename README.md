<img src="https://github.com/echasnovski/media/blob/main/mini.nvim/logo/logo_statusline.png" style="width: 100%"/>

<!-- badges: start -->
[![GitHub license](https://badgen.net/github/license/echasnovski/mini.nvim)](https://github.com/echasnovski/mini.nvim/blob/main/LICENSE)
<!-- badges: end -->

### Minimal and fast statusline module with opinionated default look

See more details in [Features](#features) and [help file](doc/mini-statusline.txt).

---

⦿ This is a fork from [mini.statusline](https://github.com/echasnovski/mini.statusline) which is part of [mini.nvim](https://github.com/echasnovski/mini.nvim) library.

⦿ Here we have flexible components available using the `MiniStatusline.flexibleGroups` which takes in a `opts` table which can have `groups` table and an optional `preprocess` function. Each table in the groups table defines a section with the following fields:
```lua
-- @param priority: optional int - A value which decides truncating order of components. Lower priority components are hidden before higher priority ones
-- @param string: function or array of functions - If function, should return the section string. Array of function can be used to give smaller versions of the string, in which the first one that fits the window width is selected. Eg :- {filename_func, filenameShort_func}
-- @param hl: optional string - The highlight group
-- @param hl_fn: optional function - A function which returns a highlight group, useful dynamic highlight groups like those based on vim mode
```

⦿ See the repository page to learn about common design principles and configuration recipes.

---

If you want to help this project grow but don't know where to start, check out [contributing guides of 'mini.nvim'](https://github.com/echasnovski/mini.nvim/blob/main/CONTRIBUTING.md) or leave a Github star for 'mini.nvim' project and/or any its standalone Git repositories.

## Demo

https://user-images.githubusercontent.com/24854248/173045208-42463c8f-a2ac-488d-9d30-216891f4bb51.mp4

## Features

- Define own custom statusline structure for active and inactive windows. This is done with a function which should return string appropriate for |statusline|. Its code should be similar to default one with structure:
    - Compute string data for every section you want to be displayed.
    - Combine them in groups with `MiniStatusline.combine_groups()`.
- Built-in active mode indicator with colors.
- Sections can hide information when window is too narrow (specific window width is configurable per section).

## Dependencies

For full experience needs (still works without any of suggestions):

- [Nerd font](https://www.nerdfonts.com/) and enabled ['mini.icons'](https://github.com/echasnovski/mini.nvim/blob/main/readmes/mini-icons.md) module to show filetype icons. Can fall back to using [nvim-tree/nvim-web-devicons](https://github.com/nvim-tree/nvim-web-devicons) plugin.

- Enabled ['mini.git'](https://github.com/echasnovski/mini.nvim/blob/main/readmes/mini-git.md) and ['mini.diff'](https://github.com/echasnovski/mini.nvim/blob/main/readmes/mini-diff.md) modules to show Git and diff related information. Can fall back to using [lewis6991/gitsigns.nvim](https://github.com/lewis6991/gitsigns.nvim) plugin.

## Installation

This plugin can be installed as part of 'mini.nvim' library (**recommended**) or as a standalone Git repository.

There are two branches to install from:

- `main` (default, **recommended**) will have latest development version of plugin. All changes since last stable release should be perceived as being in beta testing phase (meaning they already passed alpha-testing and are moderately settled).
- `stable` will be updated only upon releases with code tested during public beta-testing phase in `main` branch.

Here are code snippets for some common installation methods (use only one):

<details>
<summary>With <a href="https://github.com/echasnovski/mini.nvim/blob/main/readmes/mini-deps.md">mini.deps</a></summary>
<table>
    <thead>
        <tr>
            <th>Github repo</th>
            <th>Branch</th> <th>Code snippet</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=2>'mini.nvim' library</td> <td>Main</td> <td rowspan=2><i>Follow recommended 'mini.deps' installation</i></td>
        </tr>
        <tr>
            <td>Stable</td>
        </tr>
        <tr>
            <td rowspan=2>Standalone plugin</td> <td>Main</td> <td><code>add('echasnovski/mini.statusline')</code></td>
        </tr>
        <tr>
            <td>Stable</td> <td><code>add({ source = 'echasnovski/mini.statusline', checkout = 'stable' })</code></td>
        </tr>
    </tbody>
</table>
</details>

<details>
<summary>With <a href="https://github.com/folke/lazy.nvim">folke/lazy.nvim</a></summary>
<table>
    <thead>
        <tr>
            <th>Github repo</th>
            <th>Branch</th> <th>Code snippet</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=2>'mini.nvim' library</td>
            <td>Main</td> <td><code>{ 'echasnovski/mini.nvim', version = false },</code></td>
        </tr>
        <tr>
            <td>Stable</td> <td><code>{ 'echasnovski/mini.nvim', version = '*' },</code></td>
        </tr>
        <tr>
            <td rowspan=2>Standalone plugin</td>
            <td>Main</td> <td><code>{ 'echasnovski/mini.statusline', version = false },</code></td>
        </tr>
        <tr>
            <td>Stable</td> <td><code>{ 'echasnovski/mini.statusline', version = '*' },</code></td>
        </tr>
    </tbody>
</table>
</details>

<details>
<summary>With <a href="https://github.com/junegunn/vim-plug">junegunn/vim-plug</a></summary>
<table>
    <thead>
        <tr>
            <th>Github repo</th>
            <th>Branch</th> <th>Code snippet</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=2>'mini.nvim' library</td>
            <td>Main</td> <td><code>Plug 'echasnovski/mini.nvim'</code></td>
        </tr>
        <tr>
            <td>Stable</td> <td><code>Plug 'echasnovski/mini.nvim', { 'branch': 'stable' }</code></td>
        </tr>
        <tr>
            <td rowspan=2>Standalone plugin</td> <td>Main</td> <td><code>Plug 'echasnovski/mini.statusline'</code></td>
        </tr>
        <tr>
            <td>Stable</td> <td><code>Plug 'echasnovski/mini.statusline', { 'branch': 'stable' }</code></td>
        </tr>
    </tbody>
</table>
</details>

<br>

**Important**: don't forget to call `require('mini.statusline').setup()` to enable its functionality.

**Note**: if you are on Windows, there might be problems with too long file paths (like `error: unable to create file <some file name>: Filename too long`). Try doing one of the following:
- Enable corresponding git global config value: `git config --system core.longpaths true`. Then try to reinstall.
- Install plugin in other place with shorter path.

## Default config

```lua
-- No need to copy this inside `setup()`. Will be used automatically.
{
  -- Content of statusline as functions which return statusline string. See
  -- `:h statusline` and code of default contents (used instead of `nil`).
  content = {
    -- Content for active window
    active = nil,
    -- Content for inactive window(s)
    inactive = nil,
  },

  -- Whether to use icons by default
  use_icons = true,
}
```

## Similar plugins

- [nvim-lualine/lualine.nvim](https://github.com/nvim-lualine/lualine.nvim)
