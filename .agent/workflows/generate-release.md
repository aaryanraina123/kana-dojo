---
description: how to generate a new release with patch notes and version bump
---

Follow these steps to generate a new release for the application:

## 1. Gather Information

- View the last 50 commits: `git log -50 --pretty=format:"%s"`
- Read the current version and previous patch notes from `features/PatchNotes/patchNotesData.json`.
- Read the current version from `package.json`.

## 2. Generate Patch Notes

- **User-Friendly Language:** Translate technical commit messages into clear, benefit-oriented language for end-users.
  - ❌ Avoid: "refactor: update zustand store selectors", "feat: add abort controller to api calls"
  - ✅ Use: "Improved app performance and stability", "Smoother loading when switching between pages"
- **Filter Irrelevant Changes:** Ignore dev-only changes (CI/CD, linting, internal refactorings that don't affect UX).
- **Avoid Overlap:** Cross-reference the generated notes with the previous release in `patchNotesData.json`. If a feature or fix was already mentioned, do not include it again.
- **Group Changes:** If multiple commits relate to the same feature (e.g., several "fix sidebar" commits), combine them into a single clear bullet point.

## 3. Version Bump

- Increment the patch version number in `package.json` (e.g., `0.1.12` -> `0.1.13`).
- If the changes are significant, consider a minor version bump instead, but default to patch.

## 4. Apply Changes

- **Update `package.json`**: Update the `"version"` field.
- **Update `features/PatchNotes/patchNotesData.json`**:
  - Add a new entry at the top of the array.
  - Include the new `version`, current `date` (formatted as "Month Day, Year"), and the list of `changes`.
- **Update `CLAUDE.md`**: Update the version number at the bottom of the file.

## 5. Verification

- Run `npm run check` to ensure no regressions were introduced by updating JSON files or metadata.
- Provide a summary of the new patch notes and the new version number to the user.

## Git Commit

- After completing the release, provide a git commit command:
  ```bash
  git add -A && git commit -m "chore(release): bump version to vX.X.X" -m "Generated patch notes for version vX.X.X"
  ```
