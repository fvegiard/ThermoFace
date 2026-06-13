# NOTES.md — ThermoFace commit & cleanup log

**Date:** 2026-06-13

## What was done

### 1. Reviewed git status and project
- Branch: `main`
- Remote: `origin` https://github.com/JackieHanLab/ThermoFace.git
- Status: up to date with origin/main
- Untracked before cleanup: `_ANALYSIS.md` (generated 2026-06-10 during home-folder cleanup pass)
- No `.gitignore` present
- Problematic: Python `__pycache__/` and `.pyc` bytecode files were **tracked** in the repo (12 files under `codes/__pycache__` and `codes/FAS/__pycache__`)
- Large assets already in history: `mergefiles/` (~192 MB of dlib_landmark_predictor_*.dat files), `data/test_data/*.IS2`, `readis2_ti401pro.dat` (~19k), models/, etc.
- Structure: Python/MATLAB code for Fluke Ti401pro .IS2 thermal image preprocessing, dlib/MediaPipe ThermoFace detection, SVM, matrix generation. See README.md for usage.
- No `NOTES.md` previously; `_ANALYSIS.md` present as reference note.
- Git init not needed (repo already initialized with history).

### 2. Cleanup actions
- Created `.gitignore` (standard Python ignores for `__pycache__/`, `*.py[cod]`, venvs, IDEs, OS files, plus project notes)
- Staged `.gitignore`
- Removed committed pycache from git index only (to stop tracking bytecode while preserving history):
  ```
  git rm -r --cached codes/__pycache__ codes/FAS/__pycache__
  ```
- Deleted local `__pycache__` directories from filesystem (`rm -rf`) to clean working tree (now ignored by .gitignore)
- Prepared `_ANALYSIS.md`, `.gitignore`, and new `NOTES.md` for commit
- Staged deletions + new files with `git add -A`

### 3. Committed
- Commit message: "chore: add .gitignore (Python), remove tracked pycache from index, commit _ANALYSIS.md and NOTES.md"
- All changes committed on `main`

### 4. Pushed
- `git push origin main` (to sync cleanup to remote)

## Current state (post-commit)
- Branch: `main` (clean, no uncommitted changes)
- Remote: pushed and up-to-date
- Working tree clean: no untracked files, pycache removed, .gitignore active
- `.git` remains; no re-init performed

## Files committed/changed
| File | Status |
|------|--------|
| `.gitignore` | New |
| `_ANALYSIS.md` | New (committed) |
| `codes/__pycache__/*` (6 .pyc files) | Deleted from index (and fs) |
| `codes/FAS/__pycache__/*` (2 .pyc files) | Deleted from index (and fs) |
| `NOTES.md` | New |

## Notes / Recommendations
- Future Python runs will not pollute repo with bytecode thanks to .gitignore.
- Large binary model/data files remain in git history (as in original repo); consider LFS or separate data repo if size becomes issue for clones.
- Project appears to be a reference/clone of the ThermoFace paper code (Cell Metabolism 2024); keep as-is for research use.
- No other obvious junk (no node_modules, no extra backups, no .env, etc.).
- To run: see README.md (requires Python 3.6 env, specific deps like dlib, mediapipe, MATLAB for full preprocess).

_Generated during ThermoFace review & clean pass (delegated task)._