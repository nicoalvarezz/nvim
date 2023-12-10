# NeoVim Minimal Setup

Welcome to my NeoVim configurations repository! Here, you'll find my minimalistic setup designed to enhance your NeoVim experience. Featuring fantastic plugins like Telescope and LSP configuration, this setup is easy to install and ready to supercharge your workflow.

## Installation
Simply go to the `/lua/nicoalvarezz/packer.lua` file source it (using `:so`) and install all the plugins using `:PakcerSync`. That will install and set up the following plugins:

- telescope
- treesitter
- harpoon
- undotree
- fugitive
- lsp-zero
- mason

## Usage Suggestion
To optimize your experience with these minimalist configs, I recommend forking this repository. This way, you can seamlessly integrate your preferred plugins and tailor your NeoVim configurations to suit your individual preferences. Happy Coding! 🚀

## Notes
- When referred to `<leader>` throughout this `README`, it means the main key that will be used to make most of the remaps. In this configs, the default `<leader>` is `Space`
	- You can change this in the `/lua/nicoalvarezz/set.lua`
	```
	vim.g.mapleader = " "
    ```
* The theme will be et automatically to [horizon](https://github.com/LunarVim/horizon.nvim)
	* You can install any other them and set it in the `set.lua` file previously mentioned
* There are some other sets and remaps that you can checkout in the `set.lua` and `rempa.lua` files

## Telescope
[Telescope.nvim](https://github.com/nvim-telescope/telescope.nvim) is a powerful and extensible fuzzy finder and interactive search tool for NeoVim. It simplifies navigating and exploring your files, projects, and data with its intuitive interface. Whether you're searching for files, live previews, or interacting with LSP symbols, Telescope provides a seamless and efficient way to interact with your codebase, making it an essential tool for enhancing productivity in your NeoVim workflow.

Telescope's primary key mappings have been configured in `/after/plugin/telescope.lua`
```
# find all files
vim.keymap.set('n', '<leader>ff', builtin.find_files, {})

# find git files only
vim.keymap.set('n', '<leader>gf', builtin.git_files, {})

# live grep for fuzzy finding
vim.keymap.set('n', '<leader>fg', builtin.live_grep, {})

# find in the current buffer
vim.keymap.set('n', '<leader>fb', builtin.buffers, {})
```

## Treesitter
The goal of [nvim-treesitter](https://github.com/nvim-treesitter/nvim-treesitter) is both to provide a simple and easy way to use the interface for [tree-sitter](https://github.com/tree-sitter/tree-sitter) in Neovim and to provide some basic functionality such as highlighting.
This will simply help to set up the color of the editor as it should be.

## Harpoon
[Harpoon](https://github.com/ThePrimeagen/harpoon/tree/harpoon2) is a dynamic and versatile navigation manager for NeoVim. With its focus on project-based workflows, Harpoon allows you to effortlessly manage and switch between different files.

Harpoons's primary key mappings have been configured in `/after/plugin/harpoon.lua`
```

# Add file to harpoon
vim.keymap.set("n", "<leader>a", mark.add_file)

# show harpoon menu
vim.keymap.set("n", "<C-e>", ui.toggle_quick_menu)

# clear all harpoon files
vim.keymap.set("n", "<C-x>", mark.clear_all)

# remove current file from harpoon
vim.keymap.set("n", "<leader>rf", mark.rm_file)

# move through files using harpoon
vim.keymap.set("n", "<leader>h", function() ui.nav_file(1) end)
vim.keymap.set("n", "<leader>t", function() ui.nav_file(2) end)
vim.keymap.set("n", "<leader>n", function() ui.nav_file(3) end)
vim.keymap.set("n", "<leader>s", function() ui.nav_file(4) end)
```

This version of harpoon is deprecated, so soon [harpoon2](https://github.com/ThePrimeagen/harpoon/tree/harpoon2) will be used instead.

## Undotree
[Undotree](https://github.com/mbbill/undotree) visualises the undo history and makes it easy to browse and switch between different undo branches. This is a very interesting plugin that will allow you to browse through changes very easily. 

Undootree's primary key mappings have been configured in `/after/plugin/undotree.lua`
```
vim.keymap.set("n", "<leader>u", vim.cmd.UndotreeToggle)
```

Currently the remap is only set to show the undo tree menu. This menu will show the branches of the changes and a lot of information about the changes. Checkout the documentation to learn more about this powerful plugin.

## Fugitive
[Fugitive](https://github.com/tpope/vim-fugitive) is a powerful Git wrapper for NeoVim, designed to seamlessly integrate Git commands into your editing workflow. This plugin provides a range of features, from status information to interactive Git blame views. With Fugitive, you can efficiently navigate through Git repositories, visualise changes, and perform Git operations—all without leaving the comfort of your NeoVim environment.

Fugitive's primary key mappings have been configured in `/after/plugin/fugitive.lua`
```
# Show git status
vim.keymap.set("n", "<leader>gs", vim.cmd.Git)
```

Checkout the docs to see all the possible git commands that you can run from your nvim workflow.

## lsp-zero
[Lsp-zero](https://github.com/VonHeikemen/lsp-zero.nvim) is a collection of functions that will help you setup Neovim's LSP client, so you can get IDE-like features with minimum effort.

All the required configs to set up language server protocol (lsp) are already set up in the file `/after/plugin/lsp.lua`. In here you can find the configs that will start up lsp, as well as some keybinding and and the set up of your language servers.

To add a new lsp to your nvim you will have to add the following config to the `lsp.lua`
```
require('lspconfig').<lsp_name>.setup({
	on_attach = function(client)
		# to make sure colors are maintained after lsp being applied
		client.server_capabilities.semanticTokensProvider = nil
	end,
})
```

Lsp's primary key mappings have been configured already:
```

# Enter to confirm completion
<CR>

# to trigger completion
<C-Space>

# jump to definiton
vim.keymap.set("n", "gd", function() vim.lsp.buf.definition() end, opts)

# hover definition
vim.keymap.set("n", "K", function() vim.lsp.buf.hover() end, opts)

# actions such as adding missing imports
vim.keymap.set("n", "<leader>vca", function() vim.lsp.buf.code_action() end, opts)

# show all references (of whatever the cursros in)
vim.keymap.set("n", "<leader>vrr", function() vim.lsp.buf.references() end, opts)

# refacter rename
vim.keymap.set("n", "<leader>vrn", function() vim.lsp.buf.rename() end, opts)
```

However, for lsp to fully work, you need to install the desired lsp using `Mason`

## Mason
[Mason](https://github.com/williamboman/mason.nvim) is a Neovim plugin that allows you to easily manage external editor tooling such as LSP servers.
Refer to the documentation for a comprehensive list of commands required to install any LSP server.

## Reference
https://www.youtube.com/watch?v=w7i4amO_zaE
