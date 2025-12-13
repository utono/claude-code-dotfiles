# mr-commit

Perform git add, commit, and push for repositories.

## Arguments

$ARGUMENTS - Optional: One or more repository paths (space-separated), or `.`

## Behavior

### If ARGUMENTS is `.` (dot):
Process only the current working directory. Skip all grouped repository logic
and mr status scanning. Just git add, commit, push on this project alone.

### If other ARGUMENTS provided:
Process only the specified repositories.

### Grouped Neovim Repositories
If ANY of these paths are specified (symlink or target), process ALL of them:

| Symlink | Target |
|---------|--------|
| `~/.config/nvim` | `~/utono/nvim-code` |
| `~/.config/nvim-glosses` | `~/utono/nvim-glosses` |
| `~/.config/nvim-glosses-qa` | `~/utono/nvim-glosses-qa` |
| `~/.config/nvim-shared` | `~/utono/nvim-shared` |

Example: `/gac ~/.config/nvim` processes all four repos above.

### Grouped XC Repositories
If ANY of these paths are specified, process ALL of them:

| Repository |
|------------|
| `~/utono/xc` |
| `~/utono/nvim-glosses` |
| `~/utono/nvim-glosses-qa` |

Example: `/gac ~/utono/xc` processes all three repos above.

### If no ARGUMENTS provided:
1. **Sync mr config first**: Run `~/.local/bin/bin-mlj/mr/mr-sync-config.sh` to ensure newly created repos are registered and deleted repos are cleaned up
2. Run `mr status` from `/home/mlj` to find repositories with uncommitted changes
3. Parse the output to identify which repos have changes
4. Process each repo with changes
5. Then check all repos in `~/utono/` and process any with uncommitted changes

## Instructions

For each repository with changes:

1. Check `git status` and `git diff` to see what files have changed
2. **Keybind Documentation Check**: If any keybinds were added or changed:
   - Update `~/utono/xc/docs/keybinds.md` for xc repo changes
   - Update `~/utono/nvim-glosses/docs/keybinds.md` for nvim-glosses changes
   - Run `git add docs/keybinds.md` for any modified keybinds.md files
3. If there are changes:
   - Run `git add .` to stage all changes
   - Analyze the changes and generate an appropriate commit message
   - Run `git commit -m "<generated message>"`
   - Run `git push`
4. If no changes, skip that repository and move to the next

## Commit Message Guidelines

- Summarize the nature of changes (new feature, bug fix, refactor, etc.)
- Keep messages concise (1-2 sentences)
- Focus on the "why" rather than the "what"
- Each repo gets its own tailored commit message based on its changes

## mr status Output Parsing

The `mr status` command outputs sections like:
```
mr status: /path/to/repo
<git status output>
```

Look for repos that show modified/untracked files in their status output.

## Summary Output

At the end, display a summary table showing:
- Repository path
- Changes committed
- Push status

**If `mr status` reported any errors** (e.g., missing directories, failed chdir),
include them in the summary:
```
**mr status errors:**
- /path/to/missing/repo: No such file or directory
```

Note: The pre-sync step should have already cleaned up stale entries, but report any remaining errors.
