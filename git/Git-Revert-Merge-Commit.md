# How to revert merge commit
## Initial State
``` bash 
       A---B---C (feature)
      /         \
     /           \
D---E             M (merge commit)
     \           /
      \         /
       F---G---H (develop)
```
### Explanation
- E: Common ancestor (where feature branched from develop)
- A,B,C: Feature branch commits
- F,G,H: Develop branch commits
- M: Merge commit (develop → feature)
  
## Revert with -m 1
```bash
git revert -m 1 <merge-commit-hash>
```
```bash
       A---B---C---M---R (feature)
      /         \      ↑
     /           \      \
D---E             M      \
     \           /        \
      \         /          \
       F---G---H (develop)  \         
                             \ 
                    Revert (removes F,G,H changes)
```

## Revert with -m 2
```bash
git revert -m 2 <merge-commit-hash>
```
```bash
       A---B---C---M---R (feature)
      /         \      ↑
     /           \      \
D---E             M      \
     \           /        \
      \         /          \
       F---G---H (develop)  \         
                             \ 
                    Revert (removes A,B,C changes)
```
## Key Points
- -m 1: Preserves feature branch history (A,B,C)
- -m 2: Preserves develop branch history (F,G,H)
- Both create new revert commit (R)
- Original branches remain unchanged