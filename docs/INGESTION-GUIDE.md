# Private Repository & Multi-Platform Ingestion Guide

In M&A and Private Equity transactions, target codebases are virtually always private, confidential, or stored within virtual data rooms. Veridence provides four flexible ingestion pathways tailored to deal teams and corporate counsel.

---

```mermaid
flowchart TD
    Ingest["Codebase Ingestion Channels"]
    
    Ingest --> App["<b>Channel 1: GitHub App</b><br/>• Zero developer tokens<br/>• Connected by an account owner via /veridence github<br/>• Recommended for non-technical teams"]
    Ingest --> PAT["<b>Channel 2: 1-Time Workspace PAT</b><br/>• Classic GitHub PAT with 'repo' scope<br/>• Bound once via /veridence auth<br/>• Shared by the whole Slack workspace"]
    Ingest --> VDR["<b>Channel 3: Virtual Data Rooms</b><br/>• Google Drive / Box / AWS S3<br/>• Pre-signed HTTPS download links<br/>• Read in memory; not stored after the audit"]
    Ingest --> Web["<b>Channel 4: Web Console</b><br/>• Repository URL and license key<br/>• Optional GitHub token for private repos<br/>• On-screen report"]

    classDef chan fill:#0f172a,stroke:#38bdf8,stroke-width:1.5px,color:#f8fafc;
    class App,PAT,VDR,Web chan;
```

---

## Option A: The GitHub App (Recommended — Zero Token Management)

The simplest pathway for deal teams and target companies. No developer settings or API keys are handled.

1. **Get your workspace's link:**
   Inside your deal-room Slack workspace, run:
   ```bash
   /veridence github
   ```
   Veridence replies with a link that belongs to your workspace and is valid for 7 days.
2. **Have the account owner open it:**
   Send the link to an owner of the GitHub account that holds the target repositories. They sign in to GitHub and, if the **[Veridence GitHub App](https://github.com/apps/veridence)** is not installed yet, install it, specifying **"Only select repositories"** (e.g., `acquirer-target-core`) or all repositories. Only an owner of the account can connect it.
3. **Execute in Slack:**
   ```bash
   /veridence audit https://github.com/target-org/acquirer-target-core
   ```
   *The Veridence bot uses short-lived GitHub App installation tokens behind the scenes, so nobody has to manage a token.*

Starting from GitHub also works: install the app first, then use the **Add Veridence to Slack** button on the page that follows, and the account is connected to the workspace you add.

---

## Option B: 1-Time Workspace Personal Access Token (PAT) Link

If organization administration restrictions prevent installing the GitHub App, an authorized team member can link a classic Personal Access Token once:

1. **Generate Token:**
   * Log into GitHub (`github.com`).
   * Click profile icon (top-right) ➔ **Settings** ➔ scroll down to **Developer settings** (bottom-left).
   * Click **Personal access tokens** ➔ **Tokens (classic)** ➔ **Generate new token (classic)**.
   * Note: `Veridence Deal Room`.
   * Expiration: `30 days` (or length of diligence period).
   * Scopes: Check **`repo`** (Full control of private repositories).
   * Click green **Generate token** button and copy the token (`ghp_...`).
2. **Register Once in Slack:**
   In your deal-room Slack channel, execute:
   ```bash
   /veridence auth ghp_YourCopiedTokenStringHere
   ```
3. **Audit Privately:**
   Everyone in the Slack workspace can now audit private repositories without specifying tokens:
   ```bash
   /veridence audit https://github.com/target-org/private-repo
   ```

---

## Option C: Virtual Data Rooms & Cloud Storage Links

In institutional transactions, target companies often export sanitized codebase archives into Virtual Data Rooms (VDRs) or shared cloud folders:

* **Google Drive:**
  ```bash
  /veridence audit https://drive.google.com/file/d/1A2B3C4D5E.../view
  ```
* **Box.com:**
  ```bash
  /veridence audit https://app.box.com/s/abcdef123456...
  ```
* **Pre-signed AWS S3 / Cloudflare R2:**
  ```bash
  /veridence audit https://s3.amazonaws.com/target-vdr-escrow/snapshot.zip?X-Amz-Signature=...
  ```

---

## Option D: Web Console

For teams working outside Slack, open the **[Veridence Web Console](https://www.veridence.agiphi.com/?view=dashboard)**, enter your evaluation credential or license key and the repository URL (add a GitHub token for a private repository). The deterministic scan runs and the report appears on screen.
