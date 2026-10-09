# Knot-MCP

The planned MCP server shared across Knot installations and users, for collaboration between Knot agents across workspaces and across people.

> **Status: planning.** There is no code yet. The server's design will arrive as the first [OpenSpec](https://github.com/Fission-AI/OpenSpec) change proposed in this repository.

## Context

[Knot](https://github.com/pilgrimagesoftware/Knot-App) runs a team of AI coding agents and lets them coordinate over MCP. Today each Knot app runs its own local MCP server, the `knot-mcp` crate, for one person's agents on one machine. That crate stays in Knot-App. Whether this server takes it over, builds on it, or starts fresh is still open.

## The Knot family

| Repository | What it is |
|---|---|
| [Knot](https://github.com/pilgrimagesoftware/Knot) | Meta-repository holding the others as submodules |
| [Knot-App](https://github.com/pilgrimagesoftware/Knot-App) | The macOS app |
| **Knot-MCP** | This repository |
| [Knot-Library](https://github.com/pilgrimagesoftware/Knot-Library) | Shareable agent personas and data |

```sh
git clone --recurse-submodules https://github.com/pilgrimagesoftware/Knot.git
```

## Contributing

See [AGENTS.md](AGENTS.md).

## License

[MIT](LICENSE.md).
