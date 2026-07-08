# Deploy on Dokploy

This repo includes a Dockerfile and `docker-compose.yml` for deploying the
Next.js app to Dokploy while keeping Supabase as the external database/auth
provider.

## Dokploy setup

1. Create a new project in Dokploy.
2. Add a new **Compose** service and select **Docker Compose**.
3. Select your GitHub provider and repository.
4. Use branch `main`.
5. Set **Compose Path** to `./docker-compose.yml`.
6. Add the environment variables from `.env.local.example` in Dokploy's
   Environment tab before deploying.
7. Configure the public domain in Dokploy's **Domains** tab and route it to
   container port `3002`.
8. Deploy.

For direct IP testing, open TCP port `3002` on the server firewall and visit
`http://<server-ip>:3002`.

## Required environment variables

Set these before the first build:

```bash
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key
ENCRYPTION_KEY=your-64-char-hex-key-here
META_APP_SECRET=your-meta-app-secret
```

Recommended:

```bash
NEXT_PUBLIC_SITE_URL=https://crm.example.com
NEXT_PUBLIC_APP_LOCALE=en
```

Optional variables are documented in `.env.local.example`.

## Notes

- `NEXT_PUBLIC_*` variables are passed as Docker build args because Next.js
  embeds public variables into the client bundle during `npm run build`.
- The Dockerfile includes harmless placeholder defaults so Docker can complete
  a build even before Dokploy receives real Supabase values. Replace
  `NEXT_PUBLIC_SUPABASE_URL` and `NEXT_PUBLIC_SUPABASE_ANON_KEY` with real
  Supabase project values and redeploy before using the app.
- Secrets such as `SUPABASE_SERVICE_ROLE_KEY`, `ENCRYPTION_KEY`, and
  `META_APP_SECRET` are loaded at runtime from Dokploy's generated `.env` file
  via `env_file`.
- The compose service joins Dokploy's external `dokploy-network`; use Dokploy's
  Domains tab for routing instead of hard-coding Traefik labels.
- The app publishes host port `3002` to container port `3002` for direct IP
  access. Dokploy's own dashboard can continue using host port `3000`.
- After changing any `NEXT_PUBLIC_*` variable, redeploy so the image is rebuilt.
