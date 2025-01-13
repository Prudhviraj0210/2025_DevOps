# Git Rebase Example

Git **rebase** is a process of moving or combining a sequence of commits to a new base commit. It is used to integrate changes from one branch into another, providing a cleaner commit history compared to `merge`.

---

## Scenario
You have the following Git history:

```
    A---B---C (feature)
   /
D---E---F (main)
```

You want to rebase the `feature` branch onto the `main` branch so that it appears as if it was built on top of `main`.

---

## Steps to Perform Rebase

### 1. Create the Repository and Initial Commit

```bash
git init rebase-demo
cd rebase-demo
echo "Initial content" > file.txt
git add file.txt
git commit -m "Initial commit"
```

### 2. Create `main` Branch Changes

```bash
echo "Main branch change 1" >> file.txt
git commit -am "Main branch commit 1"
echo "Main branch change 2" >> file.txt
git commit -am "Main branch commit 2"
```

### 3. Create `feature` Branch Changes

```bash
git checkout -b feature
echo "Feature branch change 1" >> file.txt
git commit -am "Feature branch commit 1"
echo "Feature branch change 2" >> file.txt
git commit -am "Feature branch commit 2"
```

At this point, the history looks like this:

```
    A---B (feature)
   /
D---E---F (main)
```

### 4. Rebase `feature` onto `main`

Switch to the `feature` branch and rebase:

```bash
git checkout feature
git rebase main
```

Git will replay the commits from the `feature` branch (A, B) on top of the latest commit in the `main` branch (F). The history now looks like this:

```
D---E---F---A'---B' (feature)
```

---

## Resolving Conflicts During Rebase
If there are conflicts during rebase, Git will pause and allow you to resolve them. For example:

```bash
Auto-merging file.txt
CONFLICT (content): Merge conflict in file.txt
```

1. Resolve the conflict in the file.
2. Mark the conflict as resolved:

   ```bash
   git add file.txt
   ```

3. Continue the rebase:

   ```bash
   git rebase --continue
   ```

---

## Benefits of Rebase
- Creates a linear commit history.
- Simplifies the history for features developed on a branch.
- Useful for preparing a feature branch for merging.

---

This demonstrates how to use Git rebase to integrate changes and clean up commit history.
