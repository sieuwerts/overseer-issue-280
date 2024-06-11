overseer-issue-280
==================

Repostory to showcase / replicate the issue mentioned [here](https://github.com/stevearc/overseer.nvim/issues/280).

Overseer plugin configuration:
------------------------------

```Lua
return {
	"stevearc/overseer.nvim",
	dependencies = {
		"nvim-telescope/telescope.nvim",
		"nvim-lua/plenary.nvim",
		"stevearc/dressing.nvim",
	},
	config = function()
		local opts = {
			task_list = {
				max_height = { 70, 0.4 },
			},
		}

		require("overseer").setup(opts)
	end,
}
```

Steps to reproduce:
-------------------

1.	Clone this repository.
2.	Open README.md in Neovim, run `:OverseerRun` (or `:OverseerInfo`). You should now see both `make foo` and `make bar` in the list (or 3/3 tasks available for `make` for `:OverseerInfo`).
3.	Close info/run window.
4.	Run `:OverseerRun` (or `:OverseerInfo`) again and now the `make bar` target will not be visible (and `:OverseerInfo` will only contain 2/2 tasks available).
5.	Restarting Neovim will cause overseer to find the target again, but only once (issue remains).

I.e the targets from the *included* Makefile will only be visible/found the *first* time overseer is invoked.
