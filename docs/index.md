# Command Reference

A personal DevOps/engineering cheat sheet — the commands and setup steps I reach
for often, in one place. Quick-reference notes for a Java/Spring backend workflow.

!!! tip "How to use this"
    Every page is a flat list of commands with a one-line description above each.
    Use your browser's find (Ctrl/Cmd+F) or the search box to jump straight to what
    you need. Placeholders in `<angle_brackets>` are meant to be replaced.

## Setup

One-time installation and configuration guides.

| Guide | What it covers |
|-------|----------------|
| [Server Setup](setup/server.md) | Installing `.deb`/`.rpm` packages, Java 21, Maven, Git, Docker, PostgreSQL 17 |
| [Kafka (Confluent, KRaft)](setup/kafka.md) | Confluent Platform 7.7 in KRaft mode: install, properties, storage format, systemd services, Kafka UI |

## Commands

Day-to-day command references.

| Reference | What it covers |
|-----------|----------------|
| [Linux](commands/linux.md) | Users, files, compression, networking, processes, systemd |
| [Git](commands/git.md) | Init, logs, cherry-pick, amend, reset/revert, aliases |
| [Docker](commands/docker.md) | Containers, images, networks, volumes |
| [Kubernetes](commands/kubernetes.md) | kubectl for nodes, deployments, pods, services, config, and minikube |
| [Kafka](commands/kafka.md) | Topics, producers, consumers, consumer groups, configs, logs |
