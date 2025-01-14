## How to make my own config?

- Go to custom folder

- cp example_chadrc.lua chadrc.lua
- cp example_init.lua init.lua

- The chadrc here is for editing nvchad default options etc.
- The init.lua here will be used for adding new plugins , new plugin configs , replace default plugin configs , adding new mappings.

## Replace default config of a plugin

- Use the default_plugin_config_replace table in chadrc.lua

- Example :

```lua
M.plugins = {
   default_plugin_config_replace = {
      lspconfig = "custom.lspconfig",
   },
}

-- this will replace lspconfig's default config with the file custom/lspconfig.lua
-- make sure you do :PackerCompile or :PackerSync after this since the packer_compiled.vim or packer_compiled.lua present in the ~/.config/nvim/plugin dir needs to update the paths!
```

### Add new plugins

- Go to init.lua file in custom folder
- Uncomment the line hooks.add line containing the "install_plugins" stuff

- example :

```lua

hooks.add("install_plugins", function(use)
   use {
       "folke/which-key.nvim"
        event = "something",
        config = function()
            require("custom.plugin_confs.whichkey")
        end
    }
 end)

-- so the path of the config here basically is in the custom/plugin_confs/whichkey.lua
```

### Add new mappings

```lua

 hooks.add("setup_mappings", function(map)
    map("n", "<leader>cc", "dd", opt) -- example to delete the buffer
    .... many more mappings ....
 end)

```

### Autocmds

- Well, for example you just create a new file called autochad_cmds.lua in the custom folder and require it in the init.lua file of the custom folder! BOOOM!!

### Files to edit

- Only files that are supposed to edited by the user are meant to be in the custom dir, default files in that folder are example_chadrc and example_init which can be just renamed by the user into chadrc.lua and init.lua .

- The rest of the files outside the custom folder will get overwritten by the update so don't put your config there!! Just put it in the custom folder.

(note : The docs will be refined and updated more if there are any inaccuracies)

## Lazy loading

- We lazy load almost 95% of the plugins, so we expect you to lazy load the plugins you've added to reduce startuptime. Don't want users making NvChad slow just because they didn't lazy load plugins they've added!

- Check [packer's readme](https://github.com/wbthomason/packer.nvim#specifying-plugins) for more info!

![lessgooo](https://cdn.discordapp.com/attachments/610012463907209227/891011437810577480/863483056531046450.png)
