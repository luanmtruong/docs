# Kobiton Docs contributors guide

Thanks for contributing to Kobiton Docs!
This guide covers how content for [docs.kobiton.com](https://docs.kobiton.com/) is created, organized, and published. Everyone here is expected to adhere to the [Code of Conduct](CODE_OF_CONDUCT.md) so be sure to review before contributing.

If you're new to docs-as-code, start with [First time contributors](#first-time-contributors), otherwise choose a topic below:

## Table of contents

- [First time contributors](#first-time-contributors)
- [Build the docs locally](#build-the-docs-locally)
- [Antora logs](#antora-logs)
- [Antora playbooks and UI bundles](#antora-playbooks-and-ui-bundles)
- [Directory structure](#directory-structure)
- [Site navigation](#site-navigation)
- [Site URLs](#site-urls)
- [Hide a page from search](#hide-a-page-from-search)
- [Partials](#partials)
- [Directory and file names](#directory-and-file-names)
- [Page types and templates](#page-types-and-templates)
- [Style and voice](#style-and-voice)
- [Docker commands](#docker-commands)

## First time contributors

Our docs are managed as docs-as-code, meaning each document is a plain text file stored in a version-controlled repository. Learn more about each topic below:

### Version control

Version control allows our team to work on documents simultaneously without accidentally overwriting each other's work.

- [Learn about Git and GitHub](https://docs.github.com/en/get-started/using-git/about-git)
- [Get started with GitHub](https://docs.github.com/get-started/quickstart/hello-world)
- [Your first pull request](https://docs.github.com/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)

### File types and markup language

Our document files are written in a plain text markup language and only contain written content--not design content--allowing our team to separate writing-related tasks from design-related tasks.

- [Learn about the AsciiDoc markup language](https://docs.asciidoctor.org/asciidoc/latest/)
- [Get started with the AsciiDoc markup language](https://asciidoctor.org/docs/asciidoc-writers-guide/)
- [Directory and file names](#directory-and-file-names)
- [Directory structure](#directory-structure)

### Static site generator

The static site generator converts all plain text files to HTML and bundles them with our CSS when you [build the docs locally](#build-the-docs-locally).

- [Learn about Antora](https://docs.antora.org/antora/latest/how-antora-works/)
- [Get started with Antora](https://docs.antora.org/antora/latest/install-and-run-quickstart/)
- [Antora playbooks](#antora-playbooks-and-ui-bundles)

### Publishing

When a commit is merged to our `main` branch in GitHub, the site is automatically published using Docker and GitHub actions.

- [Learn about Docker](https://docs.docker.com/get-started/overview/)
- [Get started with Docker](https://docs.docker.com/get-started/)
- [Docker commands](#docker-commands)
- [Learn about GitHub actions](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions)
- [Get started with GitHub actions](https://docs.github.com/en/actions/using-workflows/triggering-a-workflow)

## Build the docs locally

We use [Antora](https://docs.antora.org/antora/latest/how-antora-works/) to generate our static site. Before you can use Antora to generate the site locally, you'll need [Node.js](https://nodejs.org/) and [Yarn](https://yarnpkg.com/). Run the following commands to see if they're installed:

```plaintext
node --version
yarn --version
```

If Node.js and Yarn are installed, install project dependencies by running:

```plaintext
yarn install
```

To build the docs [with logs](#antora-logs), run:

```plaintext
yarn local
```

To view the logs in your web browser, run:

```plaintext
yarn server-docs
```

## Antora logs

Beautified logs are generated in the `logs` directory when you run `yarn local`. If AsciiDoc preview is enabled in your text editor, you can select links in the **Table of contents** or the **File** column to open that section or file.

<img src=".github/images/beautified-logs.png" alt="Beautified Antora logs."/>

Run `yarn build` to generate standard JSON logs instead.

```json
{"level":"error","time":1691005714646,"name":"asciidoctor","file":{"path":"/Users/<your-username>/kobiton/docs/docs/modules/automation-testing/pages/index.adoc"},"source":{"url":"https://github.com/kobiton/documentation.git","local":"/Users/<your-username>/kobiton/docs/.git","worktree":"/Users/<your-username>/kobiton/docs","refname":"update-contributing-doc","reftype":"branch","startPath":"docs"},"msg":"target of image not found: $NEW-IMAGE$"}
{"level":"error","time":1691005714663,"name":"asciidoctor","file":{"path":"/Users/<your-username>/kobiton/docs/docs/modules/apps/pages/index.adoc"},"source":{"url":"https://github.com/kobiton/documentation.git","local":"/Users/<your-username>/kobiton/docs/.git","worktree":"/Users/<your-username>/kobiton/docs","refname":"update-contributing-doc","reftype":"branch","startPath":"docs"},"msg":"target of image not found: $NEW-IMAGE$"}
{"level":"error","time":1691005714679,"name":"asciidoctor","file":{"path":"/Users/<your-username>/kobiton/docs/docs/modules/devices/pages/about-device-passcodes.adoc"},"source":{"url":"https://github.com/kobiton/documentation.git","local":"/Users/<your-username>/kobiton/docs/.git","worktree":"/Users/<your-username>/kobiton/docs","refname":"update-contributing-doc","reftype":"branch","startPath":"docs"},"msg":"target of image not found: $NEW-IMAGE$"}
{"level":"error","time":1691005714694,"name":"asciidoctor","file":{"path":"/Users/<your-username>/kobiton/docs/docs/modules/devices/pages/index.adoc"},"source":{"url":"https://github.com/kobiton/documentation.git","local":"/Users/<your-username>/kobiton/docs/.git","worktree":"/Users/<your-username>/kobiton/docs","refname":"update-contributing-doc","reftype":"branch","startPath":"docs"},"msg":"target of image not found: $NEW-IMAGE$"}
{"level":"error","time":1691005714712,"name":"asciidoctor","file":{"path":"/Users/<your-username>/kobiton/docs/docs/modules/devices/pages/search-for-a-device.adoc"},"source":{"url":"https://github.com/kobiton/documentation.git","local":"/Users/<your-username>/kobiton/docs/.git","worktree":"/Users/<your-username>/kobiton/docs","refname":"update-contributing-doc","reftype":"branch","startPath":"docs"},"msg":"target of image not found: $NEW-IMAGE$"}
{"level":"error","time":1691005714718,"name":"asciidoctor","file":{"path":"/Users/<your-username>/kobiton/docs/docs/modules/integrations/pages/index.adoc"},"source":{"url":"https://github.com/kobiton/documentation.git","local":"/Users/<your-username>/kobiton/docs/.git","worktree":"/Users/<your-username>/kobiton/docs","refname":"update-contributing-doc","reftype":"branch","startPath":"docs"},"msg":"target of image not found: $NEW-IMAGE$"}
```

## Antora playbooks and UI bundles

Typically, a project uses one `antora-playbook.yml` and one `ui-bundle/` directory to configure Antora. However, our project uses a set of each: one for [docs.kobiton.com](https://docs.kobiton.com/) and one for [portal.kobiton.com](https://portal.kobiton.com/). In most cases, the playbook will match and the UI bundles will remain site-specific.

### Docs content

The content on [docs.kobiton.com](https://docs.kobiton.com/) is configured in `antora-playbook-docs.yml` and the `ui-bundle-docs` directory.

- `antora-playbook-docs.yml` is used to configure the site name, analytics keys, extensions, UI bundle location, [Antora logs](#antora-logs), and [site URLs](#site-urls).
- `ui-bundle-docs` contains all source files for style and design of the site, including the home page tiles.

<img src=".github/images/docs-site.png" alt="Kobiton Docs site landing page."/>

### Portal widget

The help widget on [portal.kobiton.com](https://portal.kobiton.com/) is configured in `antora-playbook-widget.yml` and the `ui-bundle-widget/` directory.

- `antora-playbook-widget.yml` is used to configure the site name, analytics keys, extensions, and UI bundle location.
- `ui-bundle-widget/` contains all source files for style and design of the widget on [portal.kobiton.com](https://portal.kobiton.com/).

<img src=".github/images/portal-site.png" width="500" height="" alt="Help widget on Kobiton portal."/>

## Directory structure

Our project hosts a single `modules` directory containing an `antora.yml` file, a `ROOT` directory, and a directory for each section of content.

```plaintext
PROJECT
└── docs
    ├── modules
    │   ├── ROOT
    │   └── example-section
    └── antora.yml
```

Each directory in `modules` hosts a specific section, including an `attachments`, `images`, `pages`, and `partials` directory, as well as a `nav.adoc` file.

```plaintext
modules
└── example-section
    ├── attachments
    ├── images
    ├── pages
    ├── partials
    └── nav.adoc
```

The `pages` directory hosts the written content for each section as `.adoc` files with [this file formatting](#directory-and-file-names). Content files can be stored directly in `pages` (such as `pages/*`) or in [multi-nested directories](#add-a-subsection) (such as `pages/**/*`).

```plaintext
example-section
└── pages
    ├── subsection-a
    │   ├── index.adoc
    │   └── page-a.adoc
    ├── subsection-b
    │   └── page-b.adoc
    ├── index.adoc
    └── page-c.adoc
```

_At a minimum_, each `pages` directory must contain an `index.adoc` file, which serves as the section's landing page and is accessible from the [navigation bar](#site-navigation).

<img src=".github/images/example-section.png" alt="An example section on Kobiton Docs."/>

## Site navigation

When [docs.kobiton.com](https://docs.kobiton.com/) is generated, these files create the site's navigation bar:

- `nav.adoc`: determines which pages are displayed beneath each section on the navigation bar.
- `antora.yml`: determines which sections (or modules) are added to the navigation bar.

Use these files to add [sections](#add-a-section), [pages](#add-a-page), and [subsections](#add-a-subsection) to the navigation bar.

### Add a section

To add a section to the navigation bar, open `docs/antora.yml` and add the relative path to that section's `nav.adoc` file beneath the `nav` key.

```yaml
name: ROOT
title: Kobiton Docs
version: ~
nav:
  - modules/example-section/nav.adoc
```

If the `nav.adoc` contains _at least_ a [landing page](#add-a-landing-page), that section will be added to the navigation bar. For example: 

**`nav.adoc` input:**

```asciidoc
.xref:example-section:index.adoc[] // Section landing page
* xref:example-section:page.adoc[]

* Subsection A
** xref:example-section:subsection-a/page-a.adoc[]

* xref:example-section:subsection-b/index.adoc[]
** xref:example-section:subsection-b/page-b.adoc[]
```

**`nav.adoc` output:**

<img src=".github/images/example-section.png" alt="An example section on Kobiton Docs."/>

### Add a page

A file in the `pages` directory can either serve as a section's [landing page](#add-a-landing-page) or a [content page](#add-a-content-page). _At a minimum_, a `pages` directory and `nav.adoc` file must contain a landing page (as an `index.adoc` file) so add a landing page before any content pages.

#### Add a landing page

To add a landing page to a section [or subsection](#add-a-subsection) in the navigation bar, open the `nav.adoc` for that section.

```plaintext
PROJECT
└── docs
    └── modules
       └── example-section
           ├── images
           ├── pages
           ├── partials
           └── nav.adoc
```

The landing page must be set to `.xref:index.adoc[]` at the top of the `nav.adoc` file, so [site URLs](#remove-index-strings) are generated properly. Add it to the unordered list. For example:

**`nav.adoc` input:**

```asciidoc
.xref:example-section:index.adoc[] // Section landing page
* xref:example-section:page.adoc[]

* Subsection A
** xref:example-section:subsection-a/page-a.adoc[]

* xref:example-section:subsection-b/index.adoc[]
** xref:example-section:subsection-b/page-b.adoc[]
```

**`nav.adoc` output:**

<img src=".github/images/example-section.png" alt="An example landing page on Kobiton Docs."/>

(Be sure the section's `nav.adoc` begins with `.xref:index.adoc[]` so [site URLs](#remove-index-strings) are generated properly).

#### Add a content page

To add a content page to a section [or subsection](#add-a-subsection) in the navigation bar, open the `nav.adoc` for that section.

```plaintext
PROJECT
└── docs
    └── modules
       └── example-section
           ├── images
           ├── pages
           ├── partials
           └── nav.adoc
```

Add a cross-reference to the page in the unordered list. For example:

**`nav.adoc` input:**

```asciidoc
.xref:example-section:index.adoc[]
* xref:example-section:page.adoc[] // Content page

* Subsection A
** xref:example-section:subsection-a/page-a.adoc[]

* xref:example-section:subsection-b/index.adoc[]
** xref:example-section:subsection-b/page-b.adoc[]
```

**`nav.adoc` output:**

<img src=".github/images/page.png" alt="An example content page on Kobiton Docs."/>

### Add a subsection

When you add a subsection, you can choose to [add](#with-a-landing-page) or [omit](#without-a-landing-page) a landing page for that subsection.

#### With a landing page

To add a subsection with a landing page, first create a directory for that subsection. Add an `index.adoc` file (which will serve as the landing page) and all related `.adoc` files:

```plaintext
example-section
├── pages
│   ├── subsection-a
│   │   └── page-a.adoc
│   ├── subsection-b
│   │   ├── index.adoc // Subsection landing page
│   │   └── page-a.adoc // Subsection content page
│   ├── index.adoc
│   └── page-b.adoc
└── nav.adoc
```

Open the `nav.adoc` for the main section and add cross-references to the `index.adoc` to the unordered list and all content files one list-level below it:

**`nav.adoc` input:**

```asciidoc
.xref:example-section:index.adoc[]
* xref:example-section:page.adoc[]

* Subsection A
** xref:example-section:subsection-a/page-a.adoc[]

* xref:example-section:subsection-b/index.adoc[] // Subsection landing page
** xref:example-section:subsection-b/page-b.adoc[] // Subsection content page
```

**`nav.adoc` output:**

<img src=".github/images/subsection-b.png" alt="An example subsection landing page on Kobiton Docs."/>

#### Without a landing page

To add a subsection without a landing page, first create a directory for that subsection, then add all related `.adoc` files:

```plaintext
example-section
├── pages
│   ├── subsection-a
│   │   └── page-a.adoc // Subsection content page
│   ├── subsection-b
│   │   ├── index.adoc
│   │   └── page-a.adoc
│   ├── index.adoc
│   └── page-b.adoc
└── nav.adoc
```

Open the `nav.adoc` for the main section and add the subsection title as plaintext to the unordered list, then cross-references for each `.adoc` file one list-level below it:

**`nav.adoc` input:**

```asciidoc
.xref:example-section:index.adoc[]
* xref:example-section:page.adoc[]

* Subsection A // Subsection title
** xref:example-section:subsection-a/page-a.adoc[] // Subsection content page

* xref:example-section:subsection-b/index.adoc[]
** xref:example-section:subsection-b/page-b.adoc[]
```

**`nav.adoc` output:**

<img src=".github/images/page-a.png" alt="An example subsection content page on Kobiton Docs."/>

## Site URLs

> These URL guidelines are strictly enforced to avoid formatting inconsistencies and broken end-user bookmarks.

URLs are generated from three files:

- `antora-playbook-docs.yml`: determines if URLs end in a file extension, like `.html`.
- `antora.yml`: determines if URLs contain subdirectories, like `docs/`.
- `nav.adoc`: determines if certain URLs contain `index` strings.

Use these files to remove [file extensions](#remove-file-extensions), [subdirectories](#remove-subdirectories), and [`index` strings](#remove-index-strings) from URLs. 

### Remove file extensions

The `antora-playbook-docs.yml` is used to add or remove the `.html` file extension from URL endings.

- Before: `docs.kobiton.com/devices/install-an-app.html`
- After: `docs.kobiton.com/devices/install-an-app`

For [docs.kobiton.com](https://docs.kobiton.com/), we **do not** add file extensions to URL endings, so the `html_extension_style` key is set to `drop` in the `antora-playbook-docs.yml` file:

```yaml
site:
  title: Kobiton Docs

urls:
  html_extension_style: drop

content:
  sources:
  - url: .
    start_paths: docs
    branches: HEAD
```

However, if this needs to change in the future, [set `html_extension_style` to `indexing`](https://docs.antora.org/antora/latest/playbook/urls-html-extension-style/#html-extension-style-key) or remove the key completely:

```yaml
site:
  title: Kobiton Docs

content:
  sources:
  - url: .
    start_paths: docs
    branches: HEAD
```

### Remove subdirectories

The `antora.yml` file in `PROJECT/docs/` is used to add or remove a subdirectory from the site URL.

- Before: `docs.kobiton.com/docs/get-started/`
- After: `docs.kobiton.com/get-started/`

For [docs.kobiton.com](https://docs.kobiton.com/), we **do not** add subdirectories, so the `name` property is set to `ROOT` in the `antora.yml` file:

```yaml
name: ROOT
title: Kobiton Docs
version: ~
nav:
  - modules/get-started/nav.adoc
  - modules/release-notes/nav.adoc
  - modules/integrations/nav.adoc
```

However, if this needs to change in the future, set `name` to any hyphen-separated string:

```yaml
name: kobiton-docs
title: Kobiton Docs
version: ~
nav:
  - modules/get-started/nav.adoc
  - modules/release-notes/nav.adoc
  - modules/integrations/nav.adoc
```

### Remove `index` strings

The `nav.adoc` file in each module is used to generate the [site navigation](#remove-index-strings), as well as add or remove `index` from URLs.

- Before: `docs.kobiton.com/get-started/index`
- After: `docs.kobiton.com/get-started/`

For [docs.kobiton.com](https://docs.kobiton.com/), we **do not** add `index` to URLs, so [Antora's list title formatting](https://docs.antora.org/antora/latest/navigation/files-and-lists/#list-titles-and-items) should be applied to the first `index.adoc` listed in the `nav.adoc` file:

```asciidoc
.xref:index.adoc[]
* xref:devices:search-for-a-device.adoc[]
* xref:devices:manage-devices.adoc[]

* xref:devices:network-payload-capture/index.adoc[]
** xref:devices:network-payload-capture/configure-the-local-server.adoc[]
** xref:devices:network-payload-capture/configure-the-local-server.adoc[]
** xref:devices:network-payload-capture/configure-an-ios-device.adoc[]
```

## Hide a page from search

By default, all `.adoc` files in the `modules` directory are searchable on Kobiton Docs using the [Antora Lunr Extension](https://gitlab.com/antora/antora-lunr-extension). To hide a page from search results, add the `:noindex:` attribute to the page's metadata.

```asciidoc
= Generate an API token
:navtitle: Generate an API token
:noindex:

Learn how to generate an API token in Kobiton.
```

## Partials

Antora partials allow you to reuse global and feature-specific content across the docs. Global content (role requirements, pricing, etc.) is located within `ROOT/partials`, while feature-specific content (supported app filetypes, supported gestures, etc.) is located within that specific feature's `partials` subdirectory.

```plaintext
ROOT
└── docs
    └── modules
        ├── ROOT
        │   └── partials
        │       ├── pricing.adoc
        │       └── roles-page.adoc
        └── apps
            └── partials
                └── supported-filetypes.adoc
```

To use a global partial, use the following `include` statement:

```asciidoc
include::ROOT:partial$<filename>.adoc
```

To use a feature-specific partial, use the following `include` statement:

```asciidoc
include::<feature>:partial$<filename>.adoc
```

## Directory and file names

All directories and files should follow these guidelines:

| Naming Guideline           | Before               | After                   |
|----------------------------|----------------------|-------------------------|
| Only lowercase letters     | `This Is My TITLE`   | `this is my title`      |
| Replace spaces with dashes | `this is my title`   | `this-is-my-title`      |
| Replace important symbols  | `i love c++ & c#`    | `i love cpp and csharp` |
| Remove unimportant symbols | `this: is my title!` | `this is my title`      |

For example:

```plaintext
automation-testing
└──pages
   ├── desired-capabilities.adoc
   ├── download-appium-script.adoc
   ├── index.adoc
   └── supported-client-libraries.adoc
```

## Page types and templates

We use the [Diátaxis](https://diataxis.fr/) framework to structure our docs. Each Diátaxis category corresponds to one of these templates. Add a template to your `.adoc` file to get started.

### Tutorial page type

Tutorial docs walk users through their first time attempting a task. Everything a user needs should be available in the tutorial.

For example, a tutorial titled "Your first manual session" would state a learning objective, show the user how to start a session, offer an app for them to install, and walk them through a variety of test steps.

#### Tutorial template

```asciidoc
= Title
:navtitle: Title

In this tutorial, we'll walk you through your first...

== Before you start

You'll need to download...

== Step 1

Content.

== Step 2

Content.

. Sub-step
. Sub-step
```

### How-to page type

How-to docs outline the steps for solving a specific problem. Unlike tutorials, How-tos only focus on a specific problem--not an entire process.

For example, a how-to doc titled "Download an app during a manual test session" would state the goal, give a line of context, and start step one assuming the user has _already_ launched a manual test session.

#### How-to template

```asciidoc
= Title
:navtitle: Title

Learn how to...

== Step 1

Explain and give steps.

== Step 2

Explain steps.

. Give step
. Give step
```

### Reference page type

Reference docs describe a _product_, not a _process_. They're for users who know how to complete a process, but need more details about the _tools_ they use to complete a process.

For example, a reference doc titled "Desired capabilities" should list all desired capabilities along with their definition and a brief example. The reference doc shouldn't contain steps for modifying desired capabilities or walk users through their first automation session.

#### Reference template

```asciidoc
= Title
:navtitle: Title

These are the ... for ...

== Category one

Item.

Definition.

Example.

== Category two

=== Item one

Definition.

Example.

=== Item two

Definition.

Example.
```

### Explanation page type

Explanation docs explore a topic, which could include its context within culture, its context within Kobiton, how it got here, and where it's headed.

For example, an explanation doc titled "About biometric authentication" should explore a few key milestones in its global development, why It's important to test, and how Kobiton can help.

#### Explanation template

```asciidoc
= Title
:navtitle: Title

<Topic does x...>

== First item

Content.

== Second item

Content.
```

### Release notes

Release notes are not a part of the [Diátaxis](https://diataxis.fr/) framework, so we use the following templates for our release notes.

#### For Kobiton 4.0 or later

```asciidoc
= Kobiton X.X release notes
:navtitle: Kobiton X.X release notes

_DATE_

== First item

Content.

== Second item

Content.
```

#### For legacy Kobiton

```asciidoc
= Kobiton X.X release notes (Legacy)
:navtitle: Kobiton X.X release notes

_DATE_

== First item

Content.

== Second item

Content.
```

## Style and voice

One day we'll create our own, but for now we use the [Microsoft Style Guide](https://learn.microsoft.com/en-us/style-guide/brand-voice-above-all-simple-human) to inform our style and voice.

## Docker commands

We use [Docker](https://www.docker.com/) and [GitHub actions](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions) to publish content to [docs.kobiton.com](https://docs.kobiton.com/) and [portal.kobiton.com](https://portal.kobiton.com/).

### Create an image for the docs

To create a docker image for [docs.kobiton.com](https://docs.kobiton.com/), run:

```shell
docker build -t kobiton/docs:1.0 -f docker/docs/Dockerfile .
```

### Create an image for the portal

To create a docker image for the help widget on [portal.kobiton.com](https://portal.kobiton.com/), run:

```shell
docker build -t kobiton/widget:1.0 -f docker/widget/Dockerfile .
```
