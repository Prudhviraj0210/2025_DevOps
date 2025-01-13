# Git Conflict Example

A **Git conflict** occurs when changes from two different branches or commits conflict with each other during a merge. Below is an example to understand how conflicts happen and how to resolve them.

---

## Scenario
1. **Initial File (on the `main` branch):**

   ```txt
   # greetings.txt
   Hello, World!
   ```

2. **Branch A (`feature-1`) modifies the file:**

   ```txt
   # greetings.txt
   Hello, Universe!
   ```

3. **Branch B (`feature-2`) modifies the same file differently:**

   ```txt
   # greetings.txt
   Hello, Everyone!
   ```

4. If both branches are merged into `main`, Git cannot automatically decide which change to keep, resulting in a conflict.

---

## Steps to Reproduce a Git Conflict

### 1. Create the repository and initial branch

```bash
git init conflict-demo
cd conflict-demo
echo "Hello, World!" > greetings.txt
git add greetings.txt
git commit -m "Initial commit"
```

### 2. Create and modify `feature-1`

```bash
git checkout -b feature-1
echo "Hello, Universe!" > greetings.txt
git add greetings.txt
git commit -m "Updated greetings in feature-1"
```

### 3. Create and modify `feature-2`

```bash
git checkout main
git checkout -b feature-2
echo "Hello, Everyone!" > greetings.txt
git add greetings.txt
git commit -m "Updated greetings in feature-2"
```

### 4. Merge both branches into `main`

```bash
git checkout main
git merge feature-1
git merge feature-2
```

---

## Conflict Output
When you attempt to merge `feature-2` into `main` after merging `feature-1`, Git will output something like:

```bash
Auto-merging greetings.txt
CONFLICT (content): Merge conflict in greetings.txt
Automatic merge failed; fix conflicts and then commit the result.
```

### Conflict Markers in `greetings.txt`
The `greetings.txt` file will look like this:

```txt
<<<<<<< HEAD
Hello, Universe!
=======
Hello, Everyone!
>>>>>>> feature-2
```

---

## Resolving the Conflict
1. Open the file (`greetings.txt`) and decide which change to keep, or merge them. For example:

   ```txt
   Hello, Universe and Everyone!
   ```

2. Add the resolved file and complete the merge:

   ```bash
   git add greetings.txt
   git commit -m "Resolved conflict in greetings.txt"
   ```

---

This demonstrates how conflicts occur and how to resolve them in Git!
