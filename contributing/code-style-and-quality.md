---
title:  "Code Style and Quality Guide"
---


## Code Style and Quality Guide (OUTDATED)

*Note: These guidelines are outdated and will be updated soon.*

### Pull requests and commit message
{:.no_toc}

- **Single change per PR**. Please do not combine various unrelated changes in a single pull request. Rather, open multiple individual pull requests where each PR refers to a Jira issue. This ensures that pull requests are *topic related*, can be merged more easily, and typically result in topic-specific merge conflicts only.

- **No WIP pull requests**. We consider pull requests as requests to merge the referenced code *as is* into the current *stable* master branch. Therefore, a pull request should not be "work in progress". Open a pull request if you are confident that it can be merged into the current master branch without problems. If you rather want comments on your code, post a link to your working branch.

- **Commit message**. A pull request must relate to a Jira issue; create an issue if none exists for the change you want to make. The latest commit message should reference that issue. An example commit message would be *[FLINK-633] Fix NullPointerException for empty UDF parameters*. That way, the pull request automatically gives a description of what it does, for example, what bug does it fix in what way.

- **Append review commits**. When you get comments on the pull request asking for changes, append commits for these changes. *Do not rebase and squash them.* It allows people to review the cleanup work independently. Otherwise reviewers have to go through the entire set of diffs again.

- **No merge commits**. Please do not open pull requests containing merge commits. Use `git pull --rebase origin master` if you want to update your changes to the latest master prior to opening a pull request.

### Exceptions and error messages
{:.no_toc}

- **Exception swallowing**. Do not swallow exceptions and print the stacktrace. Instead check how exceptions are handled by similar classes.

- **Meaningful error messages**. Give meaningful exception messages. Try to imagine why an exception could be thrown (what a user did wrong) and give a message that will help a user to resolve the problem.

### Tests
{:.no_toc}

- **Tests need to pass**. Any pull request where the tests do not pass or which does not compile will not undergo any further review. We recommend to connect your personal GitHub accounts with [Travis CI](http://travis-ci.org/) (like the Flink GitHub repository). Travis will run tests for all tested environments whenever you push something into *your* GitHub repository. Please note the previous [comment about flaky tests]( {{site.base}}/contribute-code.html#verifying-the-compliance-of-your-code).

- **Tests for new features are required**. All new features need to be backed by tests, *strictly*. It is very easy that a later merge accidentally throws out a feature or breaks it. This will not be caught if the feature is not guarded by tests. Anything not covered by a test is considered cosmetic.

- **Use appropriate test mechanisms**. Please use unit tests to test isolated functionality, such as methods. Unit tests should execute in subseconds and should be preferred whenever possible. The names of unit test classes have to end in `*Test`. Use integration tests to implement long-running tests. Flink offers test utilities for end-to-end tests that start a Flink instance and run a job. These tests are pretty heavy and can significantly increase build time. Hence, they should be added with care. The names of end-to-end test classes have to end in `*ITCase`.

### Documentation
{:.no_toc}

- **Documentation Updates**. Many changes in the system will also affect the documentation (both Javadocs and the user documentation in the `docs/` directory). Pull requests and patches are required to update the documentation accordingly; otherwise the change can not be accepted to the source code. See the [Contribute documentation]({{site.base}}/contribute-documentation.html) guide for how to update the documentation.

- **Javadocs for public methods**. All public methods and classes need to have Javadocs. Please write meaningful docs. Good docs are concise and informative. Please do also update Javadocs if you change the signature or behavior of a documented method.

### Code formatting
{:.no_toc}

- **No reformattings**. Please keep reformatting of source files to a minimum. Diffs become unreadable if you (or your IDE automatically) remove or replace whitespaces, reformat code, or comments. Also, other patches that affect the same files become un-mergeable. Please configure your IDE such that code is not automatically reformatted. Pull requests with excessive or unnecessary code reformatting might be rejected.



-----

## Code style


-----

## Best practices

- Travis: Flink is pre-configured for [Travis CI](http://docs.travis-ci.com/), which can be easily enabled for your personal repository fork (it uses GitHub for authentication, so you do not need an additional account). Simply add the *Travis CI* hook to your repository (*Settings --> Integrations & services --> Add service*) and enable tests for the `flink` repository on [Travis](https://travis-ci.org/profile).