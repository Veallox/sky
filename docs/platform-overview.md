# Web Terminal Platform Overview

## Goal
Create a browser-based platform ("like Chrome/Firefox") that runs Linux terminals and security tools in isolated workspaces, making ethical hacking workflows easy and safe.

## Core Capabilities
- **Browser-based workspaces**: each user session runs in a container/VM with a Linux shell and preinstalled tools.
- **App launcher**: curated list of CLI and GUI apps (e.g., terminal, editors, packet analyzers) exposed in the browser.
- **Workspace persistence**: optional snapshots and storage so users can resume sessions.
- **Safety controls**: role-based access, activity logging, rate limits, and strict outbound network policies.
- **Collaboration**: shareable sessions, read-only views, and instructor-led labs.

## User Experience
1. User signs in and chooses a lab or tool preset.
2. Platform provisions an isolated workspace with a Linux terminal.
3. User runs tools via terminal or a web-based GUI catalog.
4. Session can be saved, exported, or discarded on exit.

## Security & Compliance Requirements
- **Isolation**: run each workspace in a container or micro-VM.
- **Network egress controls**: allow only approved targets or sandboxed environments.
- **Auditability**: log commands, file changes, and tool usage.
- **Consent & scope**: enforce explicit rules for targets and provide on-screen scope warnings.

## High-Level Architecture
- **Frontend**: Web app (React/Next.js) with terminal UI (xterm.js) and app launcher.
- **Workspace Orchestrator**: API service that provisions containers/VMs.
- **Compute Pool**: Kubernetes or similar for scheduling sandboxes.
- **Storage**: object storage for snapshots and user files.
- **Gateway**: secure websocket proxy for terminal streaming.

## MVP Scope
- Login + basic workspace provisioning
- Terminal in the browser
- Preinstalled security tools
- Simple audit logs
- Admin console for managing tool presets

## Pre-Deployment Testing
- **Automated checks**: unit/integration tests for the orchestrator, workspace lifecycle, and network policy enforcement.
- **Security validation**: container escape tests, least-privilege checks, and dependency vulnerability scans.
- **Performance tests**: workspace boot time, terminal latency, and concurrent session load.
- **User acceptance**: run lab scenarios end-to-end with audit logging enabled.
- **Staging rollout**: deploy to a staging cluster that mirrors production (quotas, routing, logging).

## Store-Readiness Considerations (If Shipping Mobile Apps)
- **Scope control**: ensure the app only targets authorized lab environments and clearly communicates scope/consent.
- **Policy compliance**: review Apple App Store Review Guidelines and Google Play Developer Policies for security tools, remote execution, and user-generated content.
- **Accountability**: provide in-app reporting, abuse handling, and clear terms of service.
- **Privacy**: document data collection, telemetry, and logging in the app privacy disclosures.
- **Functional review**: verify all features listed in pricing plans are available and stable before release.

## Open Questions
- What tool presets are required for the first release?
- Is GUI app streaming required in MVP or after initial launch?
- What target environments will users be allowed to access?
