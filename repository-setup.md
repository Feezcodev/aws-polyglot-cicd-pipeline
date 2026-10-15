
# CodeCommit & Repository Setup Documentation

## 1. Overview

This document describes the repository configuration, Git remotes, branching strategy, and CI/CD pipeline trigger workflow for the AWS Polyglot CI/CD Automation Pipeline.

## 2. Repository Details

### AWS CodeCommit

Repository: `aws-devops-ci-repo`

Clone URL:

```text
https://git-codecommit.us-east-1.amazonaws.com/v1/repos/aws-devops-ci-repo
```

### GitHub

Repository: `aws-polyglot-cicd-pipeline`

Repository URL: [https://github.com/Feezcodev/aws-polyglot-cicd-pipeline](https://github.com/Feezcodev/aws-polyglot-cicd-pipeline)

Confirm that both repositories exist and match the remotes configured in your local Git repository.

## 3. AWS CLI and Git Configuration

Verify the active AWS identity:

```bash
aws sts get-caller-identity
```

Configure the AWS CodeCommit credential helper:

```bash
git config --global credential.helper \
'!aws codecommit credential-helper $@'

git config --global credential.UseHttpPath true
```

Check the configured Git remotes:

```bash
git remote -v
```

Add the remotes if they do not already exist:

```bash
git remote add codecommit \
https://git-codecommit.us-east-1.amazonaws.com/v1/repos/aws-devops-ci-repo

git remote add github \
https://github.com/Feezcodev/aws-polyglot-cicd-pipeline.git
```

Use the remote names already configured in your repository where applicable.

## 4. Branching Strategy

The project uses a feature branch workflow to organize changes and support controlled integration.

### Main Branch

- `main` contains stable, reviewed changes.
- Direct pushes should be restricted where branch protection is supported and configured.
- Changes are merged after the required reviews and checks pass.

### Feature Branches

Feature branches are created for new features, fixes, and documentation updates.

Example:

```bash
git checkout -b feature/update-pipeline-docs
```

### Pull Request Workflow

1. Create a feature branch.
2. Make and commit the changes.
3. Push the branch to the remote repository.
4. Open a pull request targeting `main`.
5. Review the changes and run required validation checks.
6. Merge the pull request after approval.

Example commands:

```bash
git add .
git commit -m "docs: update repository setup"
git push -u github feature/update-pipeline-docs
```

Repository branch protection and required approvals must be configured separately in the repository settings.

## 5. CI/CD Pipeline Trigger

The AWS CodePipeline workflow is designed to retrieve source code and execute the configured build process when the relevant source trigger fires.

Expected workflow:

1. A developer pushes a commit to the configured source branch.
2. The source stage retrieves the repository revision.
3. CodeBuild executes the commands in `buildspec.yml`.
4. Build artifacts are stored in the configured artifact location.
5. The Deploy stage publishes the configured output to its deployment destination, if enabled.

For AWS CodeCommit, configure a supported source trigger or Amazon EventBridge rule as appropriate.

For GitHub, configure the corresponding GitHub source connection and trigger if GitHub is the pipeline source.

**Important:** A GitHub pull request merge does not automatically trigger a CodeCommit-based pipeline unless the repositories are synchronized and the configured trigger responds to the resulting CodeCommit update.

## 6. Verification Checklist

- [ ] CodeCommit repository URL verified.
- [ ] GitHub repository URL verified.
- [ ] AWS CLI identity confirmed.
- [ ] Git remotes configured correctly.
- [ ] Feature branch workflow tested.
- [ ] Pull request workflow verified.
- [ ] Pipeline source repository and branch confirmed.
- [ ] Pipeline triggers tested successfully.

## Author

**Feezco Touch**

GitHub: [@Feezcodev](https://github.com/Feezcodev)

*One project. One skill. One opportunity at a time.* 🚀
