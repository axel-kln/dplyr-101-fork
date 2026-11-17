# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Purpose

Teaching material (data management course, Dauphine) introducing `dplyr` and `tidyr`.
The repository is built incrementally, one concept per commit (e.g. "Introduction to
mutate", "Add weekly sales dataset"): new content is appended to the Quarto documents
and each dataset is added in its own commit.

## Documents

- `intro_to_dplyr.qmd`: slide deck rendered to both `revealjs` and `pptx`. Code is hidden
  by default (`echo: false` in the format options); chunks meant to be shown on a slide
  set `#| echo: true` explicitly, and code shown but not run uses `#| eval: false`.
  Top-level `#` headings are sections, `##` headings are slides (`{.smaller}` for dense
  slides). Tables print with `df-print: kable`. Inline `` `r ...` `` expressions are used
  to quote computed values in the prose.
- `join.qmd`: HTML document on working with multiple tables (joins), based on the
  `Financial/` relational dataset. Work in progress.

Rendered outputs (`*.html`, `*_files/`, `*.pptx`) are git-ignored.

## Commands

```sh
quarto render intro_to_dplyr.qmd          # all formats (revealjs + pptx)
quarto render intro_to_dplyr.qmd --to revealjs
quarto render join.qmd
quarto preview join.qmd                    # live preview
```

## Conventions

- Paths are resolved with `here`: each document starts with
  `here::i_am("dplyr-101.Rproj")` and data are read with
  `vroom(here("data", "<file>.csv"))`.
- Packages: `dplyr`, `tidyr`, `vroom`, `ggplot2` (`theme_set(theme_bw())` in the slides),
  native pipe `|>`. Two-space indentation, tidyverse style.
- In `join.qmd`, tables are loaded with explicit `col_types` (integer ids, dates,
  factors), since keys must have matching types for joins.

## Data

- `data/`: standalone datasets used in the slides (credit card default, WHO life
  expectancy, weekly sales, and the fictional `planets.csv` / `stars.csv` pair, which is
  deliberately messy: inconsistent column names, multi-valued `;`-separated fields, used
  for `separate_*` and joins via `STAR_CODE`).
- `Financial/`: PKDD'99 Financial dataset (Czech bank; source and documentation in
  `Financial/names.txt`, schema diagram in `Financial/financial.svg`). Tables are linked
  by `account_id`, `client_id`, `disp_id` (`disp` links clients to accounts) and
  `district_id`. Many values are in Czech (e.g. `frequency`, transaction `type`/`operation`).
