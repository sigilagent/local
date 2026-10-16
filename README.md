# local.sigilagent.com

Opens the [Sigil](https://github.com/sigilagent/sigil) Observatory that runs on **your own
machine**, at an address without a port:

```bash
sigil serve start          # the Observatory, on localhost:8199
open https://local.sigilagent.com
```

The page is one static `index.html` served by GitHub Pages. It shows
`http://localhost:<port>/` full-window in a borderless frame, so the address bar keeps
reading `local.sigilagent.com`. Each visitor sees their own machine's agent. Nothing
is sent to this site, and it never sees your agent's data.

- **Another port:** `https://local.sigilagent.com/?port=9000`
- **Sigil not running:** the page says how to start it and keeps checking. The
  Observatory appears on its own once it answers.
- **Browser prompt:** recent Chrome asks once whether this site may reach apps on your
  device. Allow it, or open `http://localhost:8199` directly.

## Security

The Observatory agrees to be framed only by `https://local.sigilagent.com`. Every other
embedder gets a notice instead of the UI (`web/embed_interop.js` in sigilagent/sigil).
Its server listens on loopback only and refuses requests that come from other websites'
pages. This page refuses to be framed itself. When the frame loads, the Observatory
tells this page so with `postMessage`; that's how the page tells a running Sigil from
the browser's error page.

## DNS

`local` is a CNAME to `sigilagent.github.io` at the `sigilagent.com` DNS host.
