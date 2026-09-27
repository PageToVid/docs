# PageToVid documentation

The source of **https://pagetovid.github.io/docs/** — guides, the MCP server reference and best
practices for [PageToVid](https://pagetovid.com).

- Built by **GitHub Pages** from `main` (Jekyll, [Just the Docs](https://just-the-docs.com) theme).
- `mcp/tools.md` and `mcp/instructions.md` are **generated** from the MCP server
  (`scripts/gen-mcp-docs.mts` in the product repository) — do not edit them by hand.
- Screenshots live in `assets/screens/`, film frames in `assets/films/`.

## Preview locally

```bash
gem install bundler jekyll
bundle init && bundle add github-pages --group jekyll_plugins
bundle exec jekyll serve --baseurl /docs
```

Found something wrong? Use **Edit this page on GitHub** at the bottom of any page, or
[open an issue](https://github.com/PageToVid/docs/issues/new/choose).

© PageToVid
