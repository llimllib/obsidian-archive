> **Hocus** is a self-hosted application that spins up ready-to-code, disposable development environments on your own servers in seconds. You define your dev environments as code and launch them instantly from your browser. It's a **self-hosted alternative** to **Gitpod** and **Github Codespaces**.

> Hocus is integrated with any Git provider that supports the SSH protocol, like GitHub, GitLab, BitBucket, or Gitea. It prebuilds dev environments on every commit for all branches like a CI system, enabling your team members to start coding with fresh, fully-configured dev environments right away. Whether you're fixing a bug, building a new feature, or conducting a code review, Hocus has you covered.

Looks pretty simple and useful.

Typescript with keycloak for auth and postgres for db. Uses [temporal](https://github.com/temporalio/temporal) for "microservice orchestration", which I admit I don't know exactly what that means.