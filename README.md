# WordPress.org Plugin Build Zip Archive

> Build a zip archive of your WordPress.org plugin using GitHub Actions.

[![Support Level](https://img.shields.io/badge/support-active-green.svg)](#support-level) [![Release Version](https://img.shields.io/github/release/10up/action-wordpress-plugin-build-zip.svg)](https://github.com/10up/action-wordpress-plugin-build-zip/releases/latest) [![MIT License](https://img.shields.io/github/license/10up/action-wordpress-plugin-build-zip.svg)](https://github.com/10up/action-wordpress-plugin-build-zip/blob/develop/LICENSE)

This Action will build a zip archive of your WordPress plugin and attach that archive as an artifact, allowing you to download and test prior to deploying any changes to WordPress.org. This gives you the peace of mind knowing you've tested exactly what will be deployed.

Recommended to be used in conjunction with our [WordPress.org Plugin Deploy Action](https://github.com/10up/action-wordpress-plugin-deploy) as both Actions create the archive in the same way. An ideal workflow is to run this Action first and test the zip archive it provides. Once testing passes, then run our deploy Action to push changes to WordPress.org.

**Note**: while this Action will checkout your plugin code from the WordPress.org SVN repo it does not commit any code to that repo.

### ☞ Check out our [collection of WordPress-focused GitHub Actions](https://github.com/10up/actions-wordpress)

## Configuration

### Optional environment variables

* `SLUG` - defaults to the repository name, customizable in case your WordPress.org repository has a different slug or is capitalized differently.
* `BUILD_DIR` - defaults to `false`. Set this flag to the directory where you build your plugins files into, then the action will copy and build the archive from that directory. Both absolute and relative paths are supported. The relative path if provided will be concatenated with the repository root directory. All files and folders in the build directory will be archived, `.distignore` or `.gitattributes` will be ignored.

### Inputs

* `retention-days` - How many days should the zip archive be kept. Defaults to 5.

## Excluding files from the archive

If there are files or directories to be excluded from the archive, such as tests or editor config files, they can be specified in either a `.distignore` file or a `.gitattributes` file using the `export-ignore` directive. If a `.distignore` file is present, it will be used; if not, the Action will look for a `.gitattributes` file and barring that, will write a basic temporary `.gitattributes` into place before proceeding so that no Git/GitHub-specific files are included.

The recommened approach is to use a `.distignore` file, especially when there are built files that are in `.gitignore` that should be in the final archive. `.gitattributes` is useful for plugins that don't run a build step as a part of the Actions workflow and also allows for GitHub's generated ZIP files to contain the same contents as what is committed to WordPress.org.

### Sample baseline files

#### `.distignore`

**Notes:** `.distignore` is for files to be ignored **only**; it does not currently allow negation like `.gitignore`. This comes from its current expected syntax in WP-CLI's [`wp dist-archive` command](https://github.com/wp-cli/dist-archive-command/). It also will need to contain more than `.gitattributes` because that method **also** respects `.gitignore`.

```
/.wordpress-org
/.git
/.github
/node_modules

.distignore
.gitignore
```

#### `.gitattributes`

```gitattributes
# Directories
/.wordpress-org export-ignore
/.github export-ignore

# Files
/.gitattributes export-ignore
/.gitignore export-ignore
```

## Example Workflow Files

To get started, you will want to copy the contents of one of these examples into `.github/workflows/build-zip.yml` and push that to your repository. You are welcome to name the file something else, but it must be in that directory. The usage of `ubuntu-latest` is recommended for compatibility with required dependencies in this Action.

### Build zip on pushes to trunk

```yml
name: Build release zip

on:
  push:
    branches:
    - trunk

jobs:
  build:
    name: Build release zip
    runs-on: ubuntu-latest
    steps:
    - name: Checkout
      uses: actions/checkout@v4

    - name: Build plugin # Remove or modify this step as needed
      run: |
        composer install --no-dev
        npm install
        npm run build

    - name: Generate zip
      uses: 10up/action-wordpress-plugin-build-zip@stable
      env:
        SLUG: my-super-cool-plugin # optional, remove if GitHub repo name matches SVN slug, including capitalization
```

### Build zip on demand and keep that for 1 day

```yml
name: Build release zip

on:
  workflow_dispatch

jobs:
  build:
    name: Build release zip
    runs-on: ubuntu-latest
    steps:
    - name: Checkout
      uses: actions/checkout@v4

    - name: Build plugin # Remove or modify this step as needed
      run: |
        composer install --no-dev
        npm install
        npm run build

    - name: Generate zip
      uses: 10up/action-wordpress-plugin-build-zip@stable
      with:
        retention-days: 1 # Optional; defaults to 5
```

## Contributing

Want to help? Check out our [contributing guidelines](CONTRIBUTING.md) to get started.

## License

Our GitHub Actions are available for use and remix under the MIT license.

## Support Level

**Active:** 10up is actively working on this, and we expect to continue work for the foreseeable future including keeping tested up to the most recent version of WordPress.  Bug reports, feature requests, questions, and pull requests are welcome.

## Like what you see?

[![Work with 10up](https://10up.com/uploads/2016/10/10up-Github-Banner.png)](http://10up.com/contact/)
