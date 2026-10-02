# CI/CD Workflows

The four workflows in `.github/workflows/` call the shared ones in
[palasthotel/github-workflows](https://github.com/palasthotel/github-workflows). How
they work, every input and what to do when a deploy fails is described there, in
[docs/wp-plugin.md](https://github.com/palasthotel/github-workflows/blob/main/docs/wp-plugin.md).

What is specific to this plugin:

| | |
|---|---|
| wordpress.org slug | `postqueue-feeds` |
| version file | `version.txt` (`release-type: simple`) - there is no `package.json` |
| build step | none - plain PHP, no assets, no dependencies |
| main file | `public/postqueue-feeds-plugin.php` - must keep its name, see [CONTRIBUTING.md](../CONTRIBUTING.md) |
| development wrapper | `postqueue-feeds-dev.php`, `Plugin Name: Postqueue Feeds (DEV)` - the PR check fails if it ends up in the payload |
| SVN `assets/` | empty in SVN and absent here, so the deploy leaves it alone; whoever adds a banner adds `assets/` to this repository |

The development wrapper is not a version carrier and nothing syncs it. It never ships,
so its header version means nothing.

### Required repository configuration

Set for the organization and released to this repository: the variable
`RELEASE_BOT_APP_ID` and the secrets `RELEASE_BOT_PRIVATE_KEY`, `SVN_USERNAME` and
`SVN_PASSWORD`. The variable `SVN_REPO_URL` is no longer read and can be deleted.
