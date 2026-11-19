# Toolkit Portfolio

Path: `beat-3-portfolio/toolkit-portfolio.md`

**Student:** Fnu Yibole

## Featured Tools

I picked these tools because they show how I went from throwing loose prompts at an AI to actually scoping a real bug in ArduPlane, testing it in simulation, and keeping my diff clean enough for an upstream PR.

**Git Workflow**

**What it is, and the judgment hole I wrote:** My command-line git and editor workflow in the repository, and my judgment hole was enforcing AGENTS.md rules up front—tracing state before editing, keeping changes inside a single subsystem (ArduPlane/), and dropping unrequested edits like fence_stickmixing() so the diff stayed strictly focused on in_fence_recovery()

**How it evolved, dated:** 
November 10, 2026: Started with an ABORT_LANDING check in ArduPlane/fence.cpp, then traced in_fence_recovery() and Mode::enter() for manual mode overrides during a landing fence breach (#5544), cutting out a suggested fence_stickmixing() change so the patch stayed strictly in in_fence_recovery().

**Evidence:** Tools/autotest/autotest.py build.Plane test.Plane.FenceMinAltAutoEnableAbort passed locally alongside SITL checks via sim_vehicle.py -v ArduPlane.

**ArduPilot Autotest & SITL Harness**

**What it is, and the judgment hole I wrote:** It's ArduPilot's SITL simulator and Python test runner (autotest.py / sim_vehicle.py), and my judgment hole was picking the right flight edge cases—go-arounds and manual mode overrides past the 10-second manual_recovery window—and mapping them to specific test commands.

**How it evolved, dated:** 
November 10, 2026: Ran FenceMinAltAutoEnableAbort and the fence test suite after the ABORT_LANDING edit, then ran a SITL check switching to MANUAL / FBWA during a landing fence breach past 15 seconds to verify RTL didn't keep taking control back.


**Evidence:** Ran Tools/autotest/autotest.py build.Plane test.Plane.FenceMinAltAutoEnableAbort locally and had it pass, alongside a 15-second manual-override check in SITL (sim_vehicle.py -v ArduPlane).

**ArduPilot Branch Convention Checker**

**What it is, and the judgment hole I wrote:** It's ArduPilot's check_branch_conventions.py script that checks commit style, subsystem boundaries, and formatting, and my judgment hole was running it as a mandatory check on fix/your-issue-name so edits stayed strictly inside ArduPlane/.

**How it evolved, dated:** 
November 10, 2026: Kept both commits (14d196b and b2699a7) inside ArduPlane/ with Plane: prefixes and verified convention compliance before opening PR #35259.

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
Date: 2026 November
Friction: The initial ABORT_LANDING change only covered go-around suppression and didn't fix pilots getting forced back into RTL after switching to a manual mode past the 10-second recovery window.
Change: Traced in_fence_recovery() and Mode::enter() and added pilot_override handling for RC_COMMAND and GCS_COMMAND when previous_mode_reason == FENCE_BREACHED in ArduPlane/fence.cpp.
Result: Committed b2699a7 on top of 14d196b and opened PR #35259 on ArduPilot/ardupilot.

**Beat 2**
Date: 2026 November
Friction: An early draft of the override fix also included changes to fence_stickmixing(), which wasn't needed for manual modes and added extra diff surface.
Change: Dropped the fence_stickmixing() change and kept the diff strictly focused on in_fence_recovery() in ArduPlane/fence.cpp.
Result: Kept the PR to a single file (ArduPlane/fence.cpp, +9/-2 lines) passing local convention and fence test checks.

Copy the beat shape above for as many beats as your term had.

## Limitations and What's Next

The workflow still depends on me running SITL scenarios and checking the state transitions manually, so next I'd like to add an automated test in Tools/autotest/arduplane.py covering manual mode overrides during a landing fence breach.

**Tool limits.** 

issue-scout: gets stuck when an issue lacks clear reproduction steps or the discussion is all over the place.
Terminal & Git Workflow (git / AGENTS.md): still requires manual discipline to spot and cut extra edits like fence_stickmixing() before committing.
ArduPilot Autotest & SITL Harness: cannot catch hardware-specific timing issues or real sensor noise on physical boards.
ArduPilot Branch Convention Checker: checks repo rules and formatting, not whether the flight logic is sound in real flight.
