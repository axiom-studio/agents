# Axiom Studio Agents

Public agent definitions and team blueprints for Axiom Studio.

## Repository Structure

```
agents/         # Agent library definitions
└── smb/        # Small business agent suite
teams/          # Pre-built team blueprints
└── smb/        # Small business team suites
```

## Skills

Agent skill dependencies are resolved from the [axiom-studio/skills](https://github.com/axiom-studio/skills) repository.
Each agent's `agent.yaml` declares required skills via their public source URLs.
When you install an agent, any missing skills are automatically fetched from their declared URLs.

## Getting Started

Add this repository as a source in your Axiom Studio marketplace to discover and deploy agents and teams.

## Contributing

All contributions are welcome. Please open a pull request with your agent or team definition.

## License

Apache 2.0 — see [LICENSE](./LICENSE).
