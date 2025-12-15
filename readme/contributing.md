# Contributing

🤝 There are several ways you can help in the development of DocBox!

* 🔧 [Send a pull request](contributing.md#send-a-pull-request)
* 🐛 Submit a bug or feature request to our [Jira issue tracker](https://ortussolutions.atlassian.net/projects/DOCBOX)
* ✅ [Write a test](contributing.md#testing-docbox)

## 🔧 Send a Pull Request

* Fork [DocBox](https://github.com/Ortus-Solutions/DocBox) or the [DocBox documentation repo](https://github.com/ortus-docs/docbox-docs)
* Clone the repository fork to your machine - `git clone git@github.com:ME/DocBox.git`
* Create a `feature/` or `patch/` branch: `git checkout -b patch/syntax-error-in-html-output`
* Make your changes, commit as normal, and use `git push` to sync your commits to Github.
* Please target all PRs at the `development` branch.

## ✅ Testing DocBox

DocBox has a suite of Testbox specs validating that it works as expected. New features and bug fix PRs should \(ideally\) contain accompanying tests. Here's how to do that via CommandBox:

1. After cloning the repo, run `box install` to install development dependencies
2. Run `box start` to boot a test server
3. Run `box testbox run` to run the suite of DocBox tests.
4. Edit test specs in `tests/specs` as necessary, and run `box testbox run` again to validate tests pass.

