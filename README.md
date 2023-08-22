# Skeleton for Documentation Project

## Dependencies
* Python >=3.10
* Python Poetry

## How to use

To create a new documentation project using this skeleton, run the following commands:
```bash
# Clone
git clone 'this-repo-url'

# Update your Python Poetry and install dependencies
poetry self update
poetry install

# Consider updating the dependency versions. Test functionality before releasing.
poetry update
```

## Batteries Included?

This template comes with two plugins: 
* [MkDocs static i18n](https://github.com/ultrabug/mkdocs-static-i18n) for multilanguage
* [MkDocs Awesome Pages](https://github.com/lukasgeiter/mkdocs-awesome-pages-plugin) for page ordering

If you do not have a reason for using multilanguage, you can also delete the dependency `poetry remove 
mkdocs-static-i18n` and remove the plugin from `mkdocs.yml`.

## Need support for multilanguage?

Add the following to the `mkdocs.yml` file:

```yaml
plugins:
  - i18n:
      docs_structure: suffix
      default_language: en
      languages:
        en:
          name: English
          build: true
        fi:
          name: Finnish
          build: true
      # You can translate navigation items here if need be
      nav_translations:
        fi:
          Some Headline: Jokin otsikko
```

Add and install dependency: `poetry add mkdocs-static-i18n`. After this, you are ready to add alternative language files. Check [i18n Docs](https://github.com/ultrabug/mkdocs-static-i18n) for further information.

**NOTE:** You will need to modify the `.pages` files if you are using both Awesome Pages and i18n together. Example below.

```yaml
nav:
    - index.md         # Without i18n
    - ... | index*.md  # With i18n
```

## Run local build

To build the project locally to `site/`, you can simply run `poetry run mkdocs build`

Alternatively, you can run the `poetry run mkdocs serve` command to run live-reloading server.

## Build in GitHub Pages

Merge to `master` branch in any Repository. The scripts at `.github/workflows/` will be executed by Github Actions.

Sadly, GitHub will not automatically publish your Pages as could be expected. You need to visit the **Settings | 
Pages** (at `https://github.com/<username>/<reponame>/settings/pages`). There, under heading **Build and 
deployment**, choose Branch as `gh-pages` and path as `/ (root)`. Click Save. From now on, your Pages should be 
updated whenever you push to master. You should see a workflow with a title *pages build and deployment* in your 
Actions after each push.

## How to access

The URI for the GitHub Pages is `https://<username>.github.io/<repo_name>/`. The *pages build and deployment* 
workflow will output a link to this page.