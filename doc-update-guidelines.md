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

## Related Documentation
When updating one doc, check these for consistency:
- `main.md` - if feature names or structure changed
- Schema files - if data structures are referenced

## Red Flags for Full Rewrite
- More than 50% needs deletion
- Core purpose has changed
- Structure doesn't match current code
- Multiple broken examples

---

**Extend this file** with project-specific sections as needed (file placement conventions, build/deploy checklists, etc.). Keep the core principles above unchanged.
