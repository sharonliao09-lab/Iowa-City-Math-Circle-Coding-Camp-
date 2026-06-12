# icmc

Independently developed Java course with supplementary Python for ICMC.  
View live [here](https://objectoops.github.io/icmc/).

## Contents

- Interactive [Slidev](https://sli.dev/) slides presentation
  - Code blocks with syntax highlighting
  - In-browser Java and Python code-runners
- Worksheets and answer keys
  - 4 worksheets
  - 2 bonus worksheets

### Schedule

<img width="707" height="344" alt="image" src="https://github.com/user-attachments/assets/d3d41c79-1e4f-44db-bd49-cfaf2133bc8a" />

## About

- Intended for learners with little to no experience
- Covers basic language fundamentals in the first week
- Covers additional topics in the second week
- Includes beginner CS concepts like runtime complexity (but no recursion or ADTs)
- Full-feature coding environment using [code-server](https://github.com/coder/code-server) via [mybinder.org](https://mybinder.org/)
    - "Multiplayer" support using [this extension](https://open-vsx.org/extension/typefox/open-collaboration-tools)

## Forking

1. Fork this repo. Include **all branches**.
2. Adjust the headmatter information of the presentation:
   - `title` - title of the presentation
   - `info` - additional presentation info
   - `author` - replace with your name
   - `download` - path to exported presentation PDF
   - `favicon` - favicon
   - `seoMeta` - SEO
   - `date` - the date of the Monday during which the course will begin
     - The schedule and headers in the presentation will be based off this date
   - `timezone` - timezone of the date above
   - `startupLink` - Binder URL. Generate your own with your forked repo at [mybinder.org](https://mybinder.org/)
     - Binder badge links in the presentation will reflect this URL
   - `githubSnippets` - URL to snippets directory in your forked repo
     - Some large code blocks include a link to their respective file inside this directory
     - Your repo will need to be public if these links are to be used
3. Adjust or remove slides referencing ICMC or other information that may not apply.
   - Slide numbers: contact info (4), robotics (10, 11), thank you note (172)
5. Test changes locally.
6. Deploy to a static web host.
   - To generate a PDF export, temporarily set `browserExporter` to `true`, re-deploy, export the PDF from the presentation UI, restore `browserExporter`, and re-deploy again.

___

The following Binder link is intended for opening a Java + Python environment in `workbench`.

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/ObjectOops/icmc/binder?urlpath=vscode)
