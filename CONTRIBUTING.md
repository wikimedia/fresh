# Contribute to Fresh

## Release process

Always work on a clean branch when releasing:

```
git remote update && git checkout -B release -t origin/HEAD
```

### Prep commit

1. Update the bin scripts:

   * Set `scriptversion` to the new version string.

   * Run `FRESH_INTERNAL_RUNCMD=_fresh_versions bin/fresh-node`
     for changed scripts and copy the new welcome text into the script.

   You can run `git diff` or `git add -p` at this point to easily determine the
   image changes for the release notes (e.g. updated Firefox version).

2. Write release notes in a new section atop [CHANGELOG.md](./CHANGELOG.md).

   If there were changes besides image updates, the following will summarise and
   attribute those, to include in the release notes.
   Remove entries not observable by a user.
   ```
   git log --format='* %s (%aN)' --no-merges --reverse $(git describe --tags --abbrev=0 HEAD)...HEAD | sort | grep -vE '^\* (build|docs?|tests?):'
   ```

3. Commit and submit to Gerrit:

   By submitting to Gerrit now, the commit hash will be publicly downloadable
   so that we can test the installer on it.

   ```
   git add -p
   git commit -m "Prepare <version> release"
   git review
   ```

4. Test the installer:

   * Update `fresh-install` and set `FRESH_VERSION` to the submitted draft commit hash
     (obtain via `git show`), and update the individual SHA256 hashed by running
     `bin/fresh-install --debug`.

   * Run `bin/fresh-install`
   * Confirm `fresh-node` works on your machine, showing the right Fresh and image version.

5. Amend prep commit and submit for review.
   ```
   git add -p
   git commit --amend
   git review
   ```

## Release commit

1. Set version string in the URL under "Quick start" in the README,
   This must match the Git tag we'll soon create.

   Also set the new version string in `FRESH_VERSION` in `bin/fresh-install`.

2. Commit and submit for review.
   ```
   git add -p
   git commit -m "Release <version>"
   git review
   ```

3. Once merged, create the tag and push it.
   ```
   git tag -s <version>
   git push --tags
   ```
