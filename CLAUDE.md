# OptiDev Documentation Site

User-facing documentation for docs.optidev.ai. Built with Mintlify.

## Writing Guidelines

- Helpful, optimistic, concise
- Minimalist style, no fluff, no jargon
- 80% for business users (analysts, marketers) who know SQL but not code
- Focus on: "the agent builds it for you" and "click here in Dashboard"
- End each page with "For Developers" section for technical reference

## Directory Structure

```
docs/
├── docs.json            # Navigation, theme, branding config
├── index.mdx            # Landing page
├── get-started/         # Onboarding
│   ├── quickstart.mdx   # First project walkthrough
│   ├── prompt-guide.mdx # How to write good prompts
│   └── prompt-library.mdx # Example prompts by category
├── features/            # Platform capabilities
│   ├── agent-mode.mdx   # AI assistant (5 modes)
│   ├── visual-editor.mdx # Point-and-click editing
│   ├── code-editor.mdx  # VS Code in browser
│   ├── image-generation.mdx # AI image creation
│   ├── publish-your-app.mdx # Build and deploy
│   ├── custom-domain.mdx # DNS setup
│   └── publish-to-optisigns.mdx # Digital signage
├── optidev-cloud/       # Backend-as-a-service
│   ├── how-to-use.mdx   # Activation and overview
│   ├── database.mdx     # PostgreSQL access
│   ├── edge-functions.mdx # Serverless functions
│   ├── storage.mdx      # File storage
│   └── auth.mdx         # User authentication
├── security/            # Enterprise features
│   ├── securing-your-app.mdx # Best practices
│   ├── single-sign-on.mdx # SSO overview
│   ├── sso-okta.mdx     # Okta setup guide
│   └── sso-azure-ad.mdx # Azure AD setup guide
├── billing/             # Plans and payments
│   ├── plans-and-credits.mdx # Pricing tiers
│   └── payment-methods.mdx # Stripe integration
├── images/              # Static images for docs
├── logo/                # Brand assets
├── snippets/            # Reusable MDX snippets
└── claude-dev/          # Development notes (not published)
```

## Local Development

```bash
npm run dev  # localhost:3009
```

## Deployment

Push to `main` → auto-deploys to docs.optidev.ai

## Key Files

| File | Purpose |
|------|---------|
| `docs.json` | Navigation structure, colors, navbar links |
| `index.mdx` | Homepage hero and feature cards |

## Reference

- [Mintlify Docs](https://mintlify.com/docs) - Use Context7 MCP for lookup
- Main product: `~/optisigns/optiedge/optiedge-develop`
