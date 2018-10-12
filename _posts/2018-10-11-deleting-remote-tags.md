---
title: Deleting a remote git tag
thumb: github-thumb.jpg
author: Chris
type: posts
---

Mistakes happen and sometimes you need to be able to delete something you already pushed to the git remote. Deleting a branch is pretty straightforward, but deleting a tag is slightly different. Here is an example of deleting a tag `v1.2.3`:

#### Deleting a remote tag

```
git push origin :refs/tags/v1.2.3
```

#### Deleting a local tag

```
git tag -d v1.2.3
```
