# Instructions to Create main.md for Repository Navigation

## Purpose
You are creating a main.md file that will help another AI agent understand and navigate this repository. That AI needs to accomplish tasks using only your main.md as a guide.

## Core Principle: Delete More Than You Add
AI agents tend to over-document. Fight this tendency. Every unnecessary sentence makes the repository harder to understand. When unsure, remove content rather than add it.

## Step 1: Assess Repository Size

First, understand what you're documenting:
```bash
# Count files (excluding hidden and dependencies)
find . -type f -not -path '*/\.*' -not -path '*/dependencies/*' | wc -l
```

Based on file count:
- **Over 1000 files**: Document only high-level architecture
- **100-1000 files**: Include architecture plus key components
- **Under 100 files**: Can include specific important functions

## Step 2: Create Repository Map

Generate a tree structure showing only essential directories:
```bash
# Exclude common dependency/build directories
tree -L 2 -d
```

Annotate each directory with its purpose (not a description):
```
ProjectName/
├── src/                # Business logic
├── api/                # External interfaces
├── config/             # App configuration
└── docs/               # Detailed documentation
```

Skip directories that are:
- Dependencies or packages
- Build outputs
- Cache directories
- Generated code

**For projects with nested data structures** (experiment outputs, generated artifacts), show the nesting pattern with template variables. This is often the most useful part of the tree:
```
experiments/{name}/
├── config.json
├── extraction/{trait}/
│   ├── responses/
│   └── vectors/{method}/
└── inference/{prompt_set}/
```

## Step 3: Find Starting Points

Identify where code execution begins:
- Main entry files (main.*, index.*, app.*)
- Build configuration files
- Package dependency files
- Application configuration

Follow imports one level deep to understand connections. Stop there.

**For multi-workflow projects**, identify entry points per workflow, not just "run the app":
- Pipeline scripts (data prep, training, evaluation)
- Analysis/utility scripts users run directly
- Server/service entry points

## Step 4: Create main.md

Use this template, adapting sections based on project complexity:

```markdown
# [Project Name]

[One sentence describing what this does]

## Repository Structure

[Tree with purpose annotations - only directories that matter]
[Include nested data patterns with template variables if applicable]

## Quick Start

1. Install dependencies
   ```bash
   [actual command that works]
   ```

2. Run application
   ```bash
   [actual command that works]
   ```

## Key Entry Points

[For single-workflow projects, Quick Start above is sufficient — skip this section.
For multi-workflow projects, show the primary commands with real flags:]

**Workflow A:**
```bash
python scripts/do_thing.py --experiment {name} --flag value
```

**Workflow B:**
```bash
python scripts/other_thing.py --input {path}
```

## Core Components

### [Component Name]
**Purpose**: [Problem it solves]
**Entry point**: `path/to/file`
**Key files**:
- `file1` - [5 words max]
- `file2` - [5 words max]

[Include only 3-5 essential components]

## Architecture

[2-3 sentences explaining how components connect and data flows.
For projects with clear module dependencies, a simple diagram helps:]

```
core/         <- Primitives
    ^
    |-- Used by: pipeline/
    |-- Used by: analysis/

utils/        <- Shared utilities
    ^
    |-- Used by: all modules
```

## Navigation Guide

To work on:
- API endpoints -> `api/routes/`
- Business logic -> `src/services/`
- Database layer -> `src/models/`
- Configuration -> `config/`

[Adjust paths to match actual repository]

## Current Status

**Working**:
- [Features that definitely work]

**Not Working**:
- [Known broken features]

## Additional Documentation

[For projects with 5+ doc files, include a categorized index here.
Keep descriptions to one phrase each. Don't let this section exceed
the actual navigation content above it.]

See `docs/` folder for:
- `api.md` - Endpoint specifications
- `database.md` - Schema details
[Only list files that actually exist]

---

## Documentation Update Guidelines

**Core Principles:**
- **Delete first, add second** - Always remove outdated content before adding new
- **Present tense only** - Document what IS, not what WAS
- **Zero history** - No changelogs, migration notes, or "previously" references
- **YAGNI for docs** - Delete unused files and sections immediately; they create confusion

**When to Delete:**
- Old implementations, fixed bugs, previous versions
- Historical context and migration notes
- Unused files or features
- Anything you can't verify still works

**File Management:**
- Delete entire unused documentation files
- Remove orphaned sections that no longer apply
- Clean up broken internal links to deleted content

> See `doc-update-guidelines.md` for complete update instructions.
```

