# scalhive-content

The intent of this repository is to develop the content of the scalhive organization's website using the Hugo framework.

## Useful links:

- [Hugo documentation](https://gohugo.io/documentation)
- [Hugo Installation](https://gohugo.io/installation/)
- Theme - [scalhive-theme](https://github.com/TNTU-RS-internship/scalhive-theme.git)
- [Hugo docker images](https://hub.docker.com/r/klakegg/hugo)
- [Hugo Internal Templates](https://github.com/gohugoio/hugo/tree/master/tpl/tplimpl/embedded/templates)
- [Hugo themes](https://themes.gohugo.io/)
- [Tachyons documentation](http://tachyons.io/docs/)
- [Tachyons color codes](https://tachyons.io/docs/themes/skins/) for base theme
- Blogpost - [Image processing using hugo](https://clavinjune.dev/en/blogs/image-processing-using-hugo/)
- Blogpost - [Multilingual](https://www.regisphilibert.com/blog/2018/08/hugo-multilingual-part-1-managing-content-translation/)
- [Go text template](https://pkg.go.dev/text/template)
- Article [Add Contact form to Hugo with Google forms](https://blog.puvvadi.me/posts/add-contact-form-hugo-google-forms/)
- [Add-ons for Hugo](https://hugocodex.org/add-ons/) - Extend Hugo’s functionality

## [Hugo Installation](https://gohugo.io/installation/)

### Prerequisites

- [Git](https://git-scm.com/)
- [Go](https://go.dev/)
- [Dart Sass](https://gohugo.io/hugo-pipes/transpile-sass-to-css/#dart-sass)

Git is required to:

- Build Hugo from source 
- Use the Hugo Modules feature 
- Install a theme as a Git submodule 
- Access commit information from a local Git repository 
- Host your site with services such as CloudCannon, Cloudflare Pages, GitHub Pages, GitLab Pages, and Netlify

Go is required to:

- Build Hugo from source
- Use the Hugo Modules feature

Dart Sass is required to transpile Sass to CSS when using the latest features of the Sass language.

#### Check if the tools are installed

```shell
git version
go verison
```

If you'll install Hugo as a [Snap package](https://gohugo.io/installation/linux/#snap) - there is no need to install Dart Sass. 
The Hugo Snap package includes Dart Sass.

Installation instructions:
- [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Go](https://go.dev/doc/install)
- [Dart Sass](https://gohugo.io/hugo-pipes/transpile-sass-to-css/#dart-sass)

### [Hugo Linux Installation](https://gohugo.io/installation/linux/)

Snap:
```shell
sudo snap install hugo
```

Homebrew:
```shell
brew install hugo
```

Check if Hugo are installed correctly:
```shell
hugo version
```

## Deploy
Website is deploying automatically using `GitHub Actions` and two GitHub environments: 
- `development` for build site in `DEV` hugo environment and deploy it into development hosting. Contains necessary 
environment variable `DEV_BASE_URL` and secrets to connect with FTP-server - `FTP_SERVER`, `FTP_USERNAME` and `FTP_PASSWORD`.
- `production` for deploy into GitHub Pages job.

There are two versions of website - `development` and `production`.
- Development version of site deploys into url, that defined in `DEV_BASE_URL` variable.
- Production version of site deploys into GitHub Pages on url https://fantastic-engine-z4g5o6k.pages.github.io/ 
(Generated automatically by GitHub)

Website from `main` branch GitHub Actions builds using Hugo with `production` environment (HUGO_ENV=production)
and deploys this website into GitHub Pages.

Website from `dev` branch GitHub Actions builds using Hugo with `DEV` environment (HUGO_ENV=DEV) and deploys 
this website into https://dev.scalhive.com, using [SamKirkland/FTP-Deploy-Action](https://github.com/SamKirkland/FTP-Deploy-Action).
For this there are 3 secrets in environment GitHub `deployment`.

For local deploy use command:
```shell
docker-compose up
```
The site will be available at http://localhost:1313.

## Repository structure

Directory tree:
```
scalhive-content/
├── .github/
│   └── workflows/
│       └── hugo.yml
├── archetypes/
│   └── default.md
├── assets/
├── content/
├── config/           <-- site configuration
│   └── _default/
│   │   └── hugo.toml
│   └── production/
│       └── hugo.toml
├── data/
├── static/
├── .gitmodules
├── go.mod
├── docker-compose.yml
└── README.md
```

### Directories and files

Each of the subdirectories contributes to the content, structure, behavior, or presentation of site.

**.github/workflows/**

Includes workflow definition `hugo.yml` for repository that build and deploy site.

**archetypes/**

The `archetypes` directory contains templates for new content. 
See [details](https://gohugo.io/content-management/archetypes/).

**assets/**

The `assets` directory contains global resources typically passed through an asset pipeline. 
This includes resources such as images, CSS, Sass, JavaScript, and TypeScript. 
See [details](https://gohugo.io/hugo-pipes/introduction/).

**config/**

The `config` directory contains site configuration, possibly split into multiple subdirectories and files.
See [details](https://gohugo.io/getting-started/configuration/#configuration-directory). In this project there are two directories with configurations - `_default` and 
`production`. Production configuration overrides default configuration, when site builds in `production` 
environment (HUGO_ENV=production).

**content/**

The `content` directory contains the markup files and page resources that comprise the content of site. 
See [details](https://gohugo.io/content-management/organization/).

**data/**

The `data` directory contains data files (JSON, TOML, YAML, or XML) that augment content, configuration, localization, 
and navigation. See [details](https://gohugo.io/templates/data-templates/).

**static/**

The `static` directory contains files that will be copied to the public directory when you build your site. For example: 
`favicon.ico`, `robots.txt`, and files that verify site ownership. 
Before the introduction of [page bundles](https://gohugo.io/getting-started/glossary/#page-bundle) and 
[asset pipelines](https://gohugo.io/hugo-pipes/introduction/), the static directory was also used for 
images, CSS, and JavaScript. See [details](https://gohugo.io/content-management/static-files/).

**.gitmodules**

Include definition of [theme](https://github.com/TNTU-RS-internship/scalhive-theme) submodule

**go.mod**

Include go version and defines the version of [theme](https://github.com/TNTU-RS-internship/scalhive-theme) submodule

**docker-compose.yml**

File that used to deploy site locally at http://localhost:1313.

**README.md**

This file.

## Multilingual

Each markdown file that represent separate site page must have appropriation in each site language, otherwise language
button won't be presented in Menu. If some page isn't translated to other language, please for empty markdown files use
below text as page content.

For English
```text
Unfortunately, the page is not translated into this language.
```

For Ukrainian
```text
На жаль, сторінка не перекладена на цю мову.
```

## Images locations

Images could be stored in two places: `/static/` or `/assets/` folders.
- use `/assets/` folder for images which will be presented in page `main` section (images will be rendered by build);
- use `/static/` folder for background images specified in CSS code `{ background: url(""); }` 
(banner and header images) and for images which will be used for sharing but not presented on the site anywhere
(such images won't be rendered by build).

## Tagging policy

Versions in the "v0.1.2" format are marked with tags, where:
- the first number - displays the main version;
- the second number - displays a large feature (for example, adding a new page for the site);
- the third number - displays hotfix.

The latest commit after the pull request is tagged with the new version.
Depending on the issue, either the second number (a large feature was added) or the 
third number (a hotfix was made) changes.

## Release policy

Before creating a release, a milestone with the name of the corresponding `future version` is created. This milestone
include issues that need to be completed to create a new version.

After the milestone is completed, a new pull request is created to complete the `merge` operation
from `dev` branch to `main` branch. The merge commit that will be created is tagged with the new version.

Based on this new milestone version, a release titled `scalhive-content <tag>` has been created,
where `<tag>` is the tag corresponding to the completed milestone version. Also, this release is marked as `latest`.

## Update theme policy

To update the version of the `scalhive-theme submodule`, a corresponding issue must be created (which can be added as 
a task in a larger issue). This issue must have the label `update`. 

The main task of this specific issue is to change the version of the scalhive-theme submodule to a new one in file 
`/go.mod`. Changes may also be added to configuration/content files to apply new changes of scalhive-theme module.
