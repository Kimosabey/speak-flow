# Git Workflow Guide: Personal vs. Office

This guide explains how to work with your dual Git setup.

## 1. Office / Work Projects (Default)
**Use this for:** Company projects, Azure DevOps, standard GitHub work.

*   **Setup:** Do nothing special.
*   **Clone:** Use standard URLs (HTTPS or standard SSH).
    ```powershell
    git clone https://github.com/Company/Backend.git
    ```
*   **Identity:** Default (Global) settings are used automatically.
    *   **Email:** `harshan.aiyappa@company.com`
    *   **Name:** `harshan-aiyappa`

---

## 2. Personal Projects (Kimosabey)
**Use this for:** Your personal POCs and private repos.

**Step 1: Create/Clone with the Alias**
When adding a remote or cloning, change `github.com` to `github.com-personal`.

*   **Clone Example:**
    ```powershell
    git clone git@github.com-personal:Kimosabey/MyNewProject.git
    ```

*   **Existing Repo Example:**
    ```powershell
    git remote add origin git@github.com-personal:Kimosabey/MyNewProject.git
    ```

**Step 2: Configure Local Identity (Crucial)**
You MUST run these commands inside **every new personal project folder** to ensure commits are linked to your personal account.

```powershell
cd D:\01_Projects\Personal\MyNewProject
git config user.name "Kimosabey"
git config user.email "harshan.aiyappa@gmail.com"
```

### Summary Checklist for New Personal Projects
1.  [ ] Initialize: `git init`
2.  [ ] Set Remote: `git remote add origin git@github.com-personal:YourUser/Repo.git`
3.  [ ] **Set Identity**: `git config user.email ...` (Don't forget this!)
