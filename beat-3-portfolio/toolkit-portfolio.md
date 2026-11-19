# Toolkit Portfolio

Path: `beat-3-portfolio/toolkit-portfolio.md`

**Student:** Fnu Yibole

## Featured Tools

I picked these tools because they show how I went from throwing loose prompts at an AI to actually scoping a real bug in ArduPlane, testing it in simulation, and keeping my diff clean enough for an upstream PR.

**Claude Code CLI**

**What it is, and the judgment hole I wrote:** t's a CLI coding agent running right in my terminal, and my judgment hole was enforcing AGENTS.md rules up front—read-only checks first, no guessing on flight-safety behavior, single-subsystem edits (ArduPlane/), and no unrequested cleanup or noisy comments.

**How it evolved, dated:** 
November 18, 2026: Started with a narrow ABORT_LANDING check in ArduPlane/fence.cpp, then had Claude Code trace in_fence_recovery() and Mode::enter() for manual mode overrides during a landing fence breach (#5544). When it suggested changing fence_stickmixing(), I told it to drop that and keep the patch strictly to in_fence_recovery().


**ArduPilot Autotest & SITL Harness**

**What it is, and the judgment hole I wrote:** It's ArduPilot's SITL simulator and Python test runner (autotest.py / sim_vehicle.py), and my judgment hole was picking the right flight edge cases—go-arounds and manual mode overrides past the 10-second manual_recovery window—and mapping them to specific test commands.

**How it evolved, dated:** 
November 18, 2026: Ran FenceMinAltAutoEnableAbort and the fence test suite after the ABORT_LANDING edit, then ran a SITL check switching to MANUAL / FBWA during a landing fence breach past 15 seconds to verify RTL didn't keep taking control back.


**Evidence:** Ran Tools/autotest/autotest.py build.Plane test.Plane.FenceMinAltAutoEnableAbort locally and had it pass, alongside a 15-second manual-override check in SITL (sim_vehicle.py -v ArduPlane).

**ArduPilot Branch Convention Checker**

**What it is, and the judgment hole I wrote:** It's ArduPilot's check_branch_conventions.py script that checks commit style, subsystem boundaries, and formatting, and my judgment hole was running it as a mandatory check on fix/your-issue-name so edits stayed strictly inside ArduPlane/.

**How it evolved, dated:** 
November 18, 2026: Kept both commits (14d196b and b2699a7) inside ArduPlane/ with Plane: prefixes and verified convention compliance before opening PR #35259.

**Evidence:** python3 Tools/scripts/check_branch_conventions.py passed cleanly on fix/your-issue-name before opening PR #35259.

## Inventory

Claude Code CLI: Terminal coding agent used to inspect fence.cpp, mode.cpp, and system.cpp and write minimal patches.

check_branch_conventions.py: Repo check script used to verify single-subsystem scope and commit formatting.

./waf: Build tool used to configure --board sitl and build ArduPlane.

autotest.py: Test runner used for automated Fence* test cases like FenceMinAltAutoEnableAbort.

sim_vehicle.py: SITL runner used to test manual mode switches during landing fence breaches.

issue-scout: Custom skill used to inspect issue context and reproduction details.

repro-check: Custom skill used to check local reproduction steps before editing code.

ship-gate: Custom skill used to double-check diffs, tests, and AI disclosure before submitting a PR.

## The Arc

**Beat 1**
Date: October 2026
Friction: Early AI-assisted edits were too broad and crossed subsystem boundaries that ArduPilot doesn't want mixed in one change.
Change: Started forcing AGENTS.md rules and single-subsystem limits into my Claude Code prompts before editing files.
Result: Diffs got way smaller and stopped tripping repo convention checks.

**Beat 2**
Date: November 2026
Friction: A proposed fix for geofence landing recovery included extra changes to fence_stickmixing() that weren't actually needed for manual modes.
Change: Cut fence_stickmixing() out of the patch and kept the change focused on landing_or_landed and in_fence_recovery() in ArduPlane/fence.cpp.
Result: Pushed two clean commits (14d196b and b2699a7) and opened PR #35259 on ArduPilot/ardupilot.

Copy the beat shape above for as many beats as your term had.

## Limitations and What's Next

The setup still relies on me manually triggering SITL scenarios and reading through the state transitions myself, and next I want to add a dedicated automated test case in Tools/autotest/arduplane.py for manual mode overrides during a landing fence breach.

**Tool limits.** 

issue-scout: gets stuck when an issue doesn't have clear reproduction steps or the discussion is all over the place.
Claude Code CLI: can still suggest extra edits outside the tightest spot unless I explicitly rein it in.
ArduPilot Autotest & SITL Harness: won't catch real hardware quirks like actual sensor noise or physical board timing bugs.
ArduPilot Branch Convention Checker: checks repo and commit rules, not whether the flight control logic is actually sound in the air.
