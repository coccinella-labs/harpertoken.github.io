<p align="center">
  <img src="https://raw.githubusercontent.com/Coccinella-Labs/harpertoken.github.io/main/.github/assets/thumbnail.png" alt="harpertokengithubio" width="100%">
</p>

# harpertoken public site

[![Website](https://img.shields.io/website?down_color=red&down_message=offline&up_message=online&url=https%3A%2F%2Fcoccinella-labs.github.io%2Fharpertoken.github.io%2F)](https://coccinella-labs.github.io/harpertoken.github.io/)
[![License](https://img.shields.io/github/license/coccinella-labs/harpertoken.github.io)](LICENSE)
[![Last Commit](https://img.shields.io/github/last-commit/coccinella-labs/harpertoken.github.io)](https://github.com/Coccinella-Labs/harpertoken.github.io/commits/main)

# harpertoken.github.io

The public website for coccinella-labs, serving as the organization's landing page and entry point for contributors. The site includes the organization profile, links to GitHub and community platforms, contributor onboarding pages, legal information and Contributor License Agreement, and dynamic content showing recent activity and project status. Built with vanilla HTML, CSS, and JavaScript, with a Cloudflare Worker backend for supporting features.

Status: Live at https://coccinella-labs.github.io/harpertoken.github.io/

## Getting Started

To preview the site locally, clone the repository, navigate to the root directory, and start a simple HTTP server with `python3 -m http.server 8000`. Open http://127.0.0.1:8000 in your browser to view the site. Any changes to HTML, CSS, or JavaScript files will be visible on the next browser refresh.

To deploy changes to the live site, push to the main branch. GitHub Pages automatically publishes the contents of the repository root to the live URL. Changes typically appear within seconds. Pre-commit hooks defined in `.pre-commit-config.yaml` will lint HTML files before committing, catching basic structural issues.

## Site Structure

The repository is organized into five main areas. The root contains static HTML pages: `index.html` is the landing page shown when visitors arrive at the site, `legal.html` contains terms of service and privacy policy, `cla.html` is the Contributor License Agreement page, and `welcome.html` is the welcome flow for first-time contributors. The `assets/` directory holds shared CSS, JavaScript, and image files used across all pages. The `cf-worker/` directory contains a Cloudflare Worker that powers dynamic features like API proxying, activity feeds, and real-time content updates. The `linter/` directory is a simple HTML validation script run as a pre-commit check. The `scripts/` directory holds utility scripts for site maintenance and deployment.

Configuration files include `.pre-commit-config.yaml` for pre-commit hooks, `release-please-config.json` for automated release notes, `POLICY.md` and `COMMAND_POLICY.md` defining organizational policies, and `CHANGELOG.md` tracking changes over time. The `signed.json` file exports the current repository settings for version control and auditing.

## Building the Site

This is a static HTML site with no build step required. All content is served as-is from the repository root. To test locally, run `python3 -m http.server 8000` from the repository root and open http://127.0.0.1:8000. For quick validation before committing, run the linter script at `linter/` to check HTML syntax and structure. The `make` target (if a Makefile exists) may provide shortcuts for common tasks; check the repository for available targets.

The Cloudflare Worker in `cf-worker/` is deployed separately to Cloudflare's network and is not part of the standard build. To develop or deploy the worker, see `cf-worker/wrangler.toml` for its configuration; `wrangler deploy` from `cf-worker/` publishes it, and pushes touching `cf-worker/` also trigger the Deploy Worker workflow. The worker provides features that cannot be implemented with static HTML alone, such as caching strategies, request routing, and dynamic content generation.

## Pages and Content

The landing page at `index.html` introduces the organization, its projects, and links to key resources like GitHub, Docker Hub, and community discussion forums. It includes sections for featured projects, recent releases, and ways to get involved. The legal page at `legal.html` contains the full terms of service and privacy policy in easy-to-read sections. The CLA page at `cla.html` explains the Contributor License Agreement, its purpose, and how to sign it. New contributors can sign the CLA directly from this page using a linked form. The welcome page at `welcome.html` provides a guided onboarding experience for first-time contributors, introducing the organization structure, how to contribute, and how to get help.

Dynamic content sections (like recent activity and project status) are populated by the Cloudflare Worker or client-side JavaScript fetching from GitHub APIs. This allows the site to display live data without requiring rebuilds or deployments. Static content like policy, legal terms, and contributor guides are committed directly to the repository for version control and easy editing.

## Contributing

To contribute to the site, fork the repository, create a feature branch, make changes to HTML or CSS, and open a pull request. Before committing, run `python3 -m http.server` locally to preview your changes. If you are adding new pages, update `index.html` to link to them. For style changes, edit files in `assets/`. For policy or legal updates, edit `POLICY.md`, `COMMAND_POLICY.md`, or `legal.html` directly. Keep changes focused and explain the motivation in your pull request description.

When adding new content, verify that the HTML is valid by running the linter at `linter/`. Ensure that links work correctly and that images have alt text. Test on multiple browsers if possible. For significant changes that affect layout or styling, take screenshots or record a video to include in the pull request.

## Deployment

The site is deployed automatically via GitHub Pages when commits are pushed to the main branch. No manual deployment step is required. The live site is at https://coccinella-labs.github.io/harpertoken.github.io/. Custom domain setup (if desired) would be configured in GitHub repository settings.

For the Cloudflare Worker, deployment runs automatically through the Deploy Worker workflow when `cf-worker/` changes on main; `wrangler deploy` from `cf-worker/` also works for manual deploys. Changes to the worker do not affect the static site; they enhance features that require backend support.

If you need to rollback a change, revert the commit on main, and GitHub Pages will re-publish the previous version. There is no separate staging environment; changes go live immediately upon merge to main.

## Known Limitations

This is a static HTML site with no server-side rendering or databases. All content must be committed to the repository. Large datasets or frequently updated content should be served via APIs (like GitHub's public APIs) rather than embedded in HTML. The site does not support user accounts, login, or personalized content; all visitors see the same pages.

The Cloudflare Worker provides some dynamic capabilities, but it is limited to edge computing tasks. Complex operations like database queries or authentication should be handled by separate backend services. The site does not have a CMS (content management system), so content updates require git commits and code review. This is intentional for audit and quality control but may slow down rapid updates.

Browser compatibility is assumed to be modern (Chrome, Firefox, Safari, Edge). Internet Explorer and very old browsers are not supported. The site is designed to be mobile-responsive but should be tested on a range of devices to ensure usability.

## Performance

The site is static HTML and CSS, so it loads very quickly. GitHub Pages serves content from a global CDN, so latency is minimized for users worldwide. The Cloudflare Worker adds a small amount of latency for dynamic content but uses caching to minimize impact. For static pages without dynamic content, first load is typically under 500ms from most regions.

Lighthouse scores for performance, accessibility, and SEO should be checked regularly. Use the Lighthouse tool in Chrome DevTools to profile the site and identify optimization opportunities. Keep JavaScript minimal and defer non-critical scripts to avoid blocking page load.

## Architecture

The site follows a simple architecture: static HTML pages and CSS are served from GitHub Pages, with optional JavaScript running in the browser for interactivity. The Cloudflare Worker sits in front and handles caching, request routing, and API proxying. Dynamic content like recent activity is fetched client-side using JavaScript, avoiding the need to rebuild and redeploy when data changes.

The separation of concerns keeps the site maintainable: static content is edited in the repository, styling is managed in `assets/`, interactivity is added with JavaScript, and backend features are handled by the Cloudflare Worker. Each layer is independent, so changes to one do not require rebuilding others.

## Roadmap

Planned improvements include adding a blog section to share project updates and announcements, integrating with GitHub Discussions to display community conversations on the site, and building a project showcase with interactive demos. Better accessibility and internationalization (multiple languages) are also under consideration. See GitHub Issues for the full roadmap.

## Legal

MIT License. See LICENSE file for full terms. The site includes legal pages (terms of service, privacy policy, CLA) that are specific to the coccinella-labs organization and should be reviewed by legal counsel before making changes.

## Related Repositories

This site represents the public face of coccinella-labs. See Harper for the AI agent runtime, Vision for image analysis, HarperBot for PR code review automation, Core for GPU benchmarking, GPUComm-FS for artifact storage, GPUComm-Bot for CI automation, ML for distributed training, and .github for organization configuration. All of these projects are linked from the landing page.

## Contact

Questions about the website or its content? Open an issue in this repository or contact the organization maintainers.
