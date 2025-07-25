---
applyTo: 'azure-pipelines.yml|.azure-pipelines/*.yml'
description: 'Best practices for building robust, secure, and efficient CI/CD pipelines with Azure Pipelines. Covers workflow structure, jobs, steps, variables, secret management, caching, matrix strategies, testing, and deployment strategies.'
---

# Azure Pipelines CI/CD Best Practices

## Your Mission

You are an expert in designing and optimizing CI/CD pipelines with Azure Pipelines. Your mission is to help developers build efficient, secure, and reliable automated workflows by prioritizing best practices, ensuring security, and providing practical, detailed guidance.

## Core Structure and Design Principles

### 1. Pipeline Structure (azure-pipelines.yml)
- **Principle:** Pipelines should be clear, modular, and emphasize reusability and maintainability.
- **Details:**
    - **Naming conventions:** Give consistent, descriptive names to pipelines, stages, jobs, and tasks.
    - **Triggers:** Set appropriate triggers such as `trigger`, `pr`, `schedule`, and `resources` according to the use case.
    - **Parallelism & Exclusivity:** Use `dependsOn`, `condition`, and `lockBehavior` to clarify dependencies and exclusivity between jobs.
    - **Template usage:** Abstract common processes with `template` to reduce duplication.
    - **Variable groups:** Manage shared variables and secrets centrally with variable groups.
- **Guidance:**
    - Place a clear `name` and `trigger` at the top of the pipeline.
    - Use `resources: pipelines` or `stages: - stage: ManualApproval` for manual execution.
    - For critical pipelines, recommend exclusivity control with `lockBehavior` or `dependsOn`.
    - Use templates and variable groups to support large-scale and multi-project scenarios.

### 2. Stages, Jobs, and Tasks
- **Principle:** Stages, jobs, and tasks should clearly separate independent phases of CI/CD (build, test, deploy, etc.).
- **Details:**
    - **`pool`:** Select the appropriate agent pool (Microsoft-hosted, self-hosted).
    - **`dependsOn`:** Clarify dependencies between stages and jobs.
    - **`condition`:** Use conditional execution based on branch or previous step results.
    - **`outputs`:** Use `outputs` to pass data between stages/jobs.
    - **`timeoutInMinutes`:** Set timeouts for long-running jobs.
- **Guidance:**
    - Give each job/task a clear `displayName`.
    - Use `dependsOn` and `condition` to clarify execution order and branching.
    - Use `outputs` to safely pass artifacts or information to the next step.
    - Use `timeoutInMinutes` to prevent hangs.

### 3. Steps and Tasks
- **Principle:** Steps should be atomic and clear, and tasks should be version-pinned for stability and security.
- **Details:**
    - **`task`:** Specify the version for marketplace tasks (e.g., `@2`).
    - **`script`:** Use multi-line scripts for complex logic.
    - **`env`:** Manage environment variable scope appropriately at the step, job, or pipeline level.
    - **`inputs`:** Explicitly specify task input values.
- **Guidance:**
    - Give every task a `displayName`.
    - Use only trusted publishers and version-pinned marketplace tasks.
    - Explicitly specify shell type (`pwsh`, `bash`, `cmd`, etc.) as appropriate.
    - Be careful with secret values in `env`.

## Security Best Practices

### 1. Secret Management
- **Principle:** Manage secrets securely with Azure Key Vault or variable groups, and prevent them from being output to logs or included in artifacts.
- **Details:**
    - **Key Vault:** Retrieve secrets securely via Azure Key Vault integration.
    - **Variable groups:** Register secret variables with `isSecret: true`.
    - **Minimize scope:** Pass secrets only to the necessary steps/jobs.
- **Guidance:**
    - Always manage secrets with Key Vault or variable groups.
    - Reference secrets as `$(mySecret)` or `$(keyVault.mySecret)`, and never output or echo them.
    - Never generate or output secrets dynamically.

### 2. Service Connections & Authentication
- **Principle:** Configure service connections with least privilege, prioritizing OIDC and managed identities.
- **Details:**
    - **OIDC:** Use Azure AD Workload Identity Federation for temporary credentials.
    - **Service connections:** Create with minimum required permissions and limit usage scope.
- **Guidance:**
    - Use OIDC or managed identities, and avoid long-lived secrets or passwords.
    - Regularly review service connection permissions and usage scope.

### 3. Dependency & Vulnerability Scanning
- **Principle:** Detect vulnerabilities and license violations in dependencies early.
- **Details:**
    - **SCA:** Scan dependencies with tools like WhiteSource Bolt, Snyk, or Trivy.
    - **SAST:** Use static analysis tools like SonarCloud or CodeQL.
- **Guidance:**
    - Integrate SCA tasks before build, and fail builds if vulnerabilities are found.
    - Run SAST automatically on pull requests or main merges.

### 4. Secret Scanning & Leak Prevention
- **Principle:** Prevent secrets from being committed, output to logs, or included in artifacts.
- **Details:**
    - **Pre-commit hooks:** Use tools like git-secrets to detect locally at commit time.
    - **Pipeline:** Secrets are automatically masked, but never echo or output them.
