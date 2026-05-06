# Chic Portfolio Design

Production-ready React + Vite portfolio with contact and feedback forms that work on static hosting (GitHub Pages) using EmailJS and/or Web3Forms.

## 1) Local Setup

Prerequisites:
- Node.js 20+ (LTS recommended)
- npm (comes with Node.js)

Install and run:

```bash
npm install
npm run dev
```

## 2) Contact Form Setup (EmailJS)

This project supports client-side email sending for static hosting.

Create `.env` in project root:

```bash
VITE_EMAILJS_PUBLIC_KEY=your_public_key_here
VITE_EMAILJS_SERVICE_ID=your_service_id_here
VITE_EMAILJS_TEMPLATE_ID=your_template_id_here
```

Important:
- Use the **Public Key** from EmailJS in `VITE_EMAILJS_PUBLIC_KEY`.
- Do **not** put EmailJS private key in frontend env files.
- Your EmailJS template must include these variables:
  - `form_type`
  - `from_name`
  - `from_email`
  - `subject`
  - `message`

Optional fallback:
- You can also configure `VITE_WEB3FORMS_ACCESS_KEY` to use Web3Forms.

## 3) GitHub Pages Deployment

### A) Set base path in GitHub Actions environment

For repo deployment URL:

`https://<username>.github.io/<repo-name>/`

base path must be:

`/<repo-name>/`

This is configured in workflow by setting `VITE_BASE_PATH`.

### B) Push to `main`

The included GitHub Actions workflow builds and deploys to Pages on each push to `main`.

## 4) Configure GitHub Secrets

In GitHub repo:
`Settings -> Secrets and variables -> Actions -> New repository secret`

Add:
- `VITE_EMAILJS_PUBLIC_KEY`
- `VITE_EMAILJS_SERVICE_ID`
- `VITE_EMAILJS_TEMPLATE_ID`
- Optional: `VITE_WEB3FORMS_ACCESS_KEY`

## 5) First-Time GitHub Pages Enablement

In GitHub repo:
`Settings -> Pages`

Set:
- Source: `GitHub Actions`

Then push to `main` and wait for deployment to complete.

## 6) Production Checklist

- `npm run build` succeeds locally
- EmailJS template variables match exactly
- GitHub secrets are present
- Workflow run is green
- Open deployed URL and test:
  - Send Message form
  - Feedback form

## 7) Troubleshooting

- Form does not send:
  - Recheck EmailJS service ID, template ID, and public key.
  - Confirm template variable names match exactly.
- Blank or broken asset paths:
  - Ensure `VITE_BASE_PATH` equals `/<repo-name>/` in workflow.
- 404 on direct route refresh:
  - Workflow creates `404.html` fallback automatically for SPA routing.
