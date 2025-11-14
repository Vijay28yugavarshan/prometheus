# Prometheus


## Admin login
Set `ADMIN_PASSWORD` and `ADMIN_JWT_SECRET` in backend/.env to enable admin login route `/api/admin/login` which returns a JWT.

---
## Fly.io Deployment (recommended)

### Prerequisites
- Install `flyctl`: https://fly.io/docs/hands-on/install-flyctl/
- Create a Fly account and run `flyctl auth login`

### Create Fly apps (once)
```bash
# login and create apps
flyctl apps create prometheus-backend --org personal
flyctl apps create prometheus-frontend --org personal
# or choose your region
```
Then set secrets on Fly (example):
```bash
flyctl secrets set OPENAI_API_KEY=sk-... BRAVE_API_KEY=bravekey ADMIN_PASSWORD=yourpassword ADMIN_JWT_SECRET=supersecret --app prometheus-backend
```
Deploy manually (from repo root) using images built by GitHub Actions, or use `flyctl deploy` to build from local Dockerfile:
```bash
# deploy backend by building locally
cd backend
flyctl deploy --app prometheus-backend
# deploy frontend
cd ../frontend
flyctl deploy --app prometheus-frontend
```
Or use the GitHub Actions workflow `.github/workflows/fly-deploy.yml` which builds images and deploys automatically when you push to `main`. Make sure you set these repository secrets in GitHub:
- `FLY_API_TOKEN` (from `flyctl auth token`)
- `FLY_APP_NAME_BACKEND` (e.g. prometheus-backend)
- `FLY_APP_NAME_FRONTEND` (e.g. prometheus-frontend)

