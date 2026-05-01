# Linux-Trainer
A self-paced course covering both Debian/Ubuntu and Fedora/RHEL families. Read a lesson, run the lab in your VM, check your understanding, repeat.

# Linux Trainer

A self-paced web app to take you from beginner to mid-level Linux capable. Covers both Debian/Ubuntu and Fedora/RHEL families, oriented toward people building their own home server.

The app shows you lessons in your browser. You practice the actual commands in a Linux VM (VirtualBox is the recommended setup). It tracks your progress, gives you quick-check quizzes, and keeps a list of "labs" — small exercises you do in your VM and tick off when complete.

## Quick start

You need **Python 3.9 or newer**. On Windows, install it from python.org and tick "Add to PATH."

```bash
# 1. Clone or download this folder somewhere on your machine
cd linux-trainer

# 2. Create a virtual environment (isolates the dependencies)
python -m venv .venv

# 3. Activate it
#    macOS / Linux:
source .venv/bin/activate
#    Windows (PowerShell):
.venv\Scripts\Activate.ps1

# 4. Install requirements
pip install -r requirements.txt

# 5. Run the app
python app.py
```

Then open <http://localhost:5000> in your browser.

That's it. To stop, press Ctrl+C in the terminal where it's running. To start again, re-run `python app.py` (with the venv activated).

## What's in here

```
linux-trainer/
├── app.py                  # Flask backend (the whole server is one file)
├── requirements.txt        # Python dependencies
├── lessons/                # All curriculum content lives here as Markdown
│   ├── module-01-orientation/
│   │   ├── module.json
│   │   ├── 01-what-is-linux.md
│   │   ├── 02-vm-setup.md
│   │   ├── 03-the-shell.md
│   │   ├── 04-filesystem.md
│   │   └── 05-survival-kit.md
│   └── module-02-files/
│       └── ...
├── static/
│   ├── css/main.css        # Styling
│   └── js/app.js           # Quiz logic, completion toggles
├── templates/
│   ├── base.html
│   ├── home.html           # Curriculum overview
│   └── lesson.html         # Individual lesson view
└── data/
    └── progress.json       # Auto-created. Your completion state.
```

## Writing a new lesson

Lessons are plain Markdown with a small front-matter block on top.

Create a new file in any module's directory, for example `lessons/module-02-files/02-wildcards.md`:

```markdown
---
title: Wildcards and Globbing
order: 2
estimate: 10 min
---

# Wildcards and Globbing

Your lesson content goes here as regular Markdown. You can use:

- **Bold** and *italic*
- Headings (`##`, `###`)
- Code blocks (use triple backticks)
- Tables
- Blockquotes

::lab::
**Goal:** What the learner should accomplish.

Step-by-step exercise the learner does in their VM.

**Done when:** the success criterion.
::endlab::

::quiz::
Q: A question.
- An option
- Another option *
- A third option
Explanation: Why the starred answer is correct.

Q: Another question.
- Yes
- No *
Explanation: Reasoning.
::endquiz::
```

Rules:

- The `---` front matter block is required. `title`, `order`, and `estimate` are the keys it understands.
- `order` controls the lesson's position within its module.
- The `::lab::` and `::quiz::` blocks are optional. Use them when they add value.
- A `*` after a quiz option marks it as the correct answer.

Refresh the browser — there's no build step or restart needed.

## Adding a new module

Create a folder under `lessons/` whose name starts with `module-` (the rest is up to you), and put a `module.json` inside:

```json
{
  "title": "Networking and SSH",
  "description": "Talking to other machines, securely.",
  "order": 6
}
```

Then drop lesson `.md` files inside it.

## Suggested course progression

The full curriculum the app is designed to cover, in order:

1. **Orientation** — what Linux is, the shell, filesystem, survival kit ✓ *(included)*
2. **Files and navigation in depth** — wildcards, redirection, pipes, find/grep
3. **Reading and editing** — `less`, `nano`, basic `vim`, sed/awk awareness
4. **Permissions and users** — `chmod`, `chown`, `sudo`, `/etc/passwd`
5. **Processes and services** — `ps`, `top`, `kill`, `systemctl`
6. **Networking basics** — `ip`, `ss`, `ping`, `curl`, SSH
7. **Package management** — `apt` and `dnf` covered side-by-side
8. **Shell scripting** — variables, loops, conditionals, cron
9. **Storage and mounts** — disks, partitions, `fstab`, mounting NAS shares
10. **Server fundamentals** — SSH hardening, firewalls, log files, backups

By the end of Module 10 you'll have everything needed to set up your home server with confidence.

## Roadmap (Phase 2)

This is "Phase 1" — lessons in the browser, practice in your own VM. A future Phase 2 could add:

- Embedded terminal in the browser via xterm.js + WebSockets
- Per-lesson Docker containers for sandboxed practice
- Auto-validation of lab tasks by inspecting the container state
- A daily review system that resurfaces commands you haven't seen in a while

For now, the simpler design will get you learning Linux *today* rather than spending weeks building infrastructure first.

## Resetting progress

Click "Reset progress" at the bottom of the home page, or just delete `data/progress.json` and refresh.
