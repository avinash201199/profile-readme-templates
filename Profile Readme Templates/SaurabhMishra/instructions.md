# 🐍 GitHub Profile Snake Animation Setup Guide

This guide helps you add an animated "Snake" that slitherers through your GitHub contribution grid — just like the one in this README!
Follow the steps below carefully. 🚀

---

## 📂 1️⃣ Create Required Folder and File

Inside your GitHub profile repository (the one named after your username, e.g., `saurabhm6341/saurabhm6341`), create the following folder and file structure:

.github/
└── workflows/
└── snake.yml


> 💡 **Tip:** The `.github` folder should be at the **root** of your repository.

---

## ⚙️ 2️⃣ Paste the Workflow Code

Open the `snake.yml` file and paste the following complete configuration.

**Remember to replace `YOUR_GITHUB_USERNAME` with your actual GitHub username.**

```yaml
name: Generate Snake Animation

on:
  # Run automatically every 12 hours
  schedule:
    - cron: "0 */12 * * *"

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

jobs:
  generate:
    runs-on: ubuntu-latest
    permissions:
      contents: write # Allows the action to push generated files

    steps:
      # Checkout the repository
      - name: Checkout repository
        uses: actions/checkout@v4

      # Generate the snake animation
      - name: Generate Snake 🐍
        uses: Platane/snk@v3
        with:
          github_user_name: YOUR_GITHUB_USERNAME
          # Generate a transparent background SVG
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark

      # Push the generated files to the 'output' branch
      - name: Push Snake Animation to output branch
        uses: crazy-max/ghaction-github-pages@v4
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
````

-----

## 🔐 3️⃣ Enable GitHub Actions Permissions

This step is crucial for the action to be able to commit the generated animation file back to your repository.

1.  Go to your repository **Settings** → **Actions** → **General**.
2.  Scroll down to the **Workflow permissions** section.
3.  Select the option ✅ **“Read and write permissions”**.
4.  Click **Save**.

-----

## ▶️ 4️⃣ Trigger the Workflow Manually

Now, let's run the action for the first time to generate the animation.

1.  Go to the **Actions** tab in your repository.
2.  Under "All workflows," click on **"Generate Snake Animation"**.
3.  Click the **"Run workflow"** dropdown button on the right, then click the green **"Run workflow"** button.
4.  Wait a minute or two for the workflow to complete successfully.

Once it's done, a new branch named `output` will be automatically created in your repository containing the snake SVG file.

-----

## 🐍 5️⃣ Add the Snake Animation to Your README

Finally, add the following Markdown snippet to your `README.md` file where you want the animation to appear.

**Remember to replace `YOUR_GITHUB_USERNAME` twice in the URL.**

```markdown
### 🐍 Watch My Contributions Slither!

<div align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="[https://raw.githubusercontent.com/YOUR_GITHUB_USERNAME/YOUR_GITHUB_USERNAME/output/github-contribution-grid-snake-dark.svg](https://raw.githubusercontent.com/YOUR_GITHUB_USERNAME/YOUR_GITHUB_USERNAME/output/github-contribution-grid-snake-dark.svg)">
    <source media="(prefers-color-scheme: light)" srcset="[https://raw.githubusercontent.com/YOUR_GITHUB_USERNAME/YOUR_GITHUB_USERNAME/output/github-contribution-grid-snake.svg](https://raw.githubusercontent.com/YOUR_GITHUB_USERNAME/YOUR_GITHUB_USERNAME/output/github-contribution-grid-snake.svg)">
    <img alt="github contribution grid snake animation" src="[https://raw.githubusercontent.com/YOUR_GITHUB_USERNAME/YOUR_GITHUB_USERNAME/output/github-contribution-grid-snake.svg](https://raw.githubusercontent.com/YOUR_GITHUB_USERNAME/YOUR_GITHUB_USERNAME/output/github-contribution-grid-snake.svg)">
  </picture>
</div>
```

> The code above will automatically show a light or dark version of the snake based on the viewer's system theme\!

-----

## 🎉 Done\!

Your GitHub profile will now proudly display a real-time animated snake that grows with your contributions\! 🐍✨

> ### 💬 Troubleshooting
>
> If you encounter an error like `The process '/usr/bin/git' failed with exit code 128`, it almost always means the workflow doesn't have the necessary permissions. Double-check that you have enabled **"Read and write permissions"** as described in **Step 3**.