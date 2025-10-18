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

> See `doc-update-guidelines.md` for complete update instructions including state management debugging, deployment checklists, and detailed update rules.
```

## Step 5: Validate Your Work

Before finalizing, verify:

1. **Paths exist**: Every file path in your main.md must be real
2. **Commands work**: Test each command you documented
3. **Structure is current**: Tree matches actual repository
4. **No speculation**: Document only what you can verify

## Step 6: Create Documentation Update Guidelines

Create a separate `doc-update-guidelines.md` file in the repository root. This file provides comprehensive instructions for maintaining and updating documentation.

Copy the following content exactly:

```markdown
# Documentation Update Guidelines

## Core Principles
- **Delete first, add second** - remove outdated content before adding new
- **Present tense only** - document what IS, not what WAS
- **Concise and actionable** - every sentence should help the reader DO something
- **Zero history** - no changelogs, migration notes, or "previously" references
- **YAGNI for docs** - delete unused files and sections immediately; they create confusion

## Before You Update
Ask yourself:
1. **Why this doc?** - What specific problem are you solving?
2. **What else breaks?** - Which other docs reference this one?
3. **Is it salvageable?** - Should you rewrite instead of patch?

## Update Rules
1. **Delete anything that references:**
   - Old implementations
   - Fixed bugs
   - Previous versions
   - Historical context
   - Unused files or features

2. **Keep only:**
   - Current functionality
   - Active configuration
   - Working examples
   - Essential concepts

3. **File management:**
   - Delete entire unused documentation files
   - Remove orphaned sections that no longer apply
   - Clean up broken internal links to deleted content

4. **Test every:**
   - Code example
   - File path
   - Command
   - Link

## State Management Debugging
When fixing component state synchronization:

1. **Map the data flow:**
   - Identify all state variables (parent and local)
   - Document which component updates which state
   - Track props passed between components
   - Note any one-way vs bi-directional flows

2. **Add proper callbacks:**
   - Components need `onVisibilityChange` and `onActiveTabChange` callbacks
   - Child components must notify parent of ALL state changes
   - Parent must wire callbacks to update its state flags
   - Never rely on child-only state for shared UI elements

3. **Fix mutual exclusion:**
   - When one sidebar opens, close the opposite sidebar
   - Update parent state when auto-hiding components
   - Check expansion state before allowing new opens
   - Clear all flags consistently on close

## Deployment Checklist
Before pushing changes that affect production builds:

1. **TypeScript exports:**
   - Verify all types used in component props are properly exported
   - Check that type imports use `type` keyword when importing types only
   - Ensure no missing type definitions in interface files

2. **Common build failures:**
   - Missing type exports from config/utility files
   - Unused imports causing tree-shaking issues
   - Incorrect file paths in import statements

3. **Quick validation:**
   - Run `npm run build` locally before pushing
   - Check TypeScript compilation with `npx tsc --noEmit`
   - Review any new prop types added to components

## Related Documentation
When updating one doc, check these for consistency:
- `main.md` - if feature names or structure changed
- Schema files - if data structures are referenced

## Red Flags for Full Rewrite
- More than 50% needs deletion
- Core purpose has changed
- Structure doesn't match current code
- Multiple broken examples

Remember: Good documentation is like good code - it's not done when there's nothing left to add, but when there's nothing left to remove.
```

This file should remain general and unchanged across all repositories. It provides detailed guidance that complements the condensed guidelines in main.md.

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
- [ ] Full doc-update-guidelines.md file exists in repository root

## Success Test

Another AI reading your main.md should be able to:
- Understand the project's purpose in 10 seconds
- Find any component within 30 seconds
- Make changes without asking questions

If they need to ask "Where is X?" or "What does Y do?", your documentation needs work.

Remember: The AI reading your main.md has limited context. Every word counts. Make each one necessary.