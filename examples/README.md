# Examples

Examples show completed section 0 inputs and the tailoring expected from the
setup prompt. They are not generated repositories and should not be copied as
architecture without checking the target project's requirements.

- [`minimal/`](minimal/) — a local-only command-line tool that should not acquire
  cloud infrastructure merely because the prompt supports it.
- [`cloudflare-web-app/`](cloudflare-web-app/) — a production-oriented web app
  that requires capability analysis before selecting Cloudflare state products.

Each example intentionally states risk, physical use, data growth, delivery
target, and prompt provenance. Those fields produce more useful project
decisions than a framework name alone.
