# JMeter Installation & Environment Setup

<p align="center">

  <img src="https://jmeter.apache.org/images/logo.svg" alt="Apache JMeter" width="180"/>

</p>

<p align="center">

<strong>A practical setup guide for QA Engineers who want to install and configure Apache JMeter for performance testing.
</strong>

</p>

---

## 📋 Prerequisites

Before installing JMeter, make sure you have:

- Java JDK
- Apache JMeter
- Git
- Terminal / Command Prompt
- Basic command-line knowledge

> **Recommended Java:** Use a supported LTS JDK. This project currently uses Eclipse Temurin JDK 17.

---

# 1. ☕ Install Java

JMeter requires Java to run.

## macOS

### Using Homebrew

Check whether Homebrew is installed:

```bash
brew --version
```

Install Eclipse Temurin JDK 17:

```bash
brew install --cask temurin@17
```

Verify installed Java versions:

```bash
/usr/libexec/java_home -V
```

Find Java 17:

```bash
/usr/libexec/java_home -v 17
```

Verify Java:

```bash
java -version
```

or:

```bash
java --version
```

---

## Configure `JAVA_HOME`

For the current terminal session:

```bash
export JAVA_HOME=$(/usr/libexec/java_home -v 17)
export PATH="$JAVA_HOME/bin:$PATH"
```

Verify:

```bash
echo $JAVA_HOME
```

Expected format:

```text
/Library/Java/JavaVirtualMachines/temurin-17.jdk/Contents/Home
```

### Make Java 17 permanent

For Zsh:

```bash
echo 'export JAVA_HOME=$(/usr/libexec/java_home -v 17)' >> ~/.zshrc
echo 'export PATH="$JAVA_HOME/bin:$PATH"' >> ~/.zshrc
```

Reload the shell:

```bash
source ~/.zshrc
```

Verify:

```bash
java -version
echo $JAVA_HOME
```

> If you already have a customized `.zshrc`, review the file before adding configuration to avoid duplicate entries.

---

# 2. 🚀 Install Apache JMeter

Download Apache JMeter from the official website:

https://jmeter.apache.org/download_jmeter.cgi

JMeter is distributed as an archive.

Extract it to a convenient location.

Example:

```text
~/Applications/apache-jmeter-5.6.3/
```

---

## Add JMeter to PATH

For example:

```bash
export JMETER_HOME="$HOME/Applications/apache-jmeter-5.6.3"
export PATH="$JMETER_HOME/bin:$PATH"
```

Verify:

```bash
jmeter --version
```

Expected:

```text
Apache JMeter 5.6.3
```

> The version shown above is the version used by the current project environment. Newer JMeter releases may be available.

---

# 3. 🪟 Windows Installation

## Install Java

Install a supported JDK.

Verify from Command Prompt or PowerShell:

```powershell
java -version
```

Check Java location:

```powershell
where.exe java
```

## Install JMeter

1. Download the JMeter ZIP archive.
2. Extract it.
3. Open the `bin` directory.
4. Run:

```text
jmeter.bat
```

Verify from Command Prompt:

```cmd
jmeter --version
```

---

# 4. 🐧 Linux Installation

Verify Java:

```bash
java -version
```

Set Java:

```bash
export JAVA_HOME=/path/to/jdk
export PATH="$JAVA_HOME/bin:$PATH"
```

Download and extract JMeter:

```bash
tar -xzf apache-jmeter-*.tgz
```

Move it if desired:

```bash
sudo mv apache-jmeter-* /opt/jmeter
```

Configure:

```bash
export JMETER_HOME=/opt/jmeter
export PATH="$JMETER_HOME/bin:$PATH"
```

Verify:

```bash
jmeter --version
```

---

# 5. 🔧 Git Installation

Git is recommended for managing JMeter test plans and documentation.

## macOS

Check Git:

```bash
git --version
```

If Git is not installed:

```bash
brew install git
```

Verify:

```bash
git --version
```

## Windows

Verify:

```powershell
git --version
```

Install Git if required from:

https://git-scm.com/

## Linux

Debian/Ubuntu:

```bash
sudo apt update
sudo apt install git
```

Verify:

```bash
git --version
```

---

# 6. 🧪 Complete Environment Verification

Run:

```bash
java -version
```

```bash
echo $JAVA_HOME
```

```bash
jmeter --version
```

