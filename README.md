# Android CI/CD Pipelines

This repository contains a sample project demonstrating pipelines for **Continuous Integration (CI)** and **Continuous Delivery (CD)** in Android using **Fastlane** and **GitHub Actions**.

---

## Pipelines Overview

As shown in the picture below, we have 4 pipelines, and their details are explained below.  
![Pipeline Diagram](./android-ci-cd.png)

### 1. **Pull Requests**
- **Trigger Event**: Triggered on any pull request created on any branch.  
- **Jobs**:  
  - **`build`**: Builds the project.  
  - **`static_code_analysis`**: Checks code quality using Android Lint and KtLint.  
  - **`unit_tests`**: Runs all unit tests.  

### 2. **Deploy Debug**
- **Trigger Event**: Triggered on push to the `develop` branch.  
- **Jobs**:  
  - **`build`**: Builds the project.  
  - **`deploy`**: Deploys the debug build using Fastlane.  

### 3. **Deploy Staging**
- **Trigger Event**: Triggered on push to the `release` branch.  
- **Jobs**:  
  - **`build`**: Builds the staging version of the project and signs the APK.  
  - **`ui_tests`**: Runs UI tests implemented in the project using the Maestro UI testing framework.  
  - **`deploy`**: Deploys the signed APK to Firebase App Distribution.  

### 4. **Deploy Release**
- **Trigger Event**: Triggered on push to the `main` branch (when the staging version is tested and ready for production).  
- **Steps**:  
  - Builds a signed Android App Bundle (AAB).  
  - Deploys the AAB to the Google Play Console using Fastlane.  

---

## App Version Code

The app version code is calculated as follows:  
1. Multiply the **major part** of the app version name (`major`, `minor`, `patch`) by **10,000**.  
2. Add the **build number** of the specific pipeline to the result.  

This ensures a unique and incrementing version code for each build.
