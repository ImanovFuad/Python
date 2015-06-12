Installing development dependencies
-----------------------------------
From the project root folder, just run:

`pip install -r dev-requirements.txt`

Branching
---------

The project adopts @nvie's branching model:

- the "develop" branch contains work-in-progress code 
- new "feature" branches can be opened by any contributor from the "develop" branch. Each feature branch adds a new feature/enhancement
- new "hotfix" branches can be opened by any contributor from the "develop" branch. Each hotfix fixes an urgent bug that impacts the current version of PyOWM. Hotfixes will be merged back in both "master" and "develop" branches by me
- the "master" branch will contain only stable code and the "develop" branch will be merged back into it only when a milestone is completed or hotfixs need to be applied. Merging of "develop" into "master" will be done by me when releasing - so please **never apply your modifications to the master branch!!!**

So how do I submit bugfixes?
---------------------------
That's simple! Just:

1. Fork the repo on GitHub
2. Create a new branch from the development, name it *hotfix/xxx* where xxx is a very short description of the bug, eg: hotfix/wind-speed-neglected
3. Work on that new branch - commit, commit, commit
4. Let's improve the code quality of PyOWM: if you can, write at least one unit test that proves that the bug has been correctly fixed
5. Issue a pull request
6. If I'm not quick on checking the pull request, please ping me!
