# ICT Exoticz Website

Website for ICT Exoticz — Wichita, KS. Built with [Astro](https://astro.build/).

---

## Table of Contents

1. [Running the Site Locally](#running-the-site-locally)
2. [Project Structure](#project-structure)
3. [Deploying to GitHub Pages](#deploying-to-github-pages)
   - [Step 1: Create a GitHub Account](#step-1-create-a-github-account)
   - [Step 2: Install Git](#step-2-install-git)
   - [Step 3: Create a GitHub Repository](#step-3-create-a-github-repository)
   - [Step 4: Update astro.config.mjs](#step-4-update-astroconfigmjs)
   - [Step 5: Push Your Code to GitHub](#step-5-push-your-code-to-github)
   - [Step 6: Enable GitHub Pages](#step-6-enable-github-pages)
   - [Step 7: Visit Your Live Site](#step-7-visit-your-live-site)
4. [Making Updates](#making-updates)
5. [Custom Domain (Optional)](#custom-domain-optional)

---

## Running the Site Locally

Before deploying, you can preview the site on your own computer.

**Prerequisites:**
- [Node.js](https://nodejs.org/) (version 18 or higher)

**Steps:**

```bash
# 1. Open a terminal and navigate to the project folder
cd ict-exoticz

# 2. Install dependencies
npm install

# 3. Start the development server
npm run dev
```

Then open your browser and go to `http://localhost:4321` to see the site.

To build the final version:

```bash
npm run build
```

---

## Project Structure

```
ict-exoticz/
├── .github/
│   └── workflows/
│       └── deploy.yml        # Automatically deploys to GitHub Pages on every push
├── public/
│   └── favicon.svg           # Browser tab icon
├── src/
│   ├── components/
│   │   ├── Header.astro      # Top navigation bar
│   │   └── Footer.astro      # Bottom footer with contact info
│   ├── layouts/
│   │   └── Layout.astro      # Shared page wrapper (header + footer)
│   └── pages/
│       ├── index.astro       # Home page
│       ├── products.astro    # Products page
│       ├── locations.astro   # Locations & hours page
│       └── contact.astro     # Contact page
├── astro.config.mjs          # Astro configuration (site URL, base path)
├── package.json              # Project dependencies
└── README.md                 # This file
```

---

## Deploying to GitHub Pages

GitHub Pages is a free hosting service from GitHub. Here's how to get your site live from scratch.

---

### Step 1: Create a GitHub Account

1. Go to [github.com](https://github.com)
2. Click **Sign up**
3. Follow the prompts to create a free account
4. Verify your email address

> Write down your GitHub username — you'll need it in Step 4.

---

### Step 2: Install Git

Git is the tool that sends your code up to GitHub.

1. Go to [git-scm.com/downloads](https://git-scm.com/downloads)
2. Download and install Git for Windows
3. During install, leave all default settings as-is
4. Open a new terminal (search "Git Bash" in the Start menu) after installing

Verify it worked:
```bash
git --version
```
You should see something like `git version 2.x.x`.

---

### Step 3: Create a GitHub Repository

A repository ("repo") is where your code lives on GitHub.

1. Log in to [github.com](https://github.com)
2. Click the **+** icon in the top right corner → **New repository**
3. Fill in:
   - **Repository name:** `ict-exoticz`
   - **Description:** ICT Exoticz website (optional)
   - **Visibility:** Public *(GitHub Pages requires public repos on free accounts)*
4. Leave everything else unchecked
5. Click **Create repository**

You'll land on a page that shows setup instructions — keep this tab open.

---

### Step 4: Update astro.config.mjs

Open the file `astro.config.mjs` in the project folder and update the `site` line with your actual GitHub username:

```js
export default defineConfig({
  site: 'https://YOUR_GITHUB_USERNAME.github.io',  // <-- change this
  base: '/ict-exoticz',
  output: 'static',
});
```

For example, if your GitHub username is `johndoe`:
```js
site: 'https://johndoe.github.io',
```

Save the file.

---

### Step 5: Push Your Code to GitHub

Open **Git Bash** (or your terminal), navigate to the project folder, and run these commands one at a time:

```bash
# 1. Go into the project folder
cd /c/Users/jalob/ict-exoticz

# 2. Initialize git in this folder (only needed once)
git init

# 3. Tell git your name and email (only needed once, use your real info)
git config user.name "Your Name"
git config user.email "your@email.com"

# 4. Add all project files to be tracked
git add .

# 5. Save a snapshot of the files (called a "commit")
git commit -m "Initial commit"

# 6. Set the main branch name
git branch -M main

# 7. Link your local folder to the GitHub repository
#    Replace YOUR_GITHUB_USERNAME with your actual username
git remote add origin https://github.com/YOUR_GITHUB_USERNAME/ict-exoticz.git

# 8. Push (upload) your code to GitHub
git push -u origin main
```

You'll be asked to log in to GitHub. If prompted for a password, use a **Personal Access Token** instead:
1. Go to GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Click **Generate new token (classic)**
3. Check the `repo` scope
4. Copy the token and paste it as your password

---

### Step 6: Enable GitHub Pages

1. Go to your repository on GitHub: `https://github.com/YOUR_GITHUB_USERNAME/ict-exoticz`
2. Click the **Settings** tab (top of the repo page)
3. In the left sidebar, click **Pages**
4. Under **Source**, select **GitHub Actions**
5. Click **Save**

The deploy workflow (`.github/workflows/deploy.yml`) will now run automatically every time you push code. You can watch it run:

1. Click the **Actions** tab in your repository
2. You'll see a workflow called "Deploy to GitHub Pages" running
3. Wait for it to show a green checkmark (takes 1–3 minutes)

---

### Step 7: Visit Your Live Site

Once the workflow finishes, your site will be live at:

```
https://YOUR_GITHUB_USERNAME.github.io/ict-exoticz
```

Replace `YOUR_GITHUB_USERNAME` with your actual GitHub username.

---

## Making Updates

Any time you edit files and want to publish the changes:

```bash
# From inside the project folder:

# 1. Stage your changes
git add .

# 2. Commit with a short description of what you changed
git commit -m "Update hours for Broadway location"

# 3. Push to GitHub (this triggers a new deploy automatically)
git push
```

The site will update within 1–3 minutes.

---

## Custom Domain (Optional)

If you have a custom domain (e.g., `ictexoticz.com`), you can point it to GitHub Pages:

1. Go to repo **Settings** → **Pages**
2. Under **Custom domain**, enter your domain and click **Save**
3. At your domain registrar (e.g., GoDaddy, Namecheap), add a CNAME DNS record:
   - **Name:** `www`
   - **Value:** `YOUR_GITHUB_USERNAME.github.io`
4. Update `astro.config.mjs`:
   ```js
   export default defineConfig({
     site: 'https://www.ictexoticz.com',
     base: '/',  // Change to '/' when using a custom domain
     output: 'static',
   });
   ```
5. Add a `CNAME` file to the `public/` folder:
   ```
   www.ictexoticz.com
   ```

DNS changes can take up to 24 hours to take effect.
