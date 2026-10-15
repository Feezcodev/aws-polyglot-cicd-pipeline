# Polyglot CI/CD Automation Pipeline with AWS DevOps Services

## 📌 Project Overview
This project establishes an automated Continuous Integration (CI) pipeline using AWS DevOps native tools to automatically compile, test, and build a polyglot application codebase (Go, Node.js, and Python) upon source control updates.

---

## 🏗️ Architecture & Infrastructure

The pipeline follows a serverless CI workflow:

1. **AWS CodeCommit (`aws-devops-ci-repo`)**: Serves as the central Git repository hosting application code and the `buildspec.yml` build definitions.
2. **AWS CodeBuild (`aws-devops-ci-project`)**: Runs the multi-runtime compilation and execution steps defined inside `buildspec.yml`.
3. **AWS CodePipeline (`aws-devops-pipeline`)**: Automates stage transitions and triggers build actions upon changes pushed to the `main` branch via EventBridge.

---

## 🔐 IAM Service Roles & Permissions

To adhere to the principle of least privilege, two dedicated service roles were configured for cross-service authorization:

### 1. CodePipeline Service Role (`code-pipeline-service-role`)
- **Purpose**: Grants AWS CodePipeline permission to monitor CodeCommit repositories and invoke CodeBuild actions.
- **Attached Policies**:
  * AWS CodeCommit read/pull permissions (`codecommit:GetBranch`, `codecommit:GetCommit`, `codecommit:UploadArchive`, `codecommit:GetUploadArchiveStatus`).
  * AWS CodeBuild execution trigger permissions (`codebuild:BatchGetBuilds`, `codebuild:StartBuild`).
  * Amazon S3 permissions for managing pipeline build artifacts (`s3:GetObject`, `s3:PutObject`).

### 2. CodeBuild Service Role (`codebuild-aws-devops-ci-project-service-role`)
- **Purpose**: Allows CodeBuild worker instances to pull source code, output build logs to CloudWatch, and write generated binaries back to S3.
- **Attached Policies**:
  * Amazon CloudWatch Logs access (`logs:CreateLogGroup`, `logs:CreateLogStream`, `logs:PutLogEvents`).
  * S3 Artifact bucket write access (`s3:PutObject`, `s3:GetObject`).
  * AWS CodeCommit fetch access.

---

## 🛠️ Build & Runtime Configuration (`buildspec.yml`)

The build specification configures the runtime environment for Go compilation along with Node.js and Python execution:

```yaml
version: 0.2

phases:
  install:
    runtime-versions:
      golang: 1.x
      nodejs: 18
      python: 3.x
  build:
    commands:
      - echo "Starting build process..."
      - go version
      - node --version
      - python3 --version
      - go build -o app main.go
      - ./app
artifacts:
  files:
    - app

    ## 📸 Verification & Evidence Screenshots

The following screenshots validate the successful execution and deployment pipeline:

1. **Pipeline Execution Success**: `Screenshots/01_codepipeline_success.png` — Shows the CodePipeline stage transitions in green "Succeeded" status.
2. **Build Logs**: `Screenshots/02_codebuild_logs_success.png` — Details the multi-runtime compilation output in CodeBuild.
3. **Repository Files**: `Screenshots/03_codecommit_repository_files.png` — Verifies the CodeCommit repository content.
4. **S3 Build Artifacts**: `Screenshots/04_s3_artifact_success.png` — Confirms the successful generation and storage of build output archives in the S3 artifact bucket.