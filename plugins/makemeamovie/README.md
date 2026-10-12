# Make Me a Movie

Make short films from a written brief without leaving Claude. Make Me a Movie writes the
storyboard, casts the characters, generates keyframes, voices, video clips and music, then
cuts the final film and seals every shot with a provenance manifest you can verify.

This plugin adds two things:

- **The Make Me a Movie connector**, a remote MCP server at `https://api.makemeamovie.app/mcp`.
- **The make-a-film skill and the `film` command**, which teach Claude the order of work:
  check your balance, draft the project, show you a quote, start only after you approve the
  credits, follow the film to the end, and hand you the mp4.

## Before you start

You need a Make Me a Movie account with credits. Sign up at <https://makemeamovie.app>, or
from the sign-in page that opens when you connect. Credits are bought on the website, never
in chat.

## Install

**claude.ai, Claude Desktop and Cowork**

1. Open **Customize > Plugins**, choose **Add > Add marketplace**, and enter
   `mark24680617/makemeamovie-plugin`.
2. Add the **Make Me a Movie** plugin.
3. Open the plugin's **Connectors** tab, add and connect Make Me a Movie, sign in, and approve
   the consent page. On a Team or Enterprise plan, an Owner may need to allow the marketplace
   and add the connector for the organization first.

**Claude Code**

```
claude plugin marketplace add mark24680617/makemeamovie-plugin
claude plugin install makemeamovie@makemeamovie
```

Then run `/mcp` in a session, choose `plugin:makemeamovie:makemeamovie` (or `makemeamovie`, if
you added the server yourself before installing the plugin), and sign in.

## Use it

Ask for a film in plain words, for example: "Make a 30-second film with Make Me a Movie about
a lighthouse keeper who finds a message in a bottle." In Claude Code and Cowork you can also
run `/makemeamovie:film` followed by your brief.

## What it sends and what it costs

- Your brief, your edits and your choices go to Make Me a Movie at
  `https://api.makemeamovie.app/mcp`. To make the film, the service sends prompts and
  reference images to AI providers: OpenAI, Google, ByteDance's Volcano Engine (servers in
  Beijing, China), Alibaba Cloud, and models hosted on Replicate. See the
  [privacy policy](https://makemeamovie.app/privacy).
- Everything made for you (keyframes, clips, the final mp4 and its provenance manifest) is
  stored at an unlisted but publicly accessible URL: anyone who has the link can open it,
  whether or not you share the film. It stays until you delete the project on the website.
- A share page is made only when you ask for one. It stays up until you delete the project on
  the website, and copies people already saved cannot be recalled.
- Making a film spends credits from your account. The plugin has Claude show you a quote and
  ask you to approve the figure before it starts, and the service will not start a film unless
  the approved figure covers the quote. Quotes approved from chat are capped per account per
  day (currently 3,000 credits), and a film can bill a little above its quote when a spoken
  line runs long.
- You can revoke Claude's access at any time under **Connected apps** on your profile page,
  <https://makemeamovie.app/profile/connections>. A film already being made keeps running to
  its quote; ask Claude to stop it first if you want it stopped.

## Links

- How it works, every tool, every price and every error: <https://makemeamovie.app/developers>
- Privacy policy: <https://makemeamovie.app/privacy>
- Terms: <https://makemeamovie.app/terms>
- Support: <markqiu@luqlabs.com>

## License

Copyright 2026 LUQ LABS LLC. Licensed under the Apache License, Version 2.0; see
[LICENSE](LICENSE).

"Make Me a Movie" and its logo are trademarks of LUQ LABS LLC. The license does not grant
permission to use them. This plugin is not made or endorsed by Anthropic.
