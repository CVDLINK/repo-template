# Publishing this project

This repo was created from the CVDLINK **repo-template**. Work through the checklist below to
release it to Zenodo → OpenAIRE → EOSC. It fits any research output — a tool, a dataset, or
something else.

Publishing an **AI model**? Use the
[**model-template**](https://github.com/CVDLINK/model-template) instead — it adds an AI Card and an
AIMe registry entry.

![Data flow](data-flow.jpg)

This file is a temporary checklist: once everything is published, you delete it (stage 7) so your
repo stays minimal.

## Checklist

Everything up to the release is reversible — after the
release it is not.

### 0 · Create your repo from the template (GitHub)

- [ ] On the [template's GitHub page](https://github.com/CVDLINK/repo-template), click the green
      **Use this template** button (top right) → *Create a new repository*.
- [ ] Choose the owner, name and visibility. Either visibility works for now, but Zenodo can only
      archive **public** repos, so it has to be public before stage 3.

### 1 · In this repo (GitHub)

- [ ] Fill in `README.md`.
- [ ] Update `CHANGELOG.md` for the release.
- [ ] Confirm the `LICENSE` (default MIT — change if needed; don't hand-write license text).
- [ ] Edit `.zenodo.json` (title, description, creators, keywords) — keep `communities: cvdlink`.
      Write every name as **`Lastname, Firstname`** (e.g. `"Virtanen, Anna"`).
      **`orcid` is optional** — delete the line for any creator without one. Zenodo checks it, so a
      placeholder value makes the release fail.
- [ ] Publishing a dataset or a document? Change `"upload_type"` in `.zenodo.json` (see
      [Notes](#notes)).
- [ ] **Validate `.zenodo.json`** (e.g. <https://www.jsonschemavalidator.net/>). If it has errors,
      Zenodo silently publishes nothing — this failure gives you no warning.
- [ ] Add the content you're sharing: code, data, notebooks, results.

### 2 · Make it public (GitHub)

- [ ] Confirm no sensitive content (data, site identifiers, credentials, internal URLs).
- [ ] If the repo is still private, make it **public** (*Settings → General → Danger Zone →
      Change visibility*).

### 3 · Connect to Zenodo (zenodo.org) — before releasing

- [ ] Sign in to **[zenodo.org](https://zenodo.org)** with GitHub (first time only).
- [ ] On your **[Zenodo GitHub settings page](https://zenodo.org/account/settings/github/)**, find
      this repo and switch the toggle **ON**. Press *Sync now* if a newly created repo isn't listed.

> **The next step is permanent.** A published Zenodo record cannot be deleted — it gets a DOI
> and stays. Zenodo also archives **only** releases published *after* the toggle above is on.

### 4 · Release (GitHub)

- [ ] Cut a versioned GitHub **release** — this is the distributable snapshot and the trigger for
      everything downstream.

### 5 · Verify (zenodo.org)

- [ ] Check the release reached Zenodo: on the
      [Zenodo GitHub settings page](https://zenodo.org/account/settings/github/), click the repo
      name to see each release's status. If it failed, the error is shown there.
- [ ] Check the **Zenodo record**: metadata complete (title, authors, keywords, license).
- [ ] The record joins the **`cvdlink`** community only after a community curator accepts its
      inclusion request — until then it is published, with a DOI, but not listed there.
- [ ] Add the **DOI** to `README.md` under *How to cite*.

### 6 · Automatic — nothing to do

OpenAIRE harvests the Zenodo record, and it becomes discoverable through the EOSC EU Node.

**Later:** a new GitHub release becomes a new Zenodo version with its own DOI. Not every commit
needs one.

### 7 · Clean up (GitHub)

- [ ] Delete this file (`PUBLISHING.md`), its diagram (`data-flow.jpg`) and the template note at
      the top of `README.md`, then commit and push. The checklist stays readable in the
      [template repo](https://github.com/CVDLINK/repo-template/blob/main/PUBLISHING.md).
- [ ] Cut a new **release** (e.g. a patch version), so the latest Zenodo version is the clean one.

## Notes

- This template uses **`.zenodo.json`** for citation/metadata — it's the file Zenodo reads,
  and the only one that can carry the `cvdlink` community and EU grant info.
- The `grants` entry is pre-filled with CVDLINK's Horizon Europe grant (`101137278`) — leave it
  as-is so the record links to the project in OpenAIRE/EOSC.
- If you change the `LICENSE`, update the `.zenodo.json` `"license"` id to match (Zenodo uses
  lowercase ids, e.g. `"mit"`, `"apache-2.0"`, `"cc-by-4.0"`). Data is usually `"cc-by-4.0"`.
- `"upload_type"` is pre-set to `software`, which covers tools and code. Use `dataset` for data,
  or `publication` for documentation and deliverables.
- **Publishing data?** `.gitignore` blocks `data/` and `*.csv` / `*.parquet` so nothing sensitive
  is pushed by accident. If the data itself is what you publish, remove those lines.

<details>
<summary><strong>Metadata reference</strong> — other output types, contributors, CITATION.cff, OpenAIRE minimums</summary>

- **All `upload_type` values:** `publication`, `poster`, `presentation`, `dataset`, `image`,
  `video`, `software`, `lesson`, `physicalobject`, `other`.
  - `publication` also needs a `"publication_type"` (e.g. `report`, `deliverable`,
    `softwaredocumentation`, `article`); `image` needs an `"image_type"` (e.g. `figure`, `diagram`).
- **The `contributors` block is optional.** Fill it in for people who aren't authors (e.g. data
  curator, supervisor), or delete the whole block if there are none. Each contributor needs a
  `type` (e.g. `ProjectMember`, `DataCurator`, `Supervisor`).
- **`CITATION.cff` is optional.** Add one if you want GitHub's "Cite this repository" button.
  Zenodo ignores it when `.zenodo.json` is present, so it's purely for the GitHub UI.
- **Minimum metadata for indexing (OpenAIRE).** Every research product needs at least one
  persistent identifier — the Zenodo DOI covers this. Research software additionally needs only a
  title and a publishing date, so a correctly filled `.zenodo.json` clears the bar comfortably.

</details>
