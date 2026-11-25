# chatcn Pro

Install chatcn Pro components with the shadcn CLI: sign in, create a license token, add the @chatcn-pro registry to components.json and add items by name. $99 once for every Pro item.

Everything else in these docs is free to use, in personal and commercial projects. chatcn Pro adds on top of it, never instead of it: effects and image reveals, an image studio, credits and billing, chat app widgets, device frames and, as they ship, templates. One payment of $99 covers every Pro item, today and later. See [what is in Pro](https://chatcn.dev/pro).

> Pro pages carry a Pro badge in the sidebar and the components index. Their previews are live for everyone; the source installs only with a license token.

## 1. Sign in

[Sign in](https://chatcn.dev/pro/signin) with the email you bought with: no password, we email you a link and a code. Your license is attached to that email.

## 2. Create a license token

On your [account page](https://chatcn.dev/pro/account), create a token for each machine or CI environment and give it a name you will recognise. The token is shown once. Store it as `CHATCN_PRO_TOKEN` in your project's `.env.local`, never in code.

`.env.local`

```bash
CHATCN_PRO_TOKEN=your-token
```

## 3. Add the registry

Add the @chatcn-pro registry to `components.json`. The CLI reads the token from your environment and sends it with every request, so nothing secret is committed.

`components.json`

```json
{
  "registries": {
    "@chatcn-pro": {
      "url": "https://chatcn.dev/r/pro/{style}/{name}.json",
      "headers": {
        "Authorization": "Bearer ${CHATCN_PRO_TOKEN}"
      }
    }
  }
}
```

## 4. Add items

Install any Pro item by name, the same way as a free one. Pro items pull in the free components they build on.

```bash
npx shadcn@latest add @chatcn-pro/dither-reveal
```

Agents can do the same through the shadcn MCP server once the registry is in `components.json`.

## Tokens and security

- Revoke a token from the account page at any time; installs that use it stop working at once.
- Each token is rate limited, so a leaked token cannot be used to mirror the registry.
- Tokens are stored hashed on the server.
- A 401 from the registry means the token is missing, wrong or revoked: check the variable name and create a new token if needed.

Source: https://chatcn.dev/docs/chatcn-pro