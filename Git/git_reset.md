# Git Reset Example

Git **reset** is a powerful command used to undo changes in the working directory, staging area, or commit history. Depending on the reset mode (`--soft`, `--mixed`, or `--hard`), it can modify different parts of the Git environment.

---

## Scenario
You have the following Git history:

```
    A---B---C (main)
```

You want to:
- Undo the last commit (`C`) without losing the changes.
- Move back to a previous commit and reset the working directory.

---

## Types of Git Reset

### 1. `--soft`
Moves the `HEAD` pointer but keeps changes in the staging area.

### 2. `--mixed`
Moves the `HEAD` pointer and removes changes from the staging area, keeping them in the working directory (default behavior).

### 3. `--hard`
Moves the `HEAD` pointer and removes changes from both the staging area and working directory.

---

## Steps to Perform Reset

### 1. Create the Repository and Initial Commits

```bash
git init reset-demo
cd reset-demo
echo "Initial content" > file.txt
git add file.txt
git commit -m "Initial commit"

echo "Change 1" >> file.txt
git commit -am "Commit 1"

echo "Change 2" >> file.txt
git commit -am "Commit 2"
```

The history looks like this:

```
    A---B---C (main)
```

### 2. Reset the Last Commit

#### a. `--soft`
Undo the last commit but keep the changes staged:

```bash
git reset --soft HEAD~1
```

Result:
- The `HEAD` moves back to `B`.
- Changes from `C` remain in the staging area.

#### b. `--mixed`
Undo the last commit and unstage the changes:

```bash
git reset --mixed HEAD~1
```

Result:
- The `HEAD` moves back to `B`.
- Changes from `C` are in the working directory but not staged.

#### c. `--hard`
Undo the last commit and discard changes completely:

```bash
git reset --hard HEAD~1
```

Result:
- The `HEAD` moves back to `B`.
- Changes from `C` are lost.

### 3. Reset to a Specific Commit
To move back to commit `A`:

```bash
git reset --hard <commit-hash-of-A>
```

Replace `<commit-hash-of-A>` with the hash of the desired commit.

---

## Warnings
- Use `--hard` cautiously, as it discards changes permanently.
- Ensure you don’t need any uncommitted work before resetting.

---

This demonstrates how to use Git reset to undo changes and move between commits.
