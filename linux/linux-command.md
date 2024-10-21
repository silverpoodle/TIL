### **1. RPM (Red Hat Package Manager) Commands**
- **Install/Upgrade a package**:  
  ```shell
  rpm -ivh mypkg-2.7-5.x86_64.rpm  # Install package
  rpm -Uvh mypkg-2.7-5.x86_64.rpm  # Upgrade package
  ```
  - `-i`: Install the package.
  - `-U`: Upgrade the package.
  - `-v`: Verbose output.
  - `-h`: Show progress bar using hashes (#).

- **Remove a package**:  
  ```shell
  rpm -e mypkg
  ```
  - `-e`: Erase (remove) the package.

- **Query a package**:  
  ```shell
  rpm -q mypkg
  ```
  - `-q`: Query the package (check if it's installed).

### **2. YUM (Yellowdog Updater Modified) Commands**
- **Check for package updates**:  
  ```shell
  yum check-update
  ```

- **Update all installed packages**:  
  ```shell
  sudo yum update
  ```

- **Display package information**:  
  ```shell
  yum info package_name
  ```

- **Update a specific package**:  
  
  ```shell
  yum update package_name
  ```
  
- **List all available or installed packages**:  
  ```shell
  yum list available  # List all available packages
  yum list installed  # List all installed packages
  yum list installed  | wc -l # count all installed packages 
  yum list installed | grep nginx # check if nginx is installed
  ```
  
- **Search for a package by name**:  
  ```sh
  yum search package_name
  ```

- **Install a package**:  
  ```shell
  sudo yum install package_name
  ```

- **Install a specific version of a package**:  
  ```shell
  sudo yum install gcc-4.0
  ```

- **Install a local RPM package**:  
  ```shell
  sudo yum install /path/to/package.rpm
  ```

- **Remove a package**:  
  
  ```shell
  sudo yum remove package_name
  ```

### **3. Apache HTTP Server Management**
- **Check if Apache is installed**:  
  ```shell
  yum list installed | grep httpd
  ```

- **Install Apache HTTP Server**:  
  ```shell
  sudo yum install httpd
  ```

- **Start Apache service**:  
  ```shell
  sudo systemctl start httpd
  ```

- **Check the status of Apache service**:  
  
  ```shell
  sudo systemctl status httpd
  ```
  
- **Remove Apache HTTP Server**:  
  ```shell
  sudo yum remove httpd
  ```

- **Service Startup** (Open TCP port 80)

  ```shell
  sudo systemctl start httpd
  sudo systemctl status httpd
  ```

  