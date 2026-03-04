# GitHubActionsLab-Bazil

## Workflow Overview

### Workflow 1: Dependent Jobs (dependent-jobs.yml)
This workflow demonstrates job dependencies using the `needs` keyword. The jobs execute in a specific sequential order:
1. **build** - First job that simulates building the application
2. **test** - Depends on build, runs tests after build completes
3. **deploy** - Depends on test, runs deployment after tests pass

**Trigger:** Runs on every push to the master branch

**Key Concept:** The `needs: build` and `needs: test` keywords create dependencies between jobs, ensuring they run in the correct order.

### Workflow 2: Multi-Platform Testing (multi-platform.yml)
This workflow demonstrates parallel job execution across different operating systems. Three independent jobs run simultaneously:
1. **ubuntu-job** - Runs on Ubuntu Linux
2. **windows-job** - Runs on Windows
3. **macos-job** - Runs on macOS

**Trigger:** Runs on every pull request to the master branch

**Key Concept:** Since there are no `needs` keywords, all jobs run in parallel, demonstrating platform-specific command differences (e.g., `uname -a` vs `systeminfo`).

## Key Concepts Demonstrated

### needs
- Creates explicit dependencies between jobs
- Jobs listed in `needs` must complete successfully before the dependent job starts
- Absence of `needs` means jobs run in parallel

### runs-on
- Specifies the operating system the job runs on
- Options: `ubuntu-latest`, `windows-latest`, `macos-latest`
- Different OS require different shell commands

### env (Environment Variables)
- Set at workflow, job, or step level
- Accessible to all steps in their scope

### uses
- Integrates GitHub Actions from the marketplace
- Example: `actions/checkout@v4` checks out your repository code

## Challenges and Solutions

### Challenge 1: YAML Syntax
**Solution:** Validate YAML syntax before pushing using online YAML validators to catch indentation errors early.

### Challenge 2: Windows PowerShell vs Bash
**Solution:** Use Windows-compatible commands (`systeminfo`, `type`) for Windows jobs and Unix commands (`uname`, `cat`) for Linux/macOS jobs.

### Challenge 3: Job Execution Order
**Solution:** Use meaningful job names and review the Actions tab's dependency visualization to verify correct execution order.

## How to Test

1. Push the `dependent-jobs.yml` to master to trigger Workflow 1
2. Create a new branch for `multi-platform.yml` changes
3. Push the `multi-platform.yml` to your new branch
4. Create a pull request to master to trigger Workflow 2
5. Monitor the Actions tab to see both workflows in action
