Installing development dependencies
-----------------------------------
From the project root folder, just run:

`pip install -r dev-requirements.txt`

It is adviced that you do it on a `virtualenv` or, if you prefer to spin up the whole dev environment with just one command, you can run the PyOWM Docker image:

`docker run -d --name pyowm csparpa/pyowm`


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

1. File a bug issue on GitHub
2. Fork the repo on GitHub
3. Create a new branch from the development, name it *hotfix/xxx* where xxx is a very short description of the bug, eg: hotfix/wind-speed-neglected
4. Work on that new branch - commit, commit, commit
5. Let's improve the code quality of PyOWM: if you can, write at least one unit test that proves that the bug has been correctly fixed
6. Issue a pull request and name it after the bug issue you've opened
7. If I'm not quick on checking the pull request, please ping me!

...and how do I submit new feature requests?
--------------------------------------------
That's simple as well!

1. Open an issue on GitHub (describe in detail the feature you're proposing)
2. Depending on the entity of the request:
   - if it's going to be a breaking change, the feature will be scheduled for embedding into the next major release - so no code shall be provided by then
   - if it's only an enhancement, please proceed with the above workflow and submit a pull request from a *feature/xxx* branch you'll create on your fork