```bash
git --version
```

A working environment should provide:

```text
Java
JAVA_HOME
Apache JMeter
Git
```

---

# 7. 🖥️ Launch JMeter GUI

Start JMeter:

```bash
jmeter
```

On macOS/Linux:

```bash
./jmeter
```

On Windows:

```cmd
jmeter.bat
```

The JMeter GUI should open.

---

# 8. ⚡ JMeter CLI / Non-GUI Mode

For actual performance testing, JMeter tests should normally be executed in **non-GUI mode**.

Basic command:

```bash
jmeter -n -t test-plan.jmx
```

Save results:

```bash
jmeter -n -t test-plan.jmx -l results.jtl
```

Generate an HTML report:

```bash
jmeter -n \
  -t test-plan.jmx \
  -l results.jtl \
  -e \
  -o html-report
```

### Common CLI options

| Option         | Purpose                      |
| -------------- | ---------------------------- |
| `-n`           | Non-GUI mode                 |
| `-t`           | Test plan (`.jmx`)           |
| `-l`           | Results file (`.jtl`)        |
| `-e`           | Generate HTML report         |
| `-o`           | HTML report output directory |
| `-j`           | JMeter log file              |
| `-Jname=value` | Define a JMeter property     |

Example:

```bash
jmeter -n \
  -t api-test.jmx \
  -l results.jtl \
  -j jmeter.log
```

---

# 9. 🔍 Useful Environment Commands

## Find Java

macOS/Linux:

```bash
which java
```

macOS:

```bash
/usr/libexec/java_home -V
```

Windows:

```powershell
where.exe java
```

## Find JMeter

macOS/Linux:

```bash
which jmeter
```

Windows:

```cmd
where jmeter
```

## Check PATH

macOS/Linux:

```bash
echo $PATH
```

Windows PowerShell:

```powershell
$env:Path
```

## Check JAVA_HOME

macOS/Linux:

```bash
echo $JAVA_HOME
```

Windows PowerShell:

```powershell
$env:JAVA_HOME
```

---

# 10. ⚠️ Common Issues

## `java: command not found`

Java is not installed or is not available in `PATH`.

Check:

```bash
java -version
```

macOS:

```bash
/usr/libexec/java_home -V
```

---

## `jmeter: command not found`

JMeter's `bin` directory is not in `PATH`.

Check:

```bash
which jmeter
```

Set:

```bash
export JMETER_HOME="/path/to/apache-jmeter"
export PATH="$JMETER_HOME/bin:$PATH"
```

---

## JMeter starts but shows warnings

JMeter or Java may display non-blocking warnings during startup.

First verify whether JMeter actually starts:

```bash
jmeter --version
```

If the version is displayed successfully, investigate warnings separately rather than assuming the installation failed.

---

## GUI performance problems

The JMeter GUI is intended primarily for:

- Creating test plans
- Debugging
- Learning
- Small-scale validation

For actual load tests, prefer:

```bash
jmeter -n -t test-plan.jmx
```

---

# 11. 🔐 Security Notes

Never commit the following to Git:

```text
Passwords
API keys
Access tokens
Production credentials
Private certificates
Real user data
```

Use:

```text
.env.example
```

or sanitized test data instead.

Also avoid putting sensitive information directly inside `.jmx` files.

---

# 12. 📌 Project Environment

The current environment used to develop this repository:

| Component     | Version                   |
| ------------- | ------------------------- |
| OS            | macOS Intel (x86_64)      |
| Java          | Eclipse Temurin 17.0.20.1 |
| Apache JMeter | 5.6.3                     |
| Git           | 2.43.0                    |
| Shell         | Zsh                       |

Verify the environment with:

```bash
uname -m
java -version
echo $JAVA_HOME
jmeter --version
git --version
```

---

# 13. ✅ Installation Checklist

```text
☐ Java JDK installed
☐ JAVA_HOME configured
☐ Java version verified
☐ Apache JMeter installed
☐ JMeter added to PATH
☐ JMeter version verified
☐ Git installed
☐ Git version verified
☐ JMeter GUI launches
☐ JMeter CLI works
```

---

# 🚀 Next Step

Environment setup is complete.

Continue with:

**01 — Performance Testing Foundations & JMeter Architecture**

The next section introduces the core concepts behind performance testing before building the first JMeter Test Plan.
