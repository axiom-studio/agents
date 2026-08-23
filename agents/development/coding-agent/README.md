# OpenSeal Coding Agent

The OpenSeal Coding Agent uses a persistent framework-native Workspace for repository files and bounded development commands. Authenticated Git clone and push are fixed native operations backed by a short-lived Vault grant; arbitrary commands never receive credentials.

## Required capabilities

- A model-provider Vault credential
- A GitHub token Vault credential bound to the Workspace's `GITHUB` slot
- `skill-github` 1.0.0 bound to the same GitHub credential for governed pull-request delivery
- `openseal.kubernetes` 1.1.0 mapped to the target environment cluster
- `skill-slack` 2.2.13 with a Slack bot/signing-secret Vault credential and destination channel
- An Atlas execution host that supports native Workspace API version 14

The default deployment profile uses a retained 20Gi Workspace, allows bounded coding tools, restricts credentialed Git traffic to `github.com`, and requires an explicit grant for Git push. Kubernetes mutation remains a separate governed Skill action and does not follow from Workspace ownership.

## Authority boundaries

The bundle grants capabilities independently and fails closed when any required
binding is absent:

- Workspace files are read/write only inside the Agent's retained claim; path
  traversal and symlink escapes are rejected by the runtime.
- Arbitrary commands are credentialless, network-denied, duration-bounded, and
  restricted to `bun`, `bunx`, `git`, and `rg`.
- Authenticated Git clone and push are fixed native operations. They receive a
  short-lived `github_token` grant only for the explicitly listed
  `axiom-studio` repositories on `github.com`; push is an explicit policy bit
  separate from clone.
- GitHub API actions are a separate Skill binding. Repository arguments are
  narrowed to the same reviewed repository set, and pull-request creation is
  classified as an external side effect.
- Kubernetes reads and mutations use the target environment's
  `openseal.kubernetes` runtime capability. Workspace or Git authority does not
  imply cluster authority.
- Slack can invoke the Agent only through the mapped provider connection and
  destination. Provider credentials remain Vault references.
- The Agent may run four conversations concurrently, while its default
  Workspace serializes mutations until isolated task worktrees are enabled.
