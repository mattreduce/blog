---
title: Projects
description: Some of my open source work
toc: true
authors: []
date: 2021-10-03T13:04:54-07:00
lastmod: 2021-10-03T15:28:00-07:00
draft: false
weight: 1
---

One of the areas I focus on as a red teamer is the building and optimization of
capabilities through development and infrastructure automation (or really
anything under Tactic [TA0042](https://attack.mitre.org/tactics/TA0042/) for
fellow MITRE ATT&CK:copyright: wonks).

I'm fortunate to have time to spend on open source work related to those two!
:smile: Here are some of my recent projects:

## :biohazard_sign: Venus

<img src="../images/projects/venus.png" style="width:8em; float:right; 
margin: 0 0 1em 0.5em" />

[github.com/MythicAgents/venus](https://github.com/MythicAgents/venus)

| Type                           | Stack   |
|:-------------------------------|:--------|
| Stage 0/1 payload, persistence | Node.js |

Venus is a [VS Code](https://code.visualstudio.com/) text editor extension that
acts as malware/implant/agent that you can control via the
[Mythic](https://github.com/its-a-feature/Mythic) command and control (C2)
framework.

It supports any OS that can run Visual Studio Code but has been tested on
macOS, Windows, and Ubuntu Linux. Its functionality is implemented with
platform-agnostic APIs, providing the same minimal set of capabilities on any
target.

Venus provides the flexibility to gain initial access on endpoints of any
flavor in an unusual and unexpected package, providing a jumping off point for
host triage and the deployment of other tools. You can also use Venus to build
and drop a malicious VS Code extension as a persistence mechanism, as
[others](https://medium.com/secarmalabs/using-visual-studio-code-extensions-for-persistence-a65c940b7ea6)
have [written](https://www.mdsec.co.uk/2021/01/macos-post-exploitation-shenanigans-with-vscode-extensions/) about.

## :disguised_face: Sockdrawer

[github.com/mattreduce/sockdrawer](https://github.com/mattreduce/sockdrawer)  
[sockdrawer.app](https://sockdrawer.app/)

| Type    | Stack                 |
|:--------|:----------------------|
| Web app | Ruby/Rails/PostgreSQL |

Sockdrawer is an alias identity manager for Red Teams, OSINT collectors,
journalists, and privacy-conscious people. Its name comes from the term
sockpuppet.

Individuals and teams can use the tool to generate alias identities and keep
notes on their use. You can keep up with current and planned feature work on
the project's public [Kanban
board](https://github.com/mattreduce/sockdrawer/projects/1).

Sockdrawer is a Ruby on Rails web application that comes with a
[Dockerfile](https://github.com/mattreduce/sockdrawer/blob/main/Dockerfile) for
development, testing and production. The project also [includes
configuration](https://github.com/mattreduce/sockdrawer/blob/main/docker-compose.yml)
for conveniently running the app with [Docker
Compose](https://docs.docker.com/compose/).

I make sure Sockdrawer is still working as it evolves through unit testing
([suite](https://github.com/mattreduce/sockdrawer/tree/main/spec)) with RSpec,
acceptance testing
([suite](https://github.com/mattreduce/sockdrawer/tree/main/features)) with
Cucumber, and GitHub Actions for continuous integration. I'm evaluating
[Cypress](https://www.cypress.io/) for end-to-end test automation.

## :microscope: Eddie

[github.com/mattreduce/eddie](https://github.com/mattreduce/eddie)

| Type     | Stack |
|:---------|:------|
| CLI tool | Bash  |

Eddie Vetter is a command-line tool for triaging macOS applications and
binaries, especially for vulnerability research.

I wrote Eddie so I wouldn't have to remember the various options for `codesign`
to triage macOS executables or deal with parsing its output every time. At the
moment it reports on:

* Whether the executable is signed
* The signing authority
* Whether or not Hardened Runtime is enabled
* The executable's entitlements (ex:
  `com.apple.security.cs.allow-dyld-environment-variables`)

I'm planning to rewrite it in Go, remove its dependency on `jq` for JSON
parsing, and expand its functionality.

## :ferris_wheel: bemusement-park

[github.com/mattreduce/bemusement-park](https://github.com/mattreduce/bemusement-park)

| Type            | Stack |
|:----------------|:------|
| Stage 0 payload | Swift |

Proof of concept for malicious auto-running
[Xcode](https://developer.apple.com/xcode/) Playgrounds.

## :package: mythic-crate

[github.com/mattreduce/mythic-crate](https://github.com/mattreduce/mythic-crate)

| Type                   | Stack        |
|:-----------------------|:--------------|
| Dev environment config | Bash/Vagrant |

I made mythic-crate to give myself a repeatable setup for local Mythic C2
development. Since then, I've also used it to run a local command and control
server for use with payloads running in my local macOS research lab.

## :notebook: cti-self-study

[github.com/mattreduce/cti-self-study](https://github.com/mattreduce/cti-self-study)

| Type           | Stack             |
|:---------------|:------------------|
| Notes template | Markdown/Obsidian |

I recently started working through Katie Nickels' Cyber Threat Intelligence
Self Study Plan. It's a collection of suggested reading, videos, activities and
things to ponder for folks who are new to CTI or interested in learning more
about it.

I decided to track my progress on this list and keep notes using the awesome
[Obsidian](https://obsidian.md/) personal knowledge base app. That way I can
check off items as I complete them, write my notes in Markdown, and even
annotate PDF and EPUB documents right in the same portable notebook.

Hoping others would find this setup useful when working through the CTI Self
Study Plan themselves, I made its initial structure and config available as a
GitHub template repo.
