<div align="center">
  <h1>Hi, I'm Danesh 👋</h1>
  <p><strong>Computer Networks & Security • IoT Automation • Cloud & AI</strong></p>

  <!-- Live Git-Koi Animation (generated via GitHub Actions) -->
  <a href="https://docs.rs/git-koi/latest/git_koi/">
    <img src="./dist/koi.gif" alt="GitHub Activity Koi" width="320" />
  </a>
  <br />
  <sub>
    Powered by <a href="https://docs.rs/git-koi/latest/git_koi/"><code>git-koi</code></a> — procedurally colored & animated from my public commit streaks and language shares.
  </sub>
</div>

---

### 🚀 About Me
- 🎓 Final-year Computer Science student (**Computer Networks & Security**) at Universiti Teknologi Malaysia.
- 🌱 Currently building **AgriBox**, an industrial IoT smart fertigation and environmental monitoring system powered by Raspberry Pi Compute Module.
- 🛠️ Interested in network automation, cloud-native architectures, and embedded Linux systems.

---

### 🐟 How the Koi Works
The animated koi above is generated automatically via a scheduled GitHub Action using the [`git_koi`](https://docs.rs/git-koi/latest/git_koi/) Rust library:
- **Coat & Pigments:** Derived proportionally from top repository languages (`coat` & `history` modules).
- **Markings & Growth:** Reflects current and longest contribution streaks (`markings` & `koi` modules).
- **Swimming Behavior:** Dictated by recent commit velocity and weekly participation (`behavior` & `motion` modules).

---

### ⚙️ GitHub Actions Setup
To run this in your profile repository (`username/username`), add `.github/workflows/koi.yml`:

```yaml
name: Update Git-Koi

on:
  schedule:
    - cron: "0 0 * * *" # Runs daily at midnight UTC
  workflow_dispatch:

permissions:
  contents: write

jobs:
  generate-koi:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Install Rust & git-koi
        run: cargo install git-koi

      - name: Generate Koi GIF
        env:
          GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        run: |
          mkdir -p dist
          git-koi --user ${{ github.repository_owner }} --output dist/koi.gif

      - name: Commit & Push
        run: |
          git config user.name "github-actions[bot]"
          git config user.email "github-actions[bot]@users.noreply.github.com"
          git add dist/koi.gif
          git commit -m "chore: update git-koi animation" || exit 0
          git push
