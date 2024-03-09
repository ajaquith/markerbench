# Installation
1. Install Hugo as described in the [Quickstart guide](https://gohugo.io/getting-started/quick-start/)
2. In GitHub, fork the Git repository for the Mediumish theme at `github.com/lgaida/mediumish-gohugo-theme`.
3. Initialize the site with our forked module.

       hugo new site markerbench
       git init
       hugo mod init markerbench
       hugo mod get github.com/ajaquith/mediumish-gohugo-theme
       ...
       (add content)
       ...
       hugo server

4. Modify the template to include author info and favicons properly:

   - [Generate favicons](https://realfavicongenerator.net) using the SVG version of the logo and place into `static/images/favicons`. Create new partials in `layouts/partials/_shared` for `head.html` (which includes a new `favicons.html` partial) and the `favicons.html` partial, which adds meta links for the favicons.
    - Create new partial for the blog article tiles that properly creates the author name and image in `layouts/partials/list-partials/postcard.html`.

# Maintenance

To refresh modules, use `hugo mod get`:

    hugo mod get github.com/ajaquith/mediumish-gohugo-theme

After refreshing, run `hugo mod tidy` to clean up the module hashes in `go.sum`.

Occasionally, upgrade the local versions of Go and Hugo installed on the developer machine, and when the version of Hugo changes:

1. Go to the [current Hugo release](https://github.com/gohugoio/hugo/releases). Note the version of Go in the release notes.
2. Change the value of the `HUGO_VERSION` in `.github/workflows/hugo.yaml` to the correct version.
3. Change the value of the `go` line in `go.mod` to the correct version.
4. Commit and push.

Occasionally, check if GitHub Actions dependent script references in `.github/workflows/hugo.yaml` change; the Actions run will throw errors or warnings. For example, bumping versions for:

- `actions/checkout`
- `actions/configure-pages`
- `actions/upload-pages-artifact`
- `actions/deploy-pages`

See also the GitHub Actions [starter pages](https://github.com/actions/starter-workflows/blob/main/pages/hugo.yml).