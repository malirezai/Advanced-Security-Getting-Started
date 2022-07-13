# Advanced Security Resources and Videos

This guide is intended to help you get started with GitHub Advanced Security. Sections below cover a variety of topics, including:

- Introduction to GitHub Advanced Security
- Private Repository Secret Scanning
- Code Scanning

## Introduction to GitHub Advanced Security

GitHub Advanced Security is a suite of capabilities for improving the security posture of your code. At present, GitHub Advanced Security provides two capabilities in addition to the [public repository secret scanning](https://help.github.com/en/github/administering-a-repository/about-secret-scanning#about-secret-scanning-for-public-repositories), [dependency graph](https://help.github.com/en/github/visualizing-repository-data-with-graphs/listing-the-packages-that-a-repository-depends-on#about-the-dependency-graph), [security alerts](https://help.github.com/en/github/managing-security-vulnerabilities/about-security-alerts-for-vulnerable-dependencies), and [automated security updates](https://help.github.com/en/github/managing-security-vulnerabilities/configuring-automated-security-updates) to which you already have access. They are:

- Private Repository Secret Scanning
- Code Scanning
- Dependency Review

## Primer Videos

- Achieving DecSecOps with GitHub Advanced Security: https://www.youtube.com/watch?v=hln5v7odguE
- Community Powered Security Analysis with CodeQL: https://githubuniverse.com/Community-powered-security-analysis-with-CodeQL/
- Catching Vulnerabilities Early with GitHub: https://githubuniverse.com/Catching-vulnerabilities-early-with-GitHub/
- So You Committed a Secret: https://githubuniverse.com/So-you-committed-a-secret/

## Private Repository Secret Scanning

When you push commits to a private repository with secret scanning enabled, GitHub scans the contents of the commits for secrets. Alerts are then sent to repository administrators and organization owners.

See the [Documentation](https://help.github.com/en/github/administering-a-repository/configuring-secret-scanning-for-private-repositories) on how to **configure Private Secret Scanning**.

## Code Scanning

Code scanning is a developer-first static application security testing (SAST) product that is built into GitHub. Once configured, it scans every code change in your repository for security vulnerabilities, and flags them in the developer workflow. This makes it easy to find security vulnerabilities in your code before they ever reach production.

Code scanning is powered by the [CodeQL](https://help.github.com/en/github/finding-security-vulnerabilities-and-errors-in-your-code/about-code-scanning#about-codeql) analysis engine to find potential vulnerabilities. Out of the box, Code Scanning includes hundreds of CodeQL queries written + open sourced by the [GitHub Security Lab](https://securitylab.github.com) and leading security researchers to find potential vulnerabilities in your code with minimal configuration.

### Getting Started with Code Scanning

#### Quick start: Code Scanning with **CodeQL Action**

The fastest way to get started with CodeQL is to follow this [guide](https://help.github.com/en/github/finding-security-vulnerabilities-and-errors-in-your-code/enabling-code-scanning) to onboard repositories. The guide will create a new GitHub Actions Workflow file with the CodeQL Action configured.

You can view, fix, and close alerts for potential vulnerabilities or errors directly within the repository. See [Managing alerts from code scanning](https://help.github.com/en/github/finding-security-vulnerabilities-and-errors-in-your-code/managing-alerts-from-code-scanning) for more information on viewing alerts. Additionally, alerts will be displayed directly within a Pull Request after the Analysis has run. It is also possible to require successful code scanning before merging Pull Requests by enabling [protected branches](https://help.github.com/en/github/administering-a-repository/configuring-protected-branches) with [status checks](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/about-status-checks).

#### Quick start: Code Scanning with the **CodeQL CLI**

You can use the CodeQL CLI to run code scanning on code that you're processing in a third-party continuous integration (CI) system following this [guide](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/running-code-scanning-in-your-ci-system).

The CodeQL CLI has detailed documentation: https://codeql.github.com/docs/codeql-cli/getting-started-with-the-codeql-cli/

The CodeQL CLI is a command-line tool that runs CodeQL analysis on a checkout of a GitHub repository. You add the CLI calls as part of your build pipeline, then create a database with CodeQL results. These results are displayed as code scanning alerts in the repository once uploaded to GitHub. See [Using the CodeQL with 3rd Party CI](https://gist.github.com/thedave42/1bccb81fa7fef6354f9d611b0d4a1b9a)
 
#### Notes

- Code Scanning via CodeQL Analysis runs as a part of the CI/CD Workflow in [GitHub Actions] (https://help.github.com/en/actions) or on third-party CI systems with the [CodeQL runner](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/running-code-scanning-in-your-ci-system#about-the-codeql-runner).
  - Every onboarded repository can utilize a GitHub Actions Workflow with the CodeQL Action that will run the analysis or with the CodeQL Runner to integrate into existing CI systems.
- For compiled languages (C/C++, C#, Go, Python), CodeQL analysis must run after a successful build
  - By default, CodeQL Analysis will attempt to Autobuild your project.
  - If Autobuild fails, you will need to first configure GitHub Actions to properly build your application before running the CodeQL Analysis.
- CodeQL Analysis runs only a limited set of high confidence security queries by default.
  - This ensures that the False Positive rate stays very low so that too much noise does not overwhelm developers.
  - It is possible to include other query sets including additional security queries and code quality queries.
- Results from third-party static analysis tools can be displayed using a [supported SARIF file](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/sarif-support-for-code-scanning)

#### APIs

The [Code Scanning API](https://docs.github.com/en/free-pro-team@latest/rest/reference/code-scanning) lets you retrieve and update code scanning alerts from a repository. You can use the endpoints to create automated reports for the code scanning alerts in an organization or upload analysis results generated using offline code scanning tools. 
- [List code scanning alerts for a repository](https://docs.github.com/en/free-pro-team@latest/rest/reference/code-scanning#list-code-scanning-alerts-for-a-repository)
- [Upload a SARIF file](https://docs.github.com/en/free-pro-team@latest/rest/reference/code-scanning#upload-a-sarif-file) containing the results of a code scanning analysis to make the results available in a repository. 

[Code Scanning Alert webhook event](https://docs.github.com/en/free-pro-team@latest/developers/webhooks-and-events/webhook-events-and-payloads#code_scanning_alert) - Activity related to code scanning alerts in a repository. The type of activity is specified in the action property of the payload object.


## Depandabot Version Updates from private GitHub repos
- https://github.blog/changelog/2020-12-02-dependabot-version-updates-from-private-github-repositories/

## Dependency Review

[About dependency review](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/reviewing-dependency-changes-in-a-pull-request#about-dependency-review). 

If a pull request targets your repository's default branch and contains changes to package manifests or lock files, you can display a dependency review to see what has changed. The dependency review includes details of changes to indirect dependencies in lock files, and it tells you if any of the added or updated dependencies contain known vulnerabilities.

