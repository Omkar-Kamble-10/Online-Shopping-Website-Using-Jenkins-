# Universal Two‑Page Website Template

This is a **simple HTML/CSS website** that can be reused as:

- A personal portfolio site  
- A college information site  
- An event management landing page  
- Any basic informational site

You only need to change the **name and text**.

---

## 1. Project Structure

```text
.
├── index.html        # Home page
├── about.html        # Second page
├── assets
│   └── css
│       └── style.css
└── Jenkinsfile       # Jenkins pipeline definition
```

---

## 2. How to Customize the Website

1. Open `index.html` and `about.html`.
2. Search for `My Awesome Site` and replace it with your site name.
3. Change headings and text to match your use case (portfolio / college / event).
4. Update contact details in the **Quick Contact** section of `index.html`.
5. (Optional) Adjust colors and styles in `assets/css/style.css`.

---

## 3. Initialize Git and Push to GitHub

Run these commands in the project folder:

```bash
git init
git add .
git commit -m "Initial universal site template"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

---

## 4. Jenkins Pipeline Setup

1. Open Jenkins and create a **New Item → Pipeline**.
2. In **Pipeline** configuration, choose:
   - Definition: **Pipeline script from SCM**
   - SCM: **Git**
   - Repository URL: your GitHub repository URL.
3. Save the job.

Jenkins will automatically read the `Jenkinsfile` and run the pipeline.

### Environment Variable for Deployment

To deploy to a folder on your Jenkins server (for example, `/var/www/html/my-site`):

1. In the Jenkins job configuration, under **Build Environment** or **Pipeline**:
   - Add an **environment variable**:  
     - Name: `DEPLOY_PATH`  
     - Value: `/var/www/html/my-site`
2. Make sure Jenkins has permission to write to that folder.

If `DEPLOY_PATH` is **empty**, the pipeline will still build and package, but it will skip deployment.

---

## 5. GitHub Webhook for Automatic Trigger

1. In your GitHub repo, go to **Settings → Webhooks → Add webhook**.
2. **Payload URL**: `http://<your-jenkins-server>/github-webhook/`
3. **Content type**: `application/json`
4. **Which events?**: *Just the push event* (or more if you prefer).
5. Click **Add webhook**.

On Jenkins:

1. Install the **GitHub Integration / GitHub plugin** if not already installed.
2. In the job configuration, check **"GitHub hook trigger for GITScm polling"**.

Now **every push to GitHub** will trigger the Jenkins pipeline, which will:

1. Checkout latest code  
2. (Optionally) build/test  
3. Package the static site  
4. Deploy it to `DEPLOY_PATH` (if configured)  

---

Enjoy using this as a simple starting point for any small static website! ✨
