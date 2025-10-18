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
- `lifeos-visual-journey-prd.md` - for LifeOS visual journey component updates
- Schema files - if data structures are referenced

## Red Flags for Full Rewrite
- More than 50% needs deletion
- Core purpose has changed
- Structure doesn't match current code
- Multiple broken examples

Remember: Good documentation is like good code - it's not done when there's nothing left to add, but when there's nothing left to remove.
