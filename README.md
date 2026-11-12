# Python Package Template

This is a lightweight template repository to generate starter code for Python packages. It primarily helps with the basic structure and a robust CI/CD, that covers:
- Formatting
- Linting
- Static type checking
- Testing and coverage
- Automated release management

To allow the automated release management job to work in the generated project, the `GITHUB_TOKEN` must be able to create and approve pull requests. This can be done by checking the box `Allow GitHub Actions to create and approve pull requests` under Settings -> Actions -> General -> Workflow permissions.

## Generating a project
`copier` is the tool used to create projects from this repository.
```bash
copier copy <url> <package_name>
```

If you have this repository on your local machine, you can use the following command to generate a repository (assuming you are in the root directory of this repository):
```bash
copier copy --vcs-ref=HEAD . <path>/<package_name>
```

This will create a directory called `package_name` in the location specified by `path` and make a copy of the template in this directory.

## Contributing
To contribute to this package, please open an issue and then create a pull request from it. To trigger the automated release job of the pipeline, the commits in the `main` branch must follow [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/). `release-please` parses commits using this specification and then decides whether the MAJOR, MINOR or PATCH version should be updated and updates the `CHANGELOG` using the commits as descriptions, so the commit message is very important. `release-please` opens up a release pull request that is updated with the latest commits in `main`. Once this pull request is merged, a new tag is created along with a corresponding GitHub release.

The following commits will result in a version bump:
1. **fix:** a commit of the _type_ `fix` patches a bug in your codebase (this correlates with [`PATCH`](http://semver.org/#summary) in Semantic Versioning).
2. **feat:** a commit of the _type_ `feat` introduces a new feature to the codebase (this correlates with [`MINOR`](http://semver.org/#summary) in Semantic Versioning).
3. **BREAKING CHANGE:** a commit that has a footer `BREAKING CHANGE:`, or appends a `!` after the type/scope, introduces a breaking API change (correlating with [`MAJOR`](http://semver.org/#summary) in Semantic Versioning).
A BREAKING CHANGE can be part of commits of any _type_.
4. _types_ other than `fix:` and `feat:` are allowed, for example [@commitlint/config-conventional](https://github.com/conventional-changelog/commitlint/tree/master/%40commitlint/config-conventional) (based on the [Angular convention](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines)) recommends `build:`, `chore:`,
  `ci:`, `docs:`, `style:`, `refactor:`, `perf:`, `test:`, and others. These will not bump the version but depending on the configuration in `pyproject.toml` they can end up in the CHANGELOG.
5. _footers_ other than `BREAKING CHANGE: <description>` may be provided and follow a convention similar to
  [git trailer format](https://git-scm.com/docs/git-interpret-trailers).

Additional types are not mandated by the Conventional Commits specification, and have no implicit effect in Semantic Versioning (unless they include a BREAKING CHANGE).