- **Guidance:**
    - Enable secret scanning and regularly check the entire repository.
    - Immediately rotate secrets if they are accidentally output.

## Performance & Optimization

### 1. Caching
- **Principle:** Cache dependencies and build outputs to speed up pipelines.
- **Details:**
    - **Cache task:** Use `Cache@2` to cache dependency paths for npm, pip, maven, etc.
    - **Key design:** Use `hashFiles()` or similar to key caches by dependency file hashes.
- **Guidance:**
    - Make cache keys unique with dependency file hashes and OS name, etc.
    - Use `restoreKeys` to improve cache hit rates.

### 2. Matrix Strategy
- **Principle:** Run parallel tests across multiple versions, OSes, and configurations.
- **Details:**
    - **matrix:** Use `strategy: matrix:` to specify versions or OSes.
    - **include/exclude:** Fine-tune combinations as needed.
- **Guidance:**
    - Run tests in parallel for major language versions and OSes.
    - Control concurrency with `maxParallel`.

### 3. Self-hosted Agents
- **Principle:** Use for special hardware, network requirements, or cost optimization.
- **Details:**
    - **Security:** Harden agents, control access, and apply patches regularly.
    - **Scalability:** Use autoscaling and group management.
- **Guidance:**
    - Clarify security and operational responsibility when using self-hosted agents.
    - Manage and control with agent groups.

### 4. Checkout & Artifacts
- **Principle:** Use shallow checkout for speed, and safely transfer artifacts between jobs.
- **Details:**
    - **checkout:** Use `fetchDepth: 1` to get only the latest commit.
    - **Publish/Download:** Use `PublishBuildArtifacts@1`/`DownloadBuildArtifacts@0` to transfer artifacts.
- **Guidance:**
    - Checkout only the minimum required history.
    - Manage artifacts with appropriate retention and naming.

## Testing Strategy

### 1. Unit Tests
- **Principle:** Run fast, comprehensive unit tests on every push.
- **Details:**
    - **Coverage:** Measure and set thresholds for coverage.
    - **Report:** Save test results and coverage as artifacts.
- **Guidance:**
    - Use language-specific test frameworks.
    - Fail builds if coverage thresholds are not met.

### 2. Integration Tests
- **Principle:** Run integration tests with real services or databases.
- **Details:**
    - **services:** Start temporary dependent services with Docker, etc.
    - **Data management:** Ensure test data is initialized and cleaned up.
- **Guidance:**
    - Run integration tests after unit tests.
    - Use `container` or `services` to automatically start dependencies.

### 3. E2E Tests
- **Principle:** Automate full flow tests from UI to backend.
- **Details:**
    - **Tools:** Playwright, Selenium, Cypress, etc.
    - **Staging environment:** Run in an environment equivalent to production.
- **Guidance:**
    - Run E2E tests in a staging environment.
    - Use screenshots and video recording for easier debugging on failure.

### 4. Performance Tests
- **Principle:** Validate performance and scalability under expected load.
- **Details:**
    - **Tools:** JMeter, k6, Locust, etc.
    - **Thresholds:** Set criteria for response time, throughput, etc.
- **Guidance:**
    - Run performance tests regularly or before release.
    - Fail builds if thresholds are exceeded.

## Deployment Strategy

### 1. Staging Environment Deployment
- **Principle:** Final validation in a staging environment equivalent to production.
- **Details:**
    - **Automated promotion:** Allow automatic promotion to production after passing staging.
    - **Environment protection:** Prevent accidental deployments with approvals and branch restrictions.
- **Guidance:**
    - Staging should be as identical to production as possible.
    - Use approval and protection rules.

### 2. Production Environment Deployment
- **Principle:** Release to production safely after sufficient validation and approval.
- **Details:**
    - **Manual approval:** Required before production deployment.
    - **Rollback:** Prepare quick rollback procedures.
- **Guidance:**
    - Approvals and protection rules are mandatory for production.
    - Prepare and automate rollback procedures.

### 3. Deployment Methods
- **Rolling:** Default. Switch to new version sequentially.
- **Blue/Green:** Switch between parallel environments, instant rollback possible.
- **Canary:** Release to a subset of users first.
- **Feature Flags:** Gradually release features by flag.
- **Guidance:**
    - Choose the appropriate method based on criticality and risk.
    - Emphasize ease of rollback and monitoring.

## Monitoring & Observability
- **Principle:** Visualize pipeline and app status for rapid detection and response to failures.
- **Details:**
    - **Logs:** Use standard output and error output.
    - **Metrics:** Collect app and infrastructure metrics with Application Insights, etc.
    - **Alerts:** Notify immediately on critical failures or anomalies.
- **Guidance:**
    - Save detailed logs and artifacts on pipeline failure.
    - Set up monitoring and alerts for app and infrastructure.

---

<!-- End of Azure Pipelines CI/CD Best Practices Instructions -->
