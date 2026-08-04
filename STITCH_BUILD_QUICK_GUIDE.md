# Ruhaniyat Quick Build Guide

Use this as the short version of the full build process.

## 1. Connect Stitch to VS Code

1. Open the project in VS Code.
2. Add the Stitch MCP server in [.vscode/mcp.json](.vscode/mcp.json).
3. Reload VS Code so Stitch is available through Copilot tools.

## 2. Generate the UI in Stitch

1. Ask Stitch to create the main editorial screens.
2. Export each screen as HTML and screenshot files.
3. Export the page images used in the design.

## 3. Organize the exported files

1. Keep each page in its own folder under `stitch/`.
2. Save screenshots next to each page HTML.
3. Save images in the page-specific `images/` folder.
4. Record the export details in a manifest file.

## 4. Fix the HTML exports

1. Replace placeholder links with real page routes.
2. Correct broken image paths and missing folders.
3. Make sure each page points to local assets.

## 5. Wire the pages together

1. Add the same nav bar to every page.
2. Link home, archive, journeys, essays, visuals, search, and contact.
3. Add the article template links from cards and search results.

## 6. Add page behavior

1. Filter archive cards with JavaScript.
2. Add share and bookmark actions on article pages.
3. Add search pagination.
4. Validate the contact form.

## 7. Fix active navbar highlighting

1. Read `window.location.pathname` on page load.
2. Compare it to each nav link.
3. Add the underline only to the current page.
4. Keep utility pages like search and contact inactive.

## 8. Add root files and deploy

1. Keep [stitch/index.html](stitch/index.html) as the root redirect.
2. Keep [stitch/404.html](stitch/404.html) as the fallback.
3. Deploy the `stitch/` folder with GitHub Pages or Netlify.

## 9. Final checks

1. Open every page.
2. Confirm images load.
3. Confirm the navbar underline moves.
4. Confirm the buttons and form actions work.
