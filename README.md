# OAuth Flow Explorer

An interactive, static guide to the OAuth 2.0 Authorization Code flow with PKCE and the OpenID Connect layer. Follow requests step by step, inspect realistic (fabricated) messages, and select parameters to trace how they are generated, transmitted, stored, and checked.

The explorer compares three client/provider setups:

- **Rails confidential client** — Rails redeems the code over a back channel and authenticates with a server-side client secret.
- **Browser-only SPA** — a public client uses PKCE and redeems the code in the browser; it has no usable client secret.
- **Multi-tenant provider** — a connection-specific tenant selects a pinned issuer and tenant-specific endpoints/keys before the authorization redirect.

## Run locally

Requires Node.js 20 or newer.

```sh
npm install
npm run dev
```

Open the local URL printed by Vite. To build and preview the production bundle:

```sh
npm run build
npm run preview
```

## Deploy to GitHub Pages

1. Push this project to a GitHub repository, with the default branch named `main` (or edit `.github/workflows/deploy.yml` to match your branch).
2. In the repository settings, open **Pages** and set the build and deployment source to **GitHub Actions**.
3. Push a change to `main`, or run **Deploy static site to GitHub Pages** from the Actions tab.
4. Open the Pages URL shown in the workflow deployment.

The workflow builds with Vite and publishes `dist/`. Vite's base path is configured for the repository name `OAuth_visualization`; if you use a different repository name, update `vite.config.ts` to that path (for example, `/my-repo/`). For a user or organization site served from the domain root, use `/`.

## Technical scope

The example values are fictional and the page has no OAuth client credentials, server, API calls, cookies, or sign-in operation. It is an educational simulation. It illustrates OAuth 2.0 authorization code with PKCE (`S256`) and separately identifies OpenID Connect behavior such as `openid`, `nonce`, ID tokens, issuer metadata, and identity-token validation. Provider endpoint names, client authentication methods, consent behavior, CORS support, and token formats vary; the wire samples are representative, not a promise of any particular provider's implementation.

For a production client, use current OAuth security guidance, exact registered redirect URIs, cryptographically secure transaction values, TLS, trusted issuer metadata, robust callback error handling, and appropriate token/session storage. A tenant identifier is configuration, not a credential; bind each connection to the expected issuer and its trusted keys.
