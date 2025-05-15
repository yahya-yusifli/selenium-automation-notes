# Jenkins Integration

This section explains how to integrate your Selenium + Java + TestNG Maven project with Jenkins for continuous integration and automated test execution.

---

## Jenkins Setup (Local)

1. **Install Jenkins**
   - On macOS:
     ```bash
     brew install jenkins-lts
     brew services start jenkins-lts
     ```
   - Access via: `http://localhost:8080`

2. **Initial Setup**
   - Use `initialAdminPassword` to unlock.
   - Choose: **Install suggested plugins**
   - Create an admin user.

---

##  Configure Maven Project in Jenkins

1. **Global Tool Configuration**
   - Go to: `Manage Jenkins` → `Global Tool Configuration`
   - Under **JDK**:
     - Name: `Java-21`
     - (Optional) Add path if Jenkins doesn’t auto-detect.
   - Under **Maven**:
     - Name: `Maven`
     - Install automatically or provide path.

2. **Create a New Job**
   - Click: `New Item` → Select **Freestyle project**
   - Enter project name (e.g., `Selenium-TestNG-Project`)
   - Choose: `Git` and provide repository URL or local path

3. **Build Configuration**
   - Under **Build** section → Click `Add build step` → `Invoke top-level Maven targets`
   - In Goals, enter:
     ```
     clean test
     ```

---

##  Running Tests

- When you click `Build Now`, Jenkins will:
  - Pull your Maven project
  - Run your TestNG tests
  - Display console output

---

##  Test Reports (Optional)

To generate readable reports:
1. Use **Surefire Plugin** or integrate **ExtentReports**
2. Add report plugin configuration in `pom.xml`
3. Jenkins can archive `.html` or `.xml` reports:
   - Go to `Post-build Actions` → `Publish HTML reports`

---

##  Tips

- Use **Poll SCM** for scheduled Git pulls: `H/15 * * * *`
- Use **Pipeline Projects** for advanced control (e.g., Jenkinsfile)
- Install plugins:
  - Git Plugin
  - HTML Publisher Plugin
  - Pipeline

---

##  Summary

| Feature              | Description                                      |
|----------------------|--------------------------------------------------|
| Jenkins Setup         | Local LTS setup via Homebrew                     |
| Build Type            | Freestyle or Pipeline                            |
| Trigger               | Manual, SCM polling, or post-commit hook         |
| Reports               | Surefire, ExtentReports, HTML reports            |
| Useful Plugins        | Git, HTML Publisher, Pipeline, TestNG Results    |
