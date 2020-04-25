# FreeProving Guidelines

This repository contains common guidelines that govern all repositories that are part of the FreeProving project.
The guidelines should not be replicated across repositories to guarantee consistency and ease maintainability.

## Contributing Guidelines

The following link to the contributing guidelines of the FreeProving project should be included in the `CONTRIBUTING.md` file of all repositories that are part of the FreeProving project.

```markdown
# Contributing

See the [contributing guidelines][] of the FreeProving project.

[contributing guidelines]:
  https://github.com/FreeProving/guidelines/blob/master/CONTRIBUTING.md
  "Contributing Guidelines of the FreeProving project"
```

## Code of Conduct

The following link to our Code of Conduct should be included in the `CODE_OF_CONDUCT.md` file of all repositories that are part of the FreeProving project.

```markdown
# Code of Conduct

The Free Proving project and everyone participating in it is governed by our [Code of Conduct][CODE_OF_CONDUCT].
By participating, you are expected to uphold this code.

[CODE_OF_CONDUCT]:
  https://github.com/FreeProving/guidelines/blob/master/CODE_OF_CONDUCT.md
  "Code of Conduct of the FreeProving project"
```

Include the following comment in every pull request or issue template to make contributors aware of our Code of Conduct.

```markdown
<!--
  Have you read our Code of Conduct?
  By filing an issue or pull request, you are expected to comply with it, including treating everyone with respect:
  https://github.com/FreeProving/guidelines/blob/master/CODE_OF_CONDUCT.md
-->
```

## Issue templates

The `ISSUE_TEMPLATE` directories contains templates for issue templates.
These templates can be copied to the `.github/ISSUE_TEMPLATE` directory of all other repositories.
Adapt the templates if necessary.

## CI Pipeline and Bash scripts

The contributing guidelines assume that the repository has a GitHub Actions continuous integration (CI) pipeline.
The configuration can be copied from the CI pipeline of the Free Compiler.
Slight adaptations will be necessary on a per repository basis as not all jobs of the CI pipeline make sense in all cases and some build steps differ.

Additional bash scripts whose usage is recommended by the contributing guidelines should also be copied and adapted from the Free Compiler if applicable in the context of the respective repository.

## License

This repository includes a [template for the The 3-Clause BSD License][guidelines/LICENSE] that is used by most repositories of the FreeProving project.
The copyright holders of the individual repositories may differ.
Some repositories may choose a different license if necessary.

[guidelines/LICENSE]:
  https://github.com/FreeProving/guidelines/blob/master/LICENSE
  "FreeProving Guidelines — LICENSE file template"
