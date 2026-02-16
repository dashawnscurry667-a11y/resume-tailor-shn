# Resume Tailor (Render Deploy Guide)

This app helps generate an ATS-friendly resume PDF from a candidate profile
and a job description. It uses AI (Anthropic Claude) to tailor the content and
Puppeteer to create the final PDF.

This README is written for non-technical users who want to deploy the app to
Render.com and use it in the browser.

## What you need before deploying

- A Render.com account
- An Anthropic API key (for resume tailoring)
  - Get it from: https://console.anthropic.com/
- The project code in a Git repository (GitHub, GitLab, or Bitbucket)

## One-time setup (Render.com)

1. Sign in to Render.com
2. Click "New +" then choose "Web Service"
3. Connect your repository (GitHub, GitLab, or Bitbucket)
4. Pick this repository from the list

Render should auto-detect settings, but confirm:

- Environment: Node
- Build Command: `npm install && npm run build`
- Start Command: `npm start`
- Node Version: 20.x (Render uses 20.11.0 in `render.yaml`)

## Environment variables (required)

In Render, open your service settings and add these environment variables:

- `ANTHROPIC_API_KEY` = your Anthropic key (required)
- `ANTHROPIC_MODEL` = optional (default: `claude-3-5-sonnet-20241022`)
- `` = 

Render will automatically set `PORT` for you.

## Deploy

1. Click "Create Web Service"
2. Wait for the build to finish
3. Open the service URL that Render provides

## How to use the app

1. Open the app in your browser
2. Choose a profile from the dropdown
3. Choose a template style
4. Fill in:
   - Company name
   - Role name
   - Job description (paste full JD text)
5. Click "Generate Tailored Resume"
6. A PDF will download automatically

## Adding or editing profiles

Profiles are stored as JSON files in `resumes/`.

- Use `resumes/_template.json` as a guide
- File name format: `FirstName_LastName.json`
- After adding a file, redeploy (or push to the repo and Render will auto-deploy)

## Adding or editing templates

Templates are HTML files in `templates/`.

- Use Handlebars syntax (`{{name}}`, `{{summary}}`, etc.)
- File name format: `Resume-Style-Color.html`
- After adding a template, redeploy

## Local development (optional)

If a developer wants to run it locally:

1. Install Node.js 20.x
2. Run: `npm install`
3. Set `ANTHROPIC_API_KEY`
4. Start: `npm run dev`
5. Open: http://localhost:3000

## Troubleshooting

- **Blank PDF or error**: Check `ANTHROPIC_API_KEY`
- **Build fails**: Confirm Node version 20.x and install steps
- **No profiles**: Ensure JSON files exist in `resumes/`
- **Template not listed**: Ensure file ends with `.html` in `templates/`

## Notes

- The PDF parsing page (`/parse`) is not fully implemented.
- The app tailors resume content based on the job description, so results vary.
