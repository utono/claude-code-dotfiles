# Git Add, Commit, Push (gac)

Perform git add, commit, and push for the following repositories:

1. ~/utono/xc
2. ~/utono/nvim-glosses
3. ~/utono/nvim-glosses-qa

## Instructions

For each repository:

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
