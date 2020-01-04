# gitlens-cheat-sheet

# Configuration

Do you find code lens intrusive or the current line blame annotation distracting — no problem, quickly turn them off or change how they behave via the interactive GitLens Settings editor. For advanced customizations, refer to the GitLens docs and edit your user settings.

GitLens has a built-in interactive settings editor which provides an easy-to-use interface to configure many of GitLens' powerful features. It can be accessed via the `GitLens: Open Settings` (`gitlens.showSettingsPage`) command from the Command Palette.

#  Side Bar views

many rich Side Bar views
- a **Repositories view** to visualize, navigate, and explore Git repositories
- a **File History view** to visualize, navigate, and explore the revision history of the current file
- a Line History view to visualize, navigate, and explore the revision history of the selected - lines of current file
- a Search Commits view to search and explore commit histories by message, author, files, id, etc
- a **Compare view** to visualize comparisons between **branches**, **tags**, **commits**, and more


# File History view

...


# Compare view

- An inline toolbar provides quick access to the Pin Comparison (when applicable), Unpin Comparison (when applicable), Switch to Two-dot Comparison (when applicable), Switch to Three-dot Comparison (when applicable), Swap Comparison, Refresh, and Dismiss (when applicable) commands


- Files Changed — lists all of the files changed between the compared revisions
Expands to a file-based view of all changed files in the working tree (optionally) and/or all files in all commits ahead of the upstream

Results can be provided by the following commands
- `Compare with Remote command` (gitlens.views.compareWithRemote)
- `Compare with HEAD command` (gitlens.views.compareWithHead)
- `Compare with Working Tree command` (gitlens.views.compareWithWorking)
- `Compare with Selected command` (gitlens.views.compareWithSelected)
- `Compare Ancestry with Working Tree command` (gitlens.views.compareAncestryWithWorking)
