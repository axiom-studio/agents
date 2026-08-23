# Kubernetes SRE Watcher

Kubernetes SRE Watcher observes Kubernetes events and workload state, identifies common operational failures, and sends concise evidence-first alerts to a configured Slack conversation.

## Required capabilities

- `openseal.kubernetes` 1.1.0 with `get_logs`, `get_resource`, `list_events`, and `list_resources`
- `skill-slack` 2.2.13 with `slack-send-message`
- A model-provider Vault credential
- A target Kubernetes cluster
- A Slack bot/signing-secret Vault credential and destination channel

The agent is detection-only. It does not receive Kubernetes mutation or remediation actions.

## Deployment

Install the listing from the AxiomStudio Official Agents marketplace source. Map its Kubernetes capability to the target tenant's cluster, configure the Slack Skill with tenant-owned Vault credentials, and bind the logical `sre-slack-channel` conversation endpoint to the operations channel.

No source credential, callback URL, cluster ID, workspace identity, or channel ID is embedded in this marketplace artifact.
