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

## Step 3: Find Starting Points

Identify where code execution begins:
- Main entry files (main.*, index.*, app.*)
- Build configuration files
- Package dependency files
- Application configuration

Follow imports one level deep to understand connections. Stop there.

## Step 4: Create main.md

Use this exact template:

```markdown
# [Project Name]

[One sentence describing what this does]

## Repository Structure

[Tree with purpose annotations - only directories that matter]

## Quick Start

1. Install dependencies
   ```bash
   [actual command that works]
   ```

2. Run application
   ```bash
   [actual command that works]
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

[2-3 sentences explaining how components connect and data flows]

## Navigation Guide

To work on:
- API endpoints → `api/routes/`
- Business logic → `src/services/`
- Database layer → `src/models/`
- Configuration → `config/`

[Adjust paths to match actual repository]

## Current Status

**Working**:
- [Features that definitely work]

**Not Working**:
- [Known broken features]

## Additional Documentation

See `docs/` folder for:
- `api.md` - Endpoint specifications
- `database.md` - Schema details
[Only list files that actually exist]

---

## Documentation Update Guidelines

### Core Principle
Delete first, add second. Always remove outdated content before adding new documentation.

### Update Rules
- **Present tense only** - Document what exists now
- **No history** - Delete references to previous versions
- **No promises** - Remove all "TODO" and "coming soon"
- **Test everything** - Verify every command and path
- **Keep it minimal** - If it's obvious from the code, don't document it

### When to Delete
- References to removed features
- Anything containing "previously", "will be", or "planned"
- Documentation you can't verify
- Explanations of obvious things

### When to Update
- Feature added → Update immediately
- Feature removed → Delete docs first
- Found outdated section → Delete or fix now

Remember: Documentation is complete when there's nothing left to remove.
```

## Step 5: Validate Your Work

Before finalizing, verify:

1. **Paths exist**: Every file path in your main.md must be real
2. **Commands work**: Test each command you documented
3. **Structure is current**: Tree matches actual repository
4. **No speculation**: Document only what you can verify

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

Your main.md is complete when:
- [ ] Another AI can understand the project's purpose immediately
- [ ] All file paths are real and tested
- [ ] All commands actually work
- [ ] It's under 500 lines (split to docs/ if longer)
- [ ] No history, no future plans, only current state
- [ ] Every sentence helps someone do something
- [ ] Documentation update guidelines are at the bottom

## Success Test

Another AI reading your main.md should be able to:
- Understand the project's purpose in 10 seconds
- Find any component within 30 seconds
- Make changes without asking questions

If they need to ask "Where is X?" or "What does Y do?", your documentation needs work.

Remember: The AI reading your main.md has limited context. Every word counts. Make each one necessary.