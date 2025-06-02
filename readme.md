# 🧠 SonarQube Setup Guide for React Projects

This guide helps you set up **SonarQube** locally and analyze a **React project** to detect bugs, code smells, security vulnerabilities, and maintainability issues.

---

## ✅ Prerequisites

Before you begin, make sure you have the following installed:

- ☕️ **Java 17+** – SonarQube requires Java 17 to run.
- 🧰 **SonarQube (Community Edition)** – The code quality platform.
- 🔍 **SonarScanner CLI** – CLI tool to analyze code.

---

## 🧩 Step 1: Install SonarQube Locally

### 📥 1.1 Download SonarQube

- Go to [SonarQube Downloads](https://www.sonarsource.com/products/sonarqube/downloads/)
- Download the **Community Edition (latest LTS version – e.g., `10.4.1`)**

### 📦 1.2 Extract and Run SonarQube

```bash
# Unzip the downloaded file
unzip sonarqube-*.zip
cd sonarqube-*/bin/linux-x86-64

# Start the SonarQube server
./sonar.sh start
```
### 🌐 Access SonarQube

* Visit: [http://localhost:9000](http://localhost:9000)
* Default login:

  * Username: `admin`
  * Password: `admin`
* ⚠️ You'll be prompted to change the default password after logging in.
---

## 🧪 Step 2: Install SonarScanner CLI

### 📥 2.1 Download SonarScanner

* Go to [SonarScanner Docs](https://docs.sonarsource.com/sonarqube/latest/analyzing-source-code/scanners/sonarscanner/)
* Download the **latest CLI version** (e.g., `sonar-scanner-cli-5.x.x`)

### ⚙️ 2.2 Extract & Add to PATH

```bash
# Unzip the scanner
unzip sonar-scanner-cli-*.zip
sudo mv sonar-scanner-* /opt/sonar-scanner

# Add to your PATH permanently (choose one depending on your shell)
echo 'export PATH=$PATH:/opt/sonar-scanner/bin' >> ~/.bashrc
source ~/.bashrc

# OR for ZSH users
echo 'export PATH=$PATH:/opt/sonar-scanner/bin' >> ~/.zshrc
source ~/.zshrc

# Verify installation
sonar-scanner --version
```

## ⚙️ Step 3: Setup React Project for SonarQube

### 📁 3.1 Navigate to Your Project

```bash
cd ~/path-to-your-react-project
```

### 📄 3.2 Create `sonar-project.properties`

In your project root, create the file:

```bash
touch sonar-project.properties
```

Add the following content:

```properties
sonar.projectKey=react-app
sonar.projectName=React App
sonar.projectVersion=1.0

# Source directory
sonar.sources=src

# Language
sonar.language=js

# Exclude test files and node_modules
sonar.exclusions=**/node_modules/**,**/*.test.js,**/__tests__/**

# Encoding
sonar.sourceEncoding=UTF-8

# SonarQube server
sonar.host.url=http://localhost:9000

# If you're using a token:
# sonar.login=your-token-here
```

### 🔐 Generate Authentication Token (Optional)

* Go to: **My Account > Security > Generate Token**
* Replace `sonar.login=your-token-here` in the file or use it in CLI

---

## ▶️ Step 4: Run SonarScanner

### Basic Scan

```bash
sonar-scanner
```

### If Using a Token (and not added in the `.properties` file):

```bash
sonar-scanner -Dsonar.login=your-generated-token
```

---

## 📊 View Your Report

* Visit: [http://localhost:9000](http://localhost:9000)
* Navigate to your project dashboard
## You'll see detailed insights: (🧠 SonarQube Analysis Metrics)
- 🚨 Code Smells  
- 🐞 Bugs  
- 🔐 Vulnerabilities  
- 📏 Maintainability  
- 📊 Coverage (optional)  
- 🔁 Duplications

---

## 🧪 (Optional) Add Jest Test Coverage

Run tests with coverage enabled:

```bash
npm test -- --coverage
```

Update your `sonar-project.properties`:

```properties
# Add Jest coverage report path
sonar.javascript.lcov.reportPaths=coverage/lcov.info
```

Then rerun:

```bash
sonar-scanner -Dsonar.login=your-generated-token
```

---

## 🏁 Done!

You've successfully:

* Installed and ran SonarQube locally 🖥️
* Configured a React project for analysis ⚙️
* Generated a code quality report 📊

---

## 🙌 Bonus

You can integrate this into a CI/CD pipeline later (GitHub Actions, GitLab CI, etc.) for continuous analysis.

Happy coding 💻 and clean coding! 🧼
