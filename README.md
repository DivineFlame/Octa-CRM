# OctaCRM

<p align="center">
  <img src="./public/octacrm-logo.png" alt="OctaCRM logo" width="360">
</p>

OctaCRM is a self-hostable WhatsApp CRM built with Next.js and Supabase. It
includes a shared inbox, contacts, pipelines, broadcasts, automations, team
accounts, public API keys, and an AI reply assistant.

## Stack

- **App**: Next.js 16, React 19, TypeScript, Tailwind CSS
- **Data**: Supabase Postgres, Auth, Storage, and RLS
- **Messaging**: Meta WhatsApp Cloud API
- **Deployment**: Docker Compose for Dokploy

## Quick Start

```bash
git clone https://github.com/DivineFlame/Octa-CRM.git
cd Octa-CRM
npm install
cp .env.local.example .env.local
npm run dev
```

Open <http://localhost:3000>. You will be redirected to `/login`, or
`/dashboard` if already signed in.

## Environment

Fill these values before deploying:

```env
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-or-publishable-key
SUPABASE_SERVICE_ROLE_KEY=your-service-role-or-secret-key
ENCRYPTION_KEY=your-64-character-hex-key
META_APP_SECRET=your-meta-app-secret
NEXT_PUBLIC_SITE_URL=http://38.247.188.228:3002
NEXT_PUBLIC_APP_LOCALE=en
```

Optional variables are documented in [.env.local.example](./.env.local.example).

## Deploy on Dokploy

This repo includes a Dokploy-ready Docker deployment:

- [Dockerfile](./Dockerfile) builds the app as a Next.js standalone server.
- [docker-compose.yml](./docker-compose.yml) publishes host port `3002` to
  container port `3002`.
- [docs/deployment-dokploy.md](./docs/deployment-dokploy.md) lists Dokploy
  setup steps and deployment notes.

For direct IP access after deployment, open TCP port `3002` on the server and
visit:

```text
http://38.247.188.228:3002
```

## Documentation

- [Dokploy deployment](./docs/deployment-dokploy.md)
- [Public API](./docs/public-api.md)
- [Automations and cron](./docs/automations-and-cron.md)

## License

[MIT](./LICENSE).
