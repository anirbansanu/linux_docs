Guide on how to install, configure, and use Git and Git LFS:

### **1. Installing Git**

#### **On Ubuntu**
1. **Update your package index:**
   ```bash
   sudo apt update
   ```
2. **Install Git:**
   ```bash
   sudo apt install git
   ```
3. **Verify the installation:**
   ```bash
   git --version
   ```

#### **On Windows**
1. **Download the Git installer:**
   - Visit the [Git official website](https://git-scm.com/download/win) and download the installer.
2. **Run the installer** and follow the instructions.
3. **Verify the installation** by opening a command prompt and typing:
   ```bash
   git --version
   ```

### **2. Configuring Git**

After installing Git, you need to configure it with your user information.

1. **Set your username:**
   ```bash
   git config --global user.name "Your Name"
   ```
2. **Set your email:**
   ```bash
   git config --global user.email "your.email@example.com"
   ```

3. **Verify your configuration:**
   ```bash
   git config --list
   ```

### **3. Installing Git LFS (Large File Storage)**

Git LFS is used to handle large files that are too big for regular Git repositories.

#### **On Ubuntu**
1. **Install Git LFS:**
   ```bash
   sudo apt install git-lfs
   ```
2. **Initialize Git LFS:**
   ```bash
   git lfs install
   ```

#### **On Windows**
1. **Download the Git LFS installer** from the [Git LFS website](https://git-lfs.github.com/).
2. **Run the installer** and follow the instructions.
3. **Initialize Git LFS:**
   ```bash
   git lfs install
   ```

### **4. Using Git LFS**

#### **Step 1: Track Files with Git LFS**
To track a specific type of file (e.g., `.psd`, `.zip`, `.sql`), use the following command:

```bash
git lfs track "*.psd"
```

This command creates a `.gitattributes` file that tells Git to use LFS for all `.psd` files.

#### **Step 2: Add and Commit Files as Usual**
Once Git LFS is tracking a file type, you can add and commit files as usual:

```bash
git add .gitattributes
git add yourfile.psd
git commit -m "Add a large file"
```

#### **Step 3: Push to Remote Repository**
When pushing to a remote repository, Git LFS will handle the large files automatically:

```bash
git push origin your-branch
```

### **5. Cloning a Repository with Git LFS**

If you're cloning a repository that uses Git LFS, Git LFS will automatically download the large files:

```bash
git clone https://github.com/user/repo.git
```

### **6. Managing Git LFS Files**

To see which files are being tracked by Git LFS, use:

```bash
git lfs ls-files
```

### **7. Additional Git LFS Commands**

- **Untrack a file:**
  ```bash
  git lfs untrack "*.psd"
  ```
- **Check Git LFS version:**
  ```bash
  git lfs version
  ```

With these steps, you should be able to install, configure, and use Git and Git LFS efficiently. 