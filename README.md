# Make Me a Movie plugin marketplace

This repository is the plugin marketplace for [Make Me a Movie](https://makemeamovie.app). It
holds one plugin, [makemeamovie](plugins/makemeamovie), which lets Claude make short films
from a written brief: storyboard, cast, keyframes, voices, clips, music and a final cut, each
shot sealed with a provenance manifest. Read the
[plugin's README](plugins/makemeamovie/README.md) for what it does, what it sends, and what it
costs.

## Install

**claude.ai, Claude Desktop and Cowork:** open **Customize > Plugins**, choose
**Add > Add marketplace**, enter `mark24680617/makemeamovie-plugin`, add the **Make Me a Movie**
plugin, then add and connect Make Me a Movie from the plugin's **Connectors** tab.

**Claude Code:**

```
claude plugin marketplace add mark24680617/makemeamovie-plugin
claude plugin install makemeamovie@makemeamovie
```

Support: <markqiu@luqlabs.com>

## License

Copyright 2026 LUQ LABS LLC. Licensed under the Apache License, Version 2.0; see
[LICENSE](LICENSE). "Make Me a Movie" and its logo are trademarks of LUQ LABS LLC; the license
does not grant permission to use them. This plugin is not made or endorsed by Anthropic.
