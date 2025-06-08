```admonish warning "TODO"
This section is currently unfinished! Help contribute more information.
```

# Git for Dummies

Git is a very commonly used version control software whose version structure is represented in terms of sequences of changes, where each change is called a "commit", and sequences of commits can be worked on in parallel.

A sequence of commits is called a "branch". Generally, the branch called "main" is the base branch that all other branches are based on, to some degree. The separate branches permit developers to create their own changes without having to handle changes made by other developers all the time. However, a branch can serve the role of specifying release type, though that's not the case in Supersymmetry.

Because these updates have to be shared online, a space such as GitHub is used to store the data, and this means that the Git repository that you have locally is not the same as the main branch.

The commits made locally also need to be made manually. In fact, local changes can either be ready for committing (staged/in the index) or not ready for committing (in the working directory).

To move all changes to the index, ```git add .``` is essential (if you're not using an IDE). Then, ```git commit -m <description>``` can be used, converting the staged changes into a commit.

While working on a branch, you may want to integrate new features added to the main branch. Doing this requires using the command ```git pull```, which will *merge* the two branches, which just leads to a new commit on your branch. Usually, Git can handle merging automatically, but when the new features from the main branch do not line up cleanly with the changes you've made, a merge conflict results. Refer to [this link on StackOverflow](https://stackoverflow.com/questions/161813/how-do-i-resolve-merge-conflicts-in-a-git-repository) for a better idea of how this can be done.

When you're ready to integrate their changes into the main branch, you can create a *pull request* that allows everyone to verify its correctness before merging any new features from the main branch into it, however is necessary. 