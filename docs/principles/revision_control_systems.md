# Revision Control Systems

Revision control, not to be confused with version control is system used to manage change to digital content over time. They allow multiple users to collaborate on a single document or set of files while maintaining a record of all changes.

Most revision control systems provide:
- Versioning: Each change made to the content creates a new version, which is stored in the system.
- Check-in/Check-out: Users can check out specific versions of the content for editing and then check them back in when finished.
- Conflict resolution: When multiple users make changes to the same content simultaneously, the system resolves conflicts by merging or reconciling the changes.
- Branching and merging: Users can create separate branches of the content, allowing them to work on different versions independently.

Every company will have their own workflow to manage a system using an RCS but the typical ones are:

- Feature Branch
- Gitflow
- Github flow
- Forking

## Typical Workflow
### Solo Development

A solo developer can normally work on the trunk (main) of the repository without the need to branch. It is still a good idea to tag code after each feature is complete if you are following an agile process. It allows you to identify a done state of the code and give an easy way to compare changes between features without the need to remember commit ids.

``` mermaid
gitGraph
    checkout main
    commit id: "setting up project"
    commit id: "implemented feature x"
    commit id: "added missing tests" tag: "v1.0.0"

```

### Group Development 
When working as a group create a feature branch for your work would be typical. If you were following CI/CD and Github flow processes once your feature was complete and code reviewed you would merge this code back into main ready for the next release. 

!!! note
    To minimise conflicts in the main branch you would merge main into your branch before pushing your changes back.

``` mermaid
---
title: Group Development
---
gitGraph
    commit
    commit
    checkout main
    branch feature
    checkout feature
    commit
    commit
    checkout main
    merge feature
    commit
    commit tag: "v1.0.0"
```


## Further Reading
- [What is Version Control](https://www.atlassian.com/git/tutorials/what-is-version-control){target="_blank"}
- [Release Strategies Using Git Branching](https://medium.com/@Insighture/release-strategies-using-git-branching-025b2edcc67a){target="_blank"}