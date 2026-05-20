# dirq-aap-playbooks

A handful of small Linux playbooks for Ansible Automation Platform
projects backed by a [DirQ](https://github.com/atgreen/dirq) fleet.

Pair this repo with [`dirq-aap-inventory`](https://github.com/atgreen/dirq-aap-inventory)
as your inventory source.

| Playbook | What it does |
|---|---|
| `ping.yml` | Reach every Linux host through the DirQ mesh. Smoke test. |
| `uptime.yml` | Run `uptime` on every host and print the output. |
| `facts.yml` | Gather facts and print a one-line summary. Exercises the DirQ fact cache plugin if it's wired up. |
| `run_command.yml` | Run an arbitrary command — pass `cmd` as an extra var at launch. AAP doesn't let the DirQ credential type appear on the **Run Command** page (it's not a Machine credential), so this playbook is a generic ad-hoc replacement. |
| `update_packages.yml` | `dnf`/`apt` upgrade across the fleet. Tests `become: true` through the DirQ exec path. |

All target the auto-generated `os_linux` group from the DirQ inventory plugin.

## AAP setup

1. Create an AAP **Project** pointing at this repo.
2. In a **Job Template**, set:
   - **Project**: the one from step 1
   - **Playbook**: pick one of the YAML files
   - **Inventory**: your DirQ-backed inventory
   - **Execution Environment**: `ghcr.io/atgreen/dirq-ee:latest`
   - **Credentials**: your `DirQ Credential` (no Machine credential needed)
3. Launch.
