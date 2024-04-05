# Do It

<img src="https://i.giphy.com/media/gitp8bQ5sAJxj6Ps3Y/giphy.webp"
     onerror="this.onerror=null;this.src='https://i.giphy.com/gitp8bQ5sAJxj6Ps3Y.gif';"
     alt="Do It, but said by Palpatine" />

This documentation goal is to provide a few good practices I try to follow myself.

## Git

### Branching

Name your main branches following gitflow. I usually use other prefixes, too. But it is important to be consistent accross the team.

Prefixes example:

| prefix   | why                                                              |
|----------|------------------------------------------------------------------|
| release  | for protected release branches only                              |
| hotfix   | for quickly fixing critical issues in production                 |
| fix      | for fixing a bug                                                 |
| feature  | for adding, removing or modifying a feature                      |
| refactor | for everything that is not anything else (e.g. code refactoring) |
| docs     | for documentation                                                |
| build    | for pipelines                                                    |

### Commits

Use [angular naming](https://github.com/angular/angular/blob/main/CONTRIBUTING.md#type). Important copy-pasta:

```text
<type>(<scope>): <short summary>
  │       │             │
  │       │             └─⫸ Summary in present tense. Not capitalized. No period at the end.
  │       │
  │       └─⫸ Commit Scope: animations|bazel|benchpress|common|compiler|compiler-cli|core|
  │                          elements|forms|http|language-service|localize|platform-browser|
  │                          platform-browser-dynamic|platform-server|router|service-worker|
  │                          upgrade|zone.js|packaging|changelog|docs-infra|migrations|
  │                          devtools
  │
  └─⫸ Commit Type: build|ci|docs|feat|fix|perf|refactor|test
```

Type must be one of the following:

- **build**: Changes that affect the build system or external dependencies (example scopes: gulp, broccoli, npm)
- **ci**: Changes to our CI configuration files and scripts (examples: CircleCi, SauceLabs)
- **docs**: Documentation only changes
- **feat**: A new feature
- **fix**: A bug fix
- **perf**: A code change that improves performance
- **refactor**: A code change that neither fixes a bug nor adds a feature
- **test**: Adding missing tests or correcting existing tests

#### Granularity

Split your work in multiple commits. You're free to choose the correct granularity, but don't make undred-files commits.

## Pull request

### 1\. Code Review

- Request code review from at least two team members. Synchronously if necessary.
- Address and resolve code review comments.

#### When Commenting

- Be respectful.
- Explain what you see, ask questions.

Read [conventional comments](https://conventionalcomments.org/), which has great insights about commenting.

### 2\. Continuous Integration (CI)

- Confirm CI build pipeline has passed successfully.
- All build and unit tests in the CI/CD pipeline are green.

### 3\. SonarQube Analysis

- SonarQube analysis passed.
- Address and fix all SonarQube issues (bugs, vulnerabilities, code smells).

### 4\. Code Coverage

- Ensure code coverage >= 80%.
- Address and fix any failing tests or coverage gaps.

### 5\. Functional Testing

- Verify that changes work as expected in a local development environment.
- Confirm new features or bug fixes resolve reported issues.

### 6\. Documentation

- Write BDD scenarios whenever it is possible (live documentation should be generated).
- Ensure code changes are appropriately documented, including the TAD (i.e. Technical Architecture Document) and README updates.

### 7\. Merge

- Merge the PR into the correct target branch.
- Delete the feature branch after successful merge.

#### Merge Strategy

Use either `squash` if it is a small PR with only one commit (in Azure DevOps, results to one commit with the PR description as body), or `rebase` with `--no-ff` otherwise ([semi-linear in Azure DevOps](https://devblogs.microsoft.com/devops/pull-requests-with-rebase/#semi-linear-merge)).

### 8\. Move your work item / JIRA Card

- The card has to have the correct status.

## Code

### Coding Standards

- Code following the established coding standards and conventions in your team.
- Write in one language only (e.g. don't mix French and English, choose one).
- Use design patterns wherever applicable.
- Anticipate issues (e.g. resilience, security, ...)

### Be a craftman

Follow the [Software Craftmanship Manifesto](https://manifesto.softwarecraftsmanship.org/).

### Know your Accronyms

Embrace:

- SOLID Principles
- SoC
- DRY
- KISS
- YAGNI

## Tests

### Unit Tests

- Name your method to tell a story.
  
  ```csharp
  public void DoSomething_WhenThisHappened_AndThatOccured() {
    // Arrange

    // Act

    // Assert
  }
  ```

- Don't keep useless Arrange/Act/Assert comments, add a carriage return instead.
- Respect the same principles as when you code a feature.

### Testing Standards

- Cover your code just as you'd cover yourself in a harsh winter. Not always at 100%, but where you need it most.
- Know test types and when to use them (Unit Tests, Integration Tests, E2E, PBT, ...).

### Methods

Embrace:

- TDD
- BDD
