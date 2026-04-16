### Updating one liner
lets say we again made some change to a feature branch which is already merged to the development branch. Every code we write locally and commit on this feature branch will be just the changes for this branch. 

This might cause problem because pushing the feature branch to repository will not update the development branch and will only update the feature branch of the repository and make the feature branch ahead of the development branch.

To fix this issue, first checkout to the local development branch in your system and perform these commands

```bash
git checkout development
git pull origin development
```

After that merge the feature branch to your local development branch.

```bash
git merge your-branch-name -m "Merged changes: merge reason message"
```

Now your local development branch is updated and ahead. Finally push the changes to the repository:

```bash
git push orgin development
```

This will also update the online development branch in your repository and make your online development branch ahead of the feature branch.
