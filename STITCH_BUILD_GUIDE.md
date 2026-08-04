# Ruhaniyat Website Build Guide

This guide documents how the Ruhaniyat website was built from the first Stitch screen export through local wiring, interactivity, deployment, and final polish.

## 1. Set up VS Code for Stitch MCP

1. Open the project in VS Code.
2. Create or edit the MCP configuration at [.vscode/mcp.json](.vscode/mcp.json).
3. Register Stitch as an HTTP MCP server.
4. Point the server URL to the Stitch endpoint used by the workspace.
5. Add the API key header required by the Stitch service.
6. Reload VS Code so the MCP server appears in Copilot/agent tooling.

The repo's MCP wiring lives in [.vscode/mcp.json](.vscode/mcp.json). Keep the key private and store only what is needed for the local VS Code session.

## 2. Generate the initial screens in Stitch

1. Open Stitch from VS Code using the MCP connection.
2. Prompt Stitch to generate the desired editorial site screens.
3. Export the main pages as separate HTML screens.
4. Export screenshots for design reference.
5. Export any required content images from the generated screens.

In this project, the generated assets were grouped by page under `stitch/`, including:

- [stitch/home/ruhaniyat-home.html](stitch/home/ruhaniyat-home.html)
- [stitch/archive/archive.html](stitch/archive/archive.html)
- [stitch/philosophy/philosophy.html](stitch/philosophy/philosophy.html)
- [stitch/essays/essays.html](stitch/essays/essays.html)
- [stitch/categories/categories.html](stitch/categories/categories.html)
- [stitch/article-template/article-template.html](stitch/article-template/article-template.html)
- [stitch/search/search.html](stitch/search/search.html)
- [stitch/connect/connect.html](stitch/connect/connect.html)

## 3. Save the exported Stitch assets

1. Keep each screen in its own folder.
2. Store its screenshot beside the HTML.
3. Store page-specific images in a local `images/` folder inside that page directory.
4. Keep a manifest file for each screen so the asset mapping stays explicit.

Example manifest files in the repo:

- [stitch/archive/manifest.json](stitch/archive/manifest.json)
- [stitch/philosophy/manifest.json](stitch/philosophy/manifest.json)
- [stitch/essays/manifest.json](stitch/essays/manifest.json)

For the home screen, the asset summary is recorded in [stitch/images/STITCH_ASSETS.md](stitch/images/STITCH_ASSETS.md).

## 4. Fix the exported HTML for real site use

Stitch exports are a starting point, not the final site. The exported pages were edited to make them work as a real navigation system.

1. Replace placeholder links with real routes.
2. Normalize image paths so the HTML points to local files.
3. Create missing folders when the export references images that do not exist yet.
4. Remove broken filename suffixes or mismatched asset names.
5. Keep the visual design intact while making the file paths valid.

The main working pages live under the `stitch/` folder and are served directly as static HTML.

## 5. Wire the pages together

1. Add consistent navigation links across every page.
2. Make the archive, journeys, essays, visuals, search, and contact pages link to each other.
3. Make the article template reachable from archive cards, essays, and search results.
4. Add root-level entry points so the site works when published as a static root.

Important routing files:

- [stitch/index.html](stitch/index.html)
- [stitch/404.html](stitch/404.html)
- [stitch/home/index.html](stitch/home/index.html)

## 6. Add page behavior with JavaScript

The site is static HTML, so the interactivity is handled inline in each page.

### Archive page

1. Filter cards by category.
2. Toggle the filter buttons visually.
3. Keep the "Load Older Entries" control as a client-side interaction.

### Article template

1. Add share support with the Web Share API.
2. Provide a clipboard fallback if sharing is unavailable.
3. Store bookmarks in `localStorage`.
4. Show feedback with a toast message.

### Search page

1. Handle query-string search input.
2. Page through results.
3. Wire next, previous, and page-number controls.

### Contact page

1. Validate required fields.
2. Validate email format.
3. Show a success or error message after submission.

## 7. Fix the active navbar state

The original export used a hardcoded underline on the archive link.
That meant the active state did not move when the user changed pages.

The fix was:

1. Add a small script to each page after the closing `</nav>` tag.
2. Read `window.location.pathname`.
3. Find all `nav a[href]` links.
4. Apply the active underline class only to the matching section page.
5. Render utility pages like search and contact with inactive navigation styling.

This logic was added across the main pages, including:

- [stitch/home/ruhaniyat-home.html](stitch/home/ruhaniyat-home.html)
- [stitch/archive/archive.html](stitch/archive/archive.html)
- [stitch/philosophy/philosophy.html](stitch/philosophy/philosophy.html)
- [stitch/essays/essays.html](stitch/essays/essays.html)
- [stitch/categories/categories.html](stitch/categories/categories.html)
- [stitch/article-template/article-template.html](stitch/article-template/article-template.html)
- [stitch/search/search.html](stitch/search/search.html)
- [stitch/connect/connect.html](stitch/connect/connect.html)

## 8. Add the root redirect and deploy targets

1. Point the published root at the Stitch folder.
2. Keep a root redirect so the entry page lands on the home screen.
3. Provide a 404 fallback that returns to the home page.
4. Configure GitHub Pages to deploy the `stitch/` folder.

The GitHub Pages workflow is defined in [.github/workflows/pages.yml](.github/workflows/pages.yml).

## 9. Commit and push the site

1. Stage the finished site files.
2. Commit the UI and interaction updates.
3. Push to the remote repository.
4. Let the host redeploy automatically.

The site was also deployed to Netlify as a static publish folder using `stitch/`.

## 10. Verify the live site

1. Open the home page.
2. Click each main nav item.
3. Confirm the underline moves to the current page.
4. Check that images load on every page.
5. Verify archive filters, share/bookmark actions, search pagination, and the contact form.

## 11. Recommended build order for a new project

If you want to recreate the same process from scratch, use this order:

1. Connect Stitch MCP in VS Code.
2. Generate the screens in Stitch.
3. Export HTML, screenshots, and images.
4. Organize each page into its own folder under `stitch/`.
5. Fix image paths and route links.
6. Add shared navigation.
7. Add page-specific JavaScript interactions.
8. Fix the active nav state.
9. Add root entry points and 404 handling.
10. Configure GitHub Pages or Netlify.
11. Push, deploy, and test the live site.

## 12. Notes from this project

- The site is intentionally static and does not use a build pipeline.
- Tailwind is loaded from the CDN in each page.
- Google Fonts provide the visual identity.
- Local JavaScript handles the behavior that a framework would normally own.
- Page structure matters because static hosting depends on correct relative paths.
