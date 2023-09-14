If you simply want to save the current state of your working directory without committing and without affecting your working directory (i.e., without stashing and reverting), you have a few options:
___

### 1. Filesystem Snapshot

You could simply make a copy of your entire working directory. This is straightforward but can consume a lot of disk space if your repository is large.

```bash
# For Linux/Unix:
cp -r /path/to/repo /path/to/repo_backup

# For Windows:
xcopy /E /I C:\path\to\repo C:\path\to\repo_backup
```

### 2. Create a WIP (Work-In-Progress) Commit

You can create a commit that captures the current state of the working directory. Later, you can amend, squash, or remove this commit as needed.

```bash
# Stage all changes
git add .

# Create a WIP commit
git commit -m "WIP: Save point"
```

### 3. Using `git worktree`

Git allows you to have multiple instances of the same repository, each pointing to a different branch. This could help you create a "snapshot" of your current work.

```bash
# This will create a new folder 'my_project_backup' with a new worktree
git worktree add /path/to/my_project_backup
```

### 4. Create a Local Branch

Another option is to create a new local branch and commit your changes there. This will keep your original branch unchanged while still saving your current work.

```bash
# Create and checkout a new branch
git checkout -b save-my-current-work

# Stage and commit all changes
git add .
git commit -m "Save point in new branch"
```

### 5. Export a Patch

You could also create a patch file that contains the current changes in your working directory. This file can later be applied to restore these changes.

```bash
# Create a patch file
git diff > my_changes.patch
```

Later, you can apply this patch.

```bash
git apply my_changes.patch
```

Each of these methods has its pros and cons, depending on what you want to achieve. For example, a filesystem snapshot is simple but can be resource-intensive. Worktree and local branches are more Git-native ways to handle your requirement, but they also create additional branches that you may need to clean up later. A WIP commit is straightforward, but you'll have to rewrite history to clean it up, which can be problematic if you've already pushed commits.

___
A patch is a text file that describes changes between two sets of code. A patch can be applied to a codebase to introduce those changes. Git has built-in support for creating and applying patches, which can be particularly useful for sharing changes that you have made locally but are not yet ready to commit or push to a repository. 

### Creating a Patch

You can create a patch file to capture the changes in your working directory compared to the last commit by running:

```bash
git diff > my_changes.patch
```

This generates a `.patch` file named `my_changes.patch` that contains the differences between your working directory and the `HEAD` commit. If you have staged changes (i.e., changes that have been added but not yet committed), you can include them in the patch by running:

```bash
git diff --cached > my_staged_changes.patch
```

Or to make a patch file for both staged and unstaged changes:

```bash
git diff HEAD > my_all_changes.patch
```

### Applying a Patch

To apply the changes from a patch file to your working directory, use:

```bash
git apply my_changes.patch
```

This will introduce the changes into your working directory but will not commit them. You would need to stage (`git add`) and commit (`git commit`) these changes manually.

### Reversing a Patch

You can also reverse the changes introduced by a patch by using the `-R` option:

```bash
git apply -R my_changes.patch
```

### Checking a Patch

Before applying a patch, you might want to see what changes it would make. You can do this without actually applying the patch:

```bash
git apply --stat my_changes.patch
```

Or you can check whether the patch can be applied cleanly:

```bash
git apply --check my_changes.patch
```

### Notes

- Patch files are portable and can be sent via email, applied to other code repositories, or manipulated with text tools.
- Applying a patch involves modifying files in your working directory or your index. It doesn't create or apply commits.
- Patches generated with `git diff` are intended specifically for the Git version control system and may not apply cleanly to a non-Git repository.

Patching is a powerful feature that allows you to share, apply, or even revert changes in a codebase, all without altering commit history.
The command to amend a commit in Git is `git commit --amend`. This command allows you to modify the most recent commit by adding new changes to it or changing its commit message. Here's how to use it in different scenarios:

### Amend with Additional Changes

If you've made changes that you forgot to include in the most recent commit, you can stage those changes and then amend the commit:

1. Make the additional changes in the working directory.
2. Stage those changes:

    ```bash
    git add .
    ```
   or if you want to add specific files:

    ```bash
    git add filename1 filename2
    ```

3. Amend the last commit:

    ```bash
    git commit --amend
    ```

### Amend the Commit Message

If you simply want to change the commit message of the most recent commit, you can do this:

1. Run:

    ```bash
    git commit --amend -m "New commit message"
    ```

   Or, if you don't include the `-m` option, an editor will open displaying the old commit message. You can edit the message, save it, and exit to update the commit.

### Amend with No Changes

If you don't stage any changes before running `git commit --amend`, Git will reuse the snapshot from the last commit and only update the commit message.

### Warning: Changing Published Commits

The `git commit --amend` command replaces the last commit with a new one. This changes the commit history, which can be dangerous if you've already pushed commits to a shared repository. If you have, and you still want to amend the commit, you'll have to force push using `git push origin <branch-name> --force`. However, this can overwrite changes on the remote that you don't have locally, and is generally not recommended for shared branches.

Instead, if you've already pushed the commit you want to amend, a safer way is to create a new commit that undoes the changes you want to get rid of, or to start a new branch from before the change you want to discard. Then you can push this new commit or new branch to the remote repository.