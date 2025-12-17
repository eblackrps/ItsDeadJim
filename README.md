# ItsDeadJim

**Version:** 0.3.1

ItsDeadJim is a **read-only chaos simulation tool** for backup environments. It models what breaks when a component “dies” (proxy, repository, job, or credential) and shows the blast radius.

It does **not** connect to real systems.  
It does **not** make changes.  
It exists to expose hidden dependencies, false-green states, and delayed failures before reality does it for you.

---

## Quick Start (Manager-Friendly)

### Run the Application
1. Unzip the release folder.
2. Navigate to:
   ```
   dist\ItsDeadJim\
   ```
3. Double-click:
   ```
   ItsDeadJim.exe
   ```
4. Follow the guided wizard:
   - Select an environment
   - (Optional) Enter a seed for repeatable demos
   - Choose a scenario and failure mode
   - Review the impact summary

No command line knowledge required.

---

## What to Distribute

Always distribute the **entire folder**, not just the EXE:

```
dist\ItsDeadJim\
  ItsDeadJim.exe
  examples\
  scenario_packs\
  assets\
  _internal\
```

Zipping this folder is the recommended delivery method.

---

## Requirements (To Run)

### Running the Packaged EXE
No installs required.

- Windows 10 or Windows 11 (64-bit)
- Ability to unzip files

Python is **not required** to run the EXE.

---

## Wizard (Default Experience)

Running `ItsDeadJim.exe` with no arguments launches the guided wizard.

Wizard features:
- Menu-based environment selection
- Environment preview (counts of proxies, repos, jobs, creds)
- Optional seed for repeatable simulations
- Scenario category browsing (no typing scenario names)
- Failure mode selection
- Manager-friendly summary output
- Option to run another simulation or exit cleanly

This is the recommended mode for demos and leadership reviews.

---

## CLI Usage (Engineer Mode)

The EXE also supports command-line usage.

### Commands
- `ItsDeadJim.exe version`
- `ItsDeadJim.exe scenarios`
- `ItsDeadJim.exe wizard`
- `ItsDeadJim.exe run <env_file> [options]`

### Example
```powershell
.\ItsDeadJim.exe run .\examples\env_basic.json --scenario green_dashboard --mode misconfig --seed 7 --manager
```

---

## Environments

Environment files are JSON models of backup environments.

Bundled examples:
- `examples/env_basic.json`
- `examples/env_small_shop.json`
- `examples/env_mid_enterprise.json`
- `examples/env_bad_day.json`

Custom environments can be:
- Placed next to the EXE
- Selected via “Enter path manually” in the wizard

---

## Scenario Packs

List available scenarios:
```powershell
.\ItsDeadJim.exe scenarios
```

Scenarios are grouped by **category** (Attack, Change, Confidence, Human Error, Identity, Organizational, Storage, etc.).

Scenario packs are loaded from:
```
scenario_packs\*.json
```

### Authoring a Scenario Pack

Create a new file in `scenario_packs/`.

Example:
```json
{
  "name": "green_dashboard",
  "description": "Everything looks healthy until restore day.",
  "category": "Confidence",
  "priority": ["job", "repo", "proxy"]
}
```

Valid target types:
- `proxy`
- `repo`
- `job`
- `cred`

---

## Failure Modes

Each scenario can be run with different failure modes:

- **kill**  
  Immediate hard failure. Loud and obvious.

- **degrade**  
  Partial impact. Performance issues, queues, slow failures.

- **misconfig**  
  Silent breakage. Dashboards stay green. Reality arrives later.

False-green and delayed consequences are intentional.

---

## Seeds (Repeatable Runs)

Using a seed makes a simulation deterministic.

- Same environment + same scenario + same seed = same outcome

Useful for:
- Demos
- Before/after comparisons
- Leadership walkthroughs

---

## Output Modes

Wizard defaults to **manager-friendly output**:
- High-level impact
- Severity summary
- “What should we fix first” heuristics
- Short narrative explanation

CLI users can access full detail.

---

## Build From Source (Developers)

### Requirements (To Build)
- Windows 10/11
- Python 3.12+
- PowerShell
- Git (optional)

### Setup
```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -U pip
python -m pip install -r requirements.txt
python -m pip install -r requirements-build.txt
python -m pip install -e .
```

### Build the EXE
```powershell
.\build_exe.ps1
```

Output:
```
dist\ItsDeadJim\ItsDeadJim.exe
```

---

## Icon

The application icon is:
```
assets\itsdeadjim.ico
```

---

## Code Signing (Optional)

Self-signing can reduce Windows warnings **only if the certificate is trusted** on the target system (for example via internal IT distribution).

Self-signing does **not** grant public SmartScreen reputation.

---

## Safety and Scope

ItsDeadJim is:
- Read-only
- Offline
- Simulation-only

It does not connect to Veeam or any production system.  
It is a modeling and risk-conversation tool.

---

## License

Internal / project-defined. Add license text here if making public.
