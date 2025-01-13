# Git Cherry-Pick Example

Git **cherry-pick** is a command that allows you to apply a specific commit from one branch to another. It’s useful when you want to port particular changes without merging the entire branch.

---

## Scenario
You have the following Git history:

```
    A---B---C---D (main)
         \
          E---F---G (feature)
```

You want to apply the commit `F` from the `feature` branch to the `main` branch without merging the entire `feature` branch.

---

## Steps to Perform Cherry-Pick

### 1. Create the Repository and Initial Commit

```bash
git init cherrypick-demo
cd cherrypick-demo
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
echo "Feature branch change 3" >> file.txt
git commit -am "Feature branch commit 3"
```

At this point, the history looks like this:

```
    A---B---C (main)
         \
          E---F---G (feature)
```

### 4. Cherry-Pick Commit `F` onto `main`

Switch to the `main` branch and cherry-pick:

```bash
git checkout main
git cherry-pick <commit-hash-of-F>
```

Replace `<commit-hash-of-F>` with the hash of the commit `F`. This applies the changes introduced by `F` to the `main` branch.

The history now looks like this:

```
    A---B---C---F' (main)
         \
          E---F---G (feature)
```

---

## Resolving Conflicts During Cherry-Pick
If there are conflicts, Git will pause and allow you to resolve them. For example:

```bash
Auto-merging file.txt
CONFLICT (content): Merge conflict in file.txt
```

1. Resolve the conflict in the file.
2. Mark the conflict as resolved:

   ```bash
   git add file.txt
   ```

3. Continue the cherry-pick:

   ```bash
   git cherry-pick --continue
   ```

---

## Benefits of Cherry-Pick
- Allows selective application of commits.
- Useful for hotfixes or porting specific changes.
- Does not affect the branch structure.

---

This demonstrates how to use Git cherry-pick to apply specific commits from one branch to another.
