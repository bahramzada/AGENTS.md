# Agent Rules & Workflow Protocols

## 1. Version Control & GitHub

### Allowed Read-Only Git Commands

The agent may run only these Git inspection commands:

* `git status --short`
* `git diff --`
* `git diff --stat`
* `git rev-parse --show-toplevel`
* `git branch --show-current`
* `git log --oneline -n 5`

### Forbidden Git Mutation Commands

Never run commands that change repository state, including:

* `git init`
* `git add`
* `git commit`
* `git push`
* `git pull`
* `git fetch`
* `git merge`
* `git rebase`
* `git reset`
* `git checkout`
* `git switch`
* `git stash`
* `git tag`
* `git clean`

All version control mutation actions must be performed manually by the user.

### Commit Suggestions

* After making code or structural file changes, provide the exact commands needed to commit the changes.
* These commands must appear at the very end of the response.
* Do **not** execute them.

Example:

```bash
git add .
git commit -m "feat: add user authentication"
```


## 2. Project Initialization & Documentation

At the first write-task in a repository, ensure that the following files exist in the project root. Create them if they are missing.

Do not create or update these files for:

* Read-only questions
* Explanation-only tasks
* Quick diagnostics
* Formatting-only answers with no file changes

### Required Files

1. **`about_project.md`**

   * Project goals
   * Architecture overview
   * Tech stack
   * Update whenever:

     * Architecture changes
     * Dependencies change
     * Entrypoints or major modules change
     * Project setup commands change

2. **`progress.md`**

   * Activity log for completed write-tasks

3. **`troubleshooting.md`**

   * Long-term memory for:

     * Constraints
     * Errors
     * Failed attempts
     * Proven solutions

### Memory Update Rules

Update `about_project.md` only when architecture, dependencies, entrypoints, major modules, or project setup commands change.

Update `progress.md` after completed write-tasks only.

Update `troubleshooting.md` only when:

* An error was resolved
* More than 2 attempts were needed
* A reusable constraint or workaround was discovered

### Progress Log Format

Every completed write-task must be logged in `progress.md`:

```text
Date/Time (UTC) | Task Name | Detail | Modified Files | Status
```

### Troubleshooting Log Format

When resolving errors or technical obstacles, record them in `troubleshooting.md`:

```markdown
## [Short Error/Issue Title]

- **Context/Component:** Docker, n8n webhook, PostgreSQL, etc.
- **Error:** Brief description of the issue or error log.
- **Failed Attempts:** Steps that were tried but did not work.
- **Solution:** Exact code, configuration, or process that resolved the issue.
```


## 3. Communication Style & Tone

### CLI Optimized

* Be concise.
* Be direct.
* Stay task-focused.

### Response Modes

Default mode:

* Keep responses concise.
* Prefer 3-6 bullets.
* Avoid preamble and postamble.

Detailed mode is allowed when:

* The user asks for analysis or review.
* The task fails.
* Security, data loss, migration, architecture, or debugging is involved.
* Multiple files were changed.
* Tests fail or cannot be run.

After code or structural file changes, the final response must include:

* Changed files
* Verification run
* Known limitations
* Commit commands at the very end

### No Preamble / Postamble

Avoid phrases such as:

* "Here is the code"
* "I have updated the file"
* "Is there anything else?"

Respond directly to the request.

### Bash Command Explanations

For non-trivial terminal commands:

* Include a one-sentence explanation.
* Explain both:

  * What the command does
  * Why it is being run


## 4. Technical Standards (Python & Arch Linux)

### Environment

* Respect the Arch Linux environment.
* Check existing tools and packages before assuming availability.

### Python Standards

* Follow PEP 8.
* Use explicit type hints for:

  * Functions
  * Methods
  * Classes

### Code Style

* Do not add comments unless:

  * The logic is unusually complex, or
  * Comments are explicitly requested.

### Consistency

Before introducing new code:

* Review existing project files such as:

  * `package.json`
  * `requirements.txt`
  * Existing source files
* Match established:

  * Naming conventions
  * Libraries
  * Project patterns

### Memory & Lessons Learned

Before investigating a complex issue:

1. Check `troubleshooting.md`.
2. Reuse existing documented solutions where applicable.

If a problem requires more than **2 attempts** to solve:

* Document the final working solution immediately in `troubleshooting.md`.


## 5. Security & Safety

### Malicious Content

Refuse requests involving:

* Malware
* Exploits
* Harmful automation
* Any code intended to cause damage

### Secrets & Credentials

* Never expose API keys.
* Never log credentials.
* Never hardcode secrets.
* Use secure configuration and environment variables.


## 6. Proactivity & Verification

### Proactive but Respectful

If a task requires a major architectural or structural change:

* Request confirmation before proceeding.

### Verification

After modifying code, proactively run applicable validation tools, such as:

```bash
ruff check .
mypy .
pytest
```

Use the project's existing tooling whenever available to verify correctness and maintain consistency.