### Template Scaling Notes

The template above should be **adapted**, not copied verbatim:

- **Small projects (<20 files)**: Skip "Key Entry Points" and "Additional Documentation". Quick Start + Core Components is enough.
- **Medium projects (20-100 files)**: Use the full template as-is.
- **Large projects (100+ files)**: The Documentation Index may need subcategories. Be disciplined — if the index is longer than the navigation content, you've over-documented.

**Common anti-pattern**: main.md that's half navigation, half reference material. Methods tables, API signatures, configuration schemas — these belong in separate docs, linked from main.md. Main.md answers "where is everything?" not "how does everything work?"

## Step 5: Validate Your Work

Before finalizing, verify:

1. **Paths exist**: Every file path in your main.md must be real
2. **Commands work**: Test each command you documented
3. **Structure is current**: Tree matches actual repository
4. **No speculation**: Document only what you can verify

## Step 6: Create Documentation Update Guidelines

Create a separate `doc-update-guidelines.md` file in the repository root (or `docs/` if the project uses that convention). See the companion `doc-update-guidelines.md` in this repo for the template content.

Projects should extend the base guidelines with project-specific sections (file placement conventions, build/deploy checklists for their stack, etc.).

## Step 7: CLAUDE.md Integration (Claude Only)

**Skip this step if you are not Claude / not running in Claude Code.**

If the repository will be used with Claude Code, create a `CLAUDE.md` in the repository root that references main.md:

```markdown
@docs/main.md

## Core Principles
[Project-specific behavioral instructions for Claude — code style,
naming conventions, what to avoid, etc.]
```

This separates concerns:
- **main.md** = navigation (any AI agent, any human)
- **CLAUDE.md** = behavioral instructions (Claude-specific: code style, conventions, constraints)

Don't duplicate main.md content in CLAUDE.md. The `@docs/main.md` directive imports it automatically.

## Step 8: Report What You Created

After creating the documentation, output to chat (not in any file):

1. What files were created and where
2. How to use them:
   - For Claude Code users: "CLAUDE.md auto-loads when Claude Code opens this repo. No action needed."
   - For other AI tools: "Copy the contents of docs/main.md into your system prompt or context window when working on this repo."
   - For humans: "Start at docs/main.md for navigation. See doc-update-guidelines.md before editing docs."
3. Any sections you left sparse due to insufficient information

## What to Include vs. Skip

### Must Include
- Project name and purpose (one sentence)
- Repository structure (annotated tree)
- How to run the project
- Where to find major components
- What's currently broken

### Skip Unless Critical
- Test directories (unless they contain important examples)
- Build outputs
- Historical information
- Future plans
- Obvious structure explanations

## Handling Existing Documentation

If you find scattered README files:
1. Extract only current, working information
2. Consolidate into main.md or docs/ folder
3. Delete the originals

If you find outdated documentation:
1. Delete it immediately
2. Don't preserve "for history"

## Creating Additional Documentation

Only create separate documentation files when a component needs more than 50 lines of explanation. Place them in `docs/` folder with simple names:
- `api.md` not `API-Documentation-v2-Final.md`
- `auth.md` not `Authentication-Module-Technical-Specification.md`

## Final Checklist

Your documentation is complete when:
- [ ] Another AI can understand the project's purpose immediately
- [ ] All file paths in main.md are real and tested
- [ ] All commands actually work
- [ ] main.md is under 500 lines (split to docs/ if longer)
- [ ] No history, no future plans, only current state
- [ ] Every sentence helps someone do something
- [ ] Condensed update guidelines are at the bottom of main.md
- [ ] doc-update-guidelines.md exists in repository root or docs/
- [ ] CLAUDE.md created if applicable (Claude only), referencing main.md via @
- [ ] Usage instructions output to chat

## Success Test

Another AI reading your main.md should be able to:
- Understand the project's purpose in 10 seconds
- Find any component within 30 seconds
- Make changes without asking questions

If they need to ask "Where is X?" or "What does Y do?", your documentation needs work.

Remember: The AI reading your main.md has limited context. Every word counts. Make each one necessary.
