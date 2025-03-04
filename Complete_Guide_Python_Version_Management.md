# Complete Guide to Python Version Management

## Prerequisites
- **Python installed on your system** (check with `python --version`).
- **A version manager** to handle multiple Python versions.

---

## **1️⃣ pyenv (Best Alternative to NVM for Python)**
📌 **What is it?**  
`pyenv` allows you to install, manage, and switch between different Python versions, just like `nvm` does for Node.js.

### **🔹 Install pyenv**
#### **Linux/macOS**
```sh
curl https://pyenv.run | bash
```
Then, add the following to your `~/.bashrc` or `~/.zshrc`:
```sh
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv virtualenv-init -)"
```
Reload your shell:
```sh
source ~/.bashrc  # or source ~/.zshrc
```

#### **Windows**
For Windows, install **pyenv-win** using:
```sh
git clone https://github.com/pyenv-win/pyenv-win.git "$HOME/.pyenv"
setx PYENV "$HOME\.pyenv"
setx PATH "%PYENV%\bin;%PYENV%\shims;%PATH%"
```

---

### **🔹 Install Python Versions Using pyenv**
```sh
pyenv install 3.10.12  # Install Python 3.10.12
pyenv install 3.11.5   # Install Python 3.11.5
```

### **🔹 Set a Global or Local Python Version**
```sh
pyenv global 3.10.12   # Set the default Python version
pyenv local 3.11.5     # Use a specific version for a project
```

### **🔹 Check Installed Versions**
```sh
pyenv versions
```

---

## **2️⃣ Conda (Best for Data Science & AI)**
📌 **What is it?**  
`conda` is a package and environment manager designed for **data science, AI, and ML**. It allows you to create isolated Python environments.

### **🔹 Install Conda (Miniconda)**
```sh
curl -fsSL https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh | bash
```

### **🔹 Create and Manage Python Environments**
```sh
conda create -n my_env python=3.10
conda activate my_env
```

---

## **3️⃣ Virtualenv + venv (Simpler Alternative)**
📌 **What is it?**  
`virtualenv` and `venv` allow you to create isolated Python environments without switching global versions.

### **🔹 Create a Virtual Environment**
```sh
python3 -m venv my_project_env
source my_project_env/bin/activate  # Linux/macOS
my_project_env\Scripts\activate   # Windows
```

To deactivate:
```sh
deactivate
```

---

## **🔥 Which One Should You Use?**
- **`pyenv`** → Best for managing multiple Python versions (like `nvm` for Node.js).  
- **`conda`** → Best for data science, AI, and ML.  
- **`virtualenv/venv`** → Best for simple Python project isolation.

Would you like a **setup guide** similar to the NVM one? 🚀
