To view a log of all your stashes in Git, you can use the following command:

```bash
git stash list
```

This command will display a list of all stashed changesets in the repository. Each stash is identified by a unique name like `stash@{0}`, `stash@{1}`, etc., followed by a brief description of the stash.

___

If you want to make a temporary backup of your working directory (with all the changes, including untracked files) between commits, there are a few methods:

### 1. Using Git:

**a. Stashing with Git**

This is best if you want a temporary save point that you can later apply back.

```bash
git stash save "Temporary backup"
```

Remember that `git stash` also resets your working directory to the last commit. To retrieve the stashed changes:

```bash
git stash apply
```

___
To delete stashes in Git, you can use the `git stash drop` command followed by the name of the stash. If you want to delete all stashes, you can use the `git stash clear` command. Here's how you can manage stash deletion:

1. **Delete a Specific Stash**:

   If you want to delete a specific stash, first identify its name using:

   ```bash
   git stash list
   ```

   This will give you a list of stashes like `stash@{0}`, `stash@{1}`, and so on. 

   To delete, for example, `stash@{1}`, you would use:

   ```bash
   git stash drop stash@{1}
   ```

2. **Delete the Most Recent Stash**:

   If you just want to delete the most recent stash, you can use:

   ```bash
   git stash drop
   ```

   Without specifying a stash name, this command will drop the latest stash (`stash@{0}`).

3. **Delete All Stashes**:

   If you want to delete all the stashed changes, you can clear the entire stash list with:

   ```bash
   git stash clear
   ```

Always be careful when using the `drop` or `clear` commands, as these actions are irreversible. Once a stash is deleted, it cannot be recovered.


If you want to stash your changes without modifying the current state (look) of your working directory, you can use the `--keep-index` option with `git stash`. This will stash all changes that have not been added to the index (via `git add`), allowing your working directory to retain its current appearance.

Here's how you can use it:

```bash
git stash save --keep-index "Your stash message"
```

However, a couple of things to note:

1. This command only stashes the changes that have not been added to the index. If you have staged changes (with `git add`), those will remain in the index and won't be stashed.
  
2. Untracked files won't be stashed unless you use the `-u` or `--include-untracked` option.

To include all changes, both staged and unstaged, in the stash while leaving the working directory unchanged, you can combine the flags:

```bash
git stash save --keep-index --include-untracked "Your stash message"
```

After running this, you'll have a new stash created, but your working directory will look the same as before.
