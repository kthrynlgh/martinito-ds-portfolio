# Portfolio guide

How this site is put together and how to add new work. This file is excluded from the built site (see `project.exclude` in `myst.yml`).

## Folder structure

```
.
├── myst.yml                     # site configuration
├── intro.md                     # landing page
├── _static/
│   ├── custom.css               # scrolling + readability tweaks
│   └── favicon.ico              # (add your own)
├── assignments/
│   ├── index.md                 # section landing page + status table
│   ├── assignment-01.ipynb
│   └── data/                    # per-notebook data, excluded from the build
├── lab-activities/
│   ├── index.md
│   └── lab-exercise-01.ipynb
├── projects/
│   ├── index.md
│   └── project-01.ipynb
├── reference/
│   ├── glossary.md
│   └── resources.md
└── templates/                   # copy these; excluded from the build
    ├── TEMPLATE-assignment.ipynb
    ├── TEMPLATE-lab-activity.ipynb
    └── TEMPLATE-project.ipynb
```

## Adding new work

1. Copy the matching template out of `templates/` into the right folder.
2. Rename it with zero-padded numbering: `assignment-03.ipynb`, `lab-exercise-04.ipynb`, `project-03.ipynb`. Zero padding keeps files sorted correctly past number 9.
3. Fill in the YAML frontmatter in the first markdown cell (`title`, `short_title`, `date`, `description`).
4. Add the file to the `toc` in `myst.yml`.
5. Add a row to the section's `index.md` table and to the tracker on `intro.md`.

## Naming conventions

| Thing | Convention | Example |
|---|---|---|
| Files | lowercase, hyphens, zero-padded | `lab-exercise-03.ipynb` |
| Folders | lowercase, hyphens | `lab-activities/` |
| Notebook title | `Type NN: Descriptive Title` | `Project 01: Forecasting Rainfall in Misamis Oriental` |
| `short_title` | under ~20 characters | `Project 01` |

`short_title` is what appears in the sidebar. Without it, long titles wrap and make the navigation hard to scan.

## Page structure

Every notebook follows the same six sections so readers always know where to look:

**Overview → Setup → Data → Method → Results → Reflection**

Use `##` for these sections and `###` for subsections. Don't go deeper than `###`; the page outline is set to depth 3.

## Keeping pages scrollable

Long notebooks are the main readability problem in a DS portfolio. Four things fix most of it:

1. **Collapse the noise.** Tag cells in Jupyter (View → Cell Toolbar → Tags, or the property panel in JupyterLab):
   - `hide-input` — hides the code, keeps the output. Use for import cells and plotting code.
   - `hide-output` — hides the output, keeps the code. Use for training logs.
   - `hide-cell` — hides both, with a button to reveal.
   - `remove-input` / `remove-output` / `remove-cell` — gone entirely, no reveal button.
2. **Cap output height.** `_static/custom.css` puts tall outputs and wide tables in their own scroll boxes, so a 500-row dataframe doesn't add three screens of scrolling.
3. **Split, don't stretch.** If a notebook passes roughly 40 cells, split it into two pages and nest both under one TOC entry. One page per idea beats one page per week.
4. **Use the outline.** `outline_maxdepth: 3` gives readers a working "On this page" jump list on the right — but only if your headings are consistent.

Also worth using: `:::{dropdown} Show derivation` for long side explanations, and `::::{tab-set}` for alternative approaches you don't want stacked vertically.

## Useful MyST directives

```markdown
:::{note} Title
Content.
:::

:::{admonition} Custom title
:class: tip     <!-- tip, warning, important, seealso, danger -->
Content.
:::

:::{dropdown} Click to expand
Hidden until clicked.
:::

::::{tab-set}
:::{tab-item} Python
Content.
:::
:::{tab-item} R
Content.
:::
::::

::::{grid} 1 1 2 2
:::{card} Title
:link: ./page.md
Body.
:::
::::
```

## Build and preview

```bash
pip install mystmd            # or: npm install -g mystmd
myst start                    # live preview at localhost:3000
myst build --html             # static build
```

## Before you publish

- [ ] Every notebook runs top to bottom from a fresh kernel
- [ ] No absolute paths (`C:\Users\...`) — use relative paths like `data/file.csv`
- [ ] No credentials, API keys, or personal data in any cell
- [ ] Every figure has axis labels with units and a caption
- [ ] Every notebook has a filled-in Reflection section
- [ ] Datasets are credited in References
- [ ] The tracker table on `intro.md` matches reality
