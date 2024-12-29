# Software Management in RHEL 8

Red Hat Enterprise Linux (RHEL) 8 introduces robust tools for managing software. This document covers the key software management tools and utilities, including `rpm`, `yum`, and `dnf`.

## Table of Contents

1. **Package Management Tools Overview**
2. **Using `rpm` for Package Management**
3. **Managing Software with `yum`**
4. **Advanced Package Management with `dnf`**
5. **Software Repositories**
6. **Lab Work: Practical Examples**

---

## 1. Package Management Tools Overview

RHEL 8 primarily uses the `dnf` package manager, which builds on `yum` but offers significant improvements in speed and dependency management. The tools available are:

- **`rpm` (Red Hat Package Manager):** For low-level package management, including installing, verifying, and querying `.rpm` files.
- **`yum` (Yellowdog Updater, Modified):** High-level tool for dependency management and working with repositories. 
- **`dnf` (Dandified Yum):** A modern replacement for `yum`, designed for better performance and usability.

---

## 2. Using `rpm` for Package Management

### Common `rpm` Commands

| Command                          | Description                                      |
|----------------------------------|--------------------------------------------------|
| `rpm -ivh package.rpm`           | Install a package.                              |
| `rpm -Uvh package.rpm`           | Upgrade a package.                              |
| `rpm -e package`                 | Remove a package.                               |
| `rpm -q package`                 | Query if a package is installed.                |
| `rpm -qa`                        | List all installed packages.                    |
| `rpm -qc package`                | List configuration files of a package.          |
| `rpm -V package`                 | Verify the integrity of an installed package.   |

### Example: Installing an RPM Package

```bash
# Download a package
wget https://example.com/sample-package.rpm

# Install the package
rpm -ivh sample-package.rpm

# Verify the installation
rpm -q sample-package
```

---

## 3. Managing Software with `yum`

### Common `yum` Commands

| Command                         | Description                                      |
|---------------------------------|--------------------------------------------------|
| `yum install package`           | Install a package.                              |
| `yum update`                    | Update all packages.                            |
| `yum update package`            | Update a specific package.                      |
| `yum remove package`            | Remove a package.                               |
| `yum list`                      | List available packages.                        |
| `yum search keyword`            | Search for a package by keyword.                |
| `yum info package`              | Get detailed info about a package.              |

### Example: Installing a Package with `yum`

```bash
# Install the vim editor
sudo yum install vim

# Verify the installation
vim --version
```

---

## 4. Advanced Package Management with `dnf`

### Advantages of `dnf`
- Improved dependency management.
- Better performance and parallel downloads.
- Enhanced CLI usability with clear output.

### Common `dnf` Commands

| Command                          | Description                                      |
|----------------------------------|--------------------------------------------------|
| `dnf install package`            | Install a package.                              |
| `dnf update`                     | Update all packages.                            |
| `dnf remove package`             | Remove a package.                               |
| `dnf list`                       | List available packages.                        |
| `dnf search keyword`             | Search for a package by keyword.                |
| `dnf history`                    | View the history of transactions.               |

### Example: Upgrading the System with `dnf`

```bash
# Upgrade all packages
sudo dnf update -y

# Check for kernel updates
sudo dnf list kernel
```

---

## 5. Software Repositories

### Managing Repositories

- **Default Repositories:** Pre-configured in `/etc/yum.repos.d/`.
- **Adding a Repository:**

  ```bash
  sudo dnf config-manager --add-repo=https://repo.example.com/custom.repo
  ```

- **Enabling/Disabling Repositories:**

  ```bash
  # Enable a repository
  sudo dnf config-manager --set-enabled repo_name

  # Disable a repository
  sudo dnf config-manager --set-disabled repo_name
  ```

- **Viewing Enabled Repositories:**

  ```bash
  sudo dnf repolist
  ```

---

<details>
  <summary>### Lab 2: Managing Software - rpm </summary>

### Lab 1: Using `rpm` to Install and Verify Packages

1. **Download a Sample RPM Package:**
   ```bash
   wget https://mirror.stream.centos.org/10-stream/BaseOS/x86_64/os/Packages/tree-2.1.0-7.el10.x86_64.rpm
   ```

2. **Install the Package:**
   ```bash
   sudo rpm -ivh sample-package.rpm
   ```

3. **Verify the Installation:**
   ```bash
   rpm -q sample-package
   ```

4. **Check the Integrity of the Package:**
   ```bash
   rpm -V sample-package
   ```
</details>
---
<details>
  <summary>### Lab 2: Managing Software -yum </summary>


1. **Search for a Package:**
   ```bash
   yum search httpd
   ```

2. **Install Apache HTTP Server:**
   ```bash
   sudo yum install httpd -y
   ```

3. **Start and Enable the Service:**
   ```bash
   sudo systemctl start httpd
   sudo systemctl enable httpd
   ```

4. **Remove Apache HTTP Server:**
   ```bash
   sudo yum remove httpd -y
   ```
</details>
---

<details>
  <summary>### Lab 2: Managing Software - dnf </summary>

1. **List Available Kernel Updates:**
   ```bash
   sudo dnf list kernel
   ```

2. **Install the Latest Kernel:**
   ```bash
   sudo dnf install kernel
   ```

3. **Check the Transaction History:**
   ```bash
   sudo dnf history
   ```

4. **Undo a Transaction (e.g., ID 5):**
   ```bash
   sudo dnf history undo 5
   ```

---

</details>
