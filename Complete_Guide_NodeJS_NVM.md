# Complete Guide to Installing Node.js with NVM

## Prerequisites
- **NVM (Node Version Manager)** is required to manage multiple Node.js versions efficiently.
- **Bash or Zsh shell** (if using Linux/macOS).

---

## 1️⃣ Install NVM (Node Version Manager)

### **🔹 For Linux/macOS**
1. **Download and install NVM**:
   ```sh
   curl -fsSL https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.4/install.sh | bash
   ```
2. **Load NVM into your shell**:
   ```sh
   source ~/.bashrc  # Use ~/.zshrc if using Zsh
   ```
3. **Verify NVM installation**:
   ```sh
   command -v nvm
   ```
   If `nvm` appears, the installation was successful.

### **🔹 For Windows**
1. **Download the NVM for Windows installer**:
   👉 [NVM for Windows](https://github.com/coreybutler/nvm-windows/releases)
2. **Run the installer** and follow the setup instructions.
3. **Restart your terminal (PowerShell, Git Bash, or CMD).**
4. **Verify installation**:
   ```sh
   nvm version
   ```

---

## 2️⃣ Fixing Missing `.bashrc` (Linux/macOS)
If you encountered `bash: /u//.bashrc: No such file or directory`, follow these steps:

1. **Check if `.bashrc` exists**:
   ```sh
   ls -la ~ | grep .bashrc
   ```
   - If no output, the file is missing.
   
2. **Create or update `.bashrc`**:
   ```sh
   touch ~/.bashrc
   echo 'export NVM_DIR="$HOME/.nvm"' >> ~/.bashrc
   echo '[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"' >> ~/.bashrc
   echo '[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"' >> ~/.bashrc
   ```
3. **Reload `.bashrc`**:
   ```sh
   source ~/.bashrc
   ```
4. **Verify NVM again**:
   ```sh
   command -v nvm
   ```

---

## 3️⃣ Install Node.js with NVM
1. **Install the latest Node.js 18 LTS version**:
   ```sh
   nvm install 18
   ```
2. **Use the installed Node.js version**:
   ```sh
   nvm use 18
   ```
3. **Set the default Node.js version**:
   ```sh
   nvm alias default 18
   ```
4. **Verify Node.js installation**:
   ```sh
   node -v
   ```
   The output should be `v18.18.0` or later.

---

## 4️⃣ Install npm and pnpm
### **🔹 Install npm (Node Package Manager)**
`npm` comes bundled with Node.js, but if needed, you can update it:
```sh
npm install -g npm@latest
```
Verify installation:
```sh
npm -v
```

### **🔹 Install pnpm (Performant Package Manager)**
Install `pnpm` globally:
```sh
npm install -g pnpm
```
Verify installation:
```sh
pnpm -v
```

---

## 5️⃣ Avoid Mixing Package Managers
Using multiple package managers in a project can cause dependency conflicts. If you find both `package-lock.json` (npm) and `pnpm-lock.yaml` (pnpm) in your project, follow these steps:

### **🔹 Standardize on One Package Manager**
#### **Use npm (if originally used npm)**
1. Remove conflicting files:
   ```sh
   rm -rf pnpm-lock.yaml node_modules
   ```
2. Reinstall dependencies:
   ```sh
   npm install
   ```

#### **Use pnpm (if originally used pnpm)**
1. Remove conflicting files:
   ```sh
   rm -rf package-lock.json node_modules
   ```
2. Reinstall dependencies:
   ```sh
   pnpm install
   ```

### **🔹 Verify Only One Lock File Exists**
After the cleanup, check that only **one** of the lock files remains:
```sh
ls -la | grep "lock"
```
- If using **npm**, you should only see `package-lock.json`.
- If using **pnpm**, you should only see `pnpm-lock.yaml`.

This will prevent issues like dependencies being moved to `node_modules/.ignored` and ensure a smooth package management experience.

---

## 6️⃣ Troubleshooting
If `nvm` is not found:
1. **Ensure `.bashrc` is loaded correctly**:
   ```sh
   source ~/.bashrc  # or source ~/.zshrc if using Zsh
   ```
2. **Manually reinstall NVM**:
   ```sh
   curl -fsSL https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.4/install.sh | bash
   source ~/.bashrc
   ```

---

## 🎉 Next Steps
Once Node.js, npm, and pnpm are installed correctly, you can proceed with other setups like installing dependencies for your project using `npm install` or `pnpm install`.
