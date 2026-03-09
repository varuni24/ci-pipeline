# ci-pipeline 

We use GitHub Actions for the CI. The workflow is a single job named `build`. It checks out the repository, sets up the environment, then runs the three main steps lint, test, buildn so everything runs inside GitHub.

 

### 1. Code linting
- **flake8** This step fails the pipeline if Flake8 reports any style or syntax issues such as unused imports. It catches simple errors before they reach review.


### 2. Unit testing
- **pytest** All tests need to pass for the pipeline to continue. Test results are printed in the GitHub Actions log for that run, showing which tests ran and whether they passed/failed.


### 3. Build automation
- **compile** Runs after the linter and tests succeed. If lint or tests fail the job stops and the build step is not executed. If successful, `py_compile` verifies that `app.py` is valid and can be compiled as a minimal build.


### Trigger Pipeline
The pipeline runs on every pull request. 

### Challenges Faced
Had to be creative to define a "build" for a script based project. For this we used `py_compile` on `app.py` as a minimal compile check. Making sure the build step ran only after lint and tests, kept all three in one job so a failed step stops the run.




