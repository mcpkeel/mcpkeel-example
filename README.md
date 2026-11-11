# mcpkeel-example

A small repository that uses [mcpkeel](https://github.com/mcpkeel/mcpkeel) the way a team would: an MCP config, the `mcp.lock` that pins it, and two workflows.

| File | What it does |
| --- | --- |
| [`.mcp.json`](.mcp.json) | Five public MCP servers, each pinned to an exact release. |
| [`mcp.lock`](mcp.lock) | What those servers told an agent when they were pinned: tools, descriptions, schemas, instructions, and the package release and digest that run. Written by `npx mcpkeel init`. |
| [`mcp-verify.yml`](.github/workflows/mcp-verify.yml) | On pull requests and every day: `mcpkeel verify --probe`, with the changes uploaded to code scanning. Fails if anything drifted. |
| [`mcp-update.yml`](.github/workflows/mcp-update.yml) | Every Monday: opens a pull request that accepts the current definitions, with mcpkeel's report as its body. |

The servers are pinned to exact versions, so a red `MCP drift` run here means a server sent something different from what its pinned release sent before. For what changes when you leave versions unpinned, see mcpkeel's nightly [drift feed](https://github.com/mcpkeel/mcpkeel/tree/canary-data).

## Try it on your own repository

```sh
npx mcpkeel init      # writes mcp.lock from your MCP config
npx mcpkeel verify    # exit 1 if a server changed
```

Then copy the two workflows.
