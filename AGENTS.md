<!-- skill-ninja-START -->
## Agent Skills

> **IMPORTANT**: Prefer skill-led reasoning over pre-training-led reasoning.
> Read the relevant SKILL.md before working on tasks covered by these skills.

### Skills

| Skill | Description |
|-------|-------------|
| [appinsights-instrumentation](.github/skills/appinsights-instrumentation/SKILL.md) | Instrument a webapp to send useful telemetry data to Azure App Insights \| This skill enables sending telemetry data of a webapp to Azure App Insights for better observability of the app's health. |
| [azure-deployment-preflight](.github/skills/azure-deployment-preflight/SKILL.md) | Performs comprehensive preflight validation of Bicep deployments to Azure, including template syn... \| This skill validates Bicep deployments before execution, supporting both Azure CLI (`az`) and Azu... |
| [azure-devops-cli](.github/skills/azure-devops-cli/SKILL.md) | Manage Azure DevOps resources via CLI including projects, repos, pipelines, builds, pull requests, ... \| This Skill helps manage Azure DevOps resources using the Azure CLI with Azure DevOps extension. |
| [azure-resource-visualizer](.github/skills/azure-resource-visualizer/SKILL.md) | Analyze Azure resource groups and generate detailed Mermaid architecture diagrams showing the rel... \| A user may ask for help understanding how individual resources fit together, or to create a diagr... |
| [azure-role-selector](.github/skills/azure-role-selector/SKILL.md) | When user is asking for guidance for which role to assign to an identity given desired permissions, this agent helps them understand the role that will meet the requirements with least privilege ac... |
| [azure-static-web-apps](.github/skills/azure-static-web-apps/SKILL.md) | Helps create, configure, and deploy Azure Static Web Apps using the SWA CLI. \| npm install -D @azure/static-web-apps-cli |
| [breakdown-plan](.github/skills/breakdown-plan/SKILL.md) | Issue Planning and Automation prompt that generates comprehensive project plans with Epic > Feature > Story/Enabler > Test hierarchy, dependencies, priorities, and automated tracking. |
| [create-github-action-workflow-specification](.github/skills/create-github-action-workflow-specification/SKILL.md) | Create a formal specification for an existing GitHub Actions CI/CD workflow, optimized for AI consum... \| Create a comprehensive specification for the GitHub Actions workflow: `${input:WorkflowFile}`. |
| [create-github-issue-feature-from-specification](.github/skills/create-github-issue-feature-from-specification/SKILL.md) | Create GitHub Issue for feature request from specification file using feature_request.yml template. \| Create GitHub Issue for the specification at `${file}`. |
| [create-github-issues-feature-from-implementation-plan](.github/skills/create-github-issues-feature-from-implementation-plan/SKILL.md) | Create GitHub Issues from implementation plan phases using feature_request.yml or chore_request.yml templates. \| Create GitHub Issues for the implementation plan at `${file}`. |
| [create-github-issues-for-unmet-specification-requirements](.github/skills/create-github-issues-for-unmet-specification-requirements/SKILL.md) | Create GitHub Issues for unimplemented requirements from specification files using feature_request.yml templ... \| Create GitHub Issues for unimplemented requirements in the specification at `${file}`. |
| [create-github-pull-request-from-specification](.github/skills/create-github-pull-request-from-specification/SKILL.md) | Create GitHub Pull Request for feature request from specification file using pull_request_templat... \| Create GitHub Pull Request for the specification at `${workspaceFolder}/.github/pull_request_temp... |
| [csharp-async](.github/skills/csharp-async/SKILL.md) | Get best practices for C# async programming \| Your goal is to help me follow best practices for asynchronous programming in C#. |
| [csharp-docs](.github/skills/csharp-docs/SKILL.md) | Ensure that C# types are documented with XML comments and follow best practices for documentation. \| Public members should be documented with XML comments. - It is encouraged to document internal m... |
| [csharp-mstest](.github/skills/csharp-mstest/SKILL.md) | Get best practices for MSTest 3.x/4.x unit testing, including modern assertion APIs and data-driv... \| Your goal is to help me write effective unit tests with modern MSTest, using current APIs and bes... |
| [csharp-nunit](.github/skills/csharp-nunit/SKILL.md) | Get best practices for NUnit unit testing, including data-driven tests \| Your goal is to help me write effective unit tests with NUnit, covering both standard and data-driven testing approaches. |
| [csharp-tunit](.github/skills/csharp-tunit/SKILL.md) | Get best practices for TUnit unit testing, including data-driven tests \| Your goal is to help me write effective unit tests with TUnit, covering both standard and data-driven testing approaches. |
| [csharp-xunit](.github/skills/csharp-xunit/SKILL.md) | Get best practices for XUnit unit testing, including data-driven tests \| Your goal is to help me write effective unit tests with XUnit, covering both standard and data-driven testing approaches. |
| [dotnet-best-practices](.github/skills/dotnet-best-practices/SKILL.md) | Ensure .NET/C# code meets best practices for the solution/project. \| Your task is to ensure .NET/C# code in ${selection} meets the best practices specific to this solution/project. This includes: |
| [dotnet-design-pattern-review](.github/skills/dotnet-design-pattern-review/SKILL.md) | Review the C#/.NET code for design pattern implementation and suggest improvements. \| Review the C#/.NET code in ${selection} for design pattern implementation and suggest improvements for the solu... |
| [dotnet-upgrade](.github/skills/dotnet-upgrade/SKILL.md) | Ready-to-use prompts for comprehensive .NET framework upgrade analysis and execution \| name: "Project Classification Analysis" prompt: "Identify all projects in the solution and classify them by ty... |
| [ef-core](.github/skills/ef-core/SKILL.md) | Get best practices for Entity Framework Core \| Your goal is to help me follow best practices when working with Entity Framework Core. |
| [gh-cli](.github/skills/gh-cli/SKILL.md) | GitHub CLI (gh) comprehensive reference for repositories, issues, pull requests, Actions, projects... \| Comprehensive reference for GitHub CLI (gh) - work seamlessly with GitHub from the command line. |
| [git-commit](.github/skills/git-commit/SKILL.md) | Execute git commit with conventional commit message analysis, intelligent staging, and message generation. |
| [git-flow-branch-creator](.github/skills/git-flow-branch-creator/SKILL.md) | Intelligent Git Flow branch creator that analyzes git status/diff and creates appropriate branches following the nvie Git Flow branching model. |
| [github-issues](.github/skills/github-issues/SKILL.md) | Create, update, and manage GitHub issues using MCP tools. \| Manage GitHub issues using the `@modelcontextprotocol/server-github` MCP server. |
| [microsoft-code-reference](.github/skills/microsoft-code-reference/SKILL.md) | Look up Microsoft API references, find working code samples, and verify SDK code is correct. |
| [microsoft-docs](.github/skills/microsoft-docs/SKILL.md) | Query official Microsoft documentation to find concepts, tutorials, and code examples across Azur... \| Research skill for the Microsoft technology ecosystem. Covers learn.microsoft.com and documentati... |
| [nuget-manager](.github/skills/nuget-manager/SKILL.md) | Manage NuGet packages in .NET projects/solutions. |
| [sql-code-review](.github/skills/sql-code-review/SKILL.md) | Universal SQL code review assistant that performs comprehensive security, maintainability, and co... \| Perform a thorough SQL code review of ${selection} (or entire project if no selection) focusing o... |
| [sql-optimization](.github/skills/sql-optimization/SKILL.md) | Universal SQL performance optimization assistant for comprehensive query tuning, indexing strateg... \| Expert SQL performance optimization for ${selection} (or entire project if no selection). Focus o... |
| [web-design-reviewer](.github/skills/web-design-reviewer/SKILL.md) | This skill enables visual inspection of websites running locally or remotely to identify and fix ... \| This skill enables visual inspection and validation of website design quality, identifying and fi... |
| [webapp-testing](.github/skills/webapp-testing/SKILL.md) | Toolkit for interacting with and testing local web applications using Playwright. \| This skill enables comprehensive testing and debugging of local web applications using Playwright automation. |

<!-- skill-ninja-END -->
