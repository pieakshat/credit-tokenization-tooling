# Contributing

Accuracy takes priority over coverage. Every entry must be verifiable against its primary source.

## How contributions work

Contributions are open to anyone. All changes are made through pull requests, including changes from maintainers. Direct pushes to `main` are not used.

1. Fork the repository and create a branch.
2. Make the change and open a pull request against `main`.
3. Complete the checklist in the pull request template.
4. Wait for the link check to pass and for maintainer review. Reviewers verify the entry against its primary source, and may request changes or decline an entry that does not meet the criteria below.

By submitting a pull request, the contributor agrees that the contribution is released under [CC0 1.0](LICENSE), the license of this repository.

## Inclusion criteria

A tool is eligible when it helps build a tokenization protocol for credit or funds and:

1. It links to a primary source: the official repository, documentation site or EIP page.
2. The contributor has read that source. Summaries are not copied from third-party lists or articles.
3. License and audit status are stated as found at the source. "No license stated" is a valid value; an audit is listed only when a report is linked.
4. It is relevant to credit and fund tokenization. General-purpose libraries are listed only when they serve a distinct role in this stack.

Unmaintained tools may be listed when still instructive. The state of maintenance is recorded in the entry's notes.

## Adding an entry

1. Choose the file in [`tools/`](tools/) that matches the tool's main role. Cross-reference it from other categories where relevant.
2. Copy the [entry template](_templates/tool-entry.md) and complete every applicable field.
3. Set **Last checked** to the date the source was read.
4. Open a pull request as described above.

## Writing style

- Descriptions are factual and written in the contributor's own words, without promotional language.
- Entries and documentation are written in the third person, in American English, and avoid conversational phrasing.
- Code from listed tools is never copied into this repository. Entries link to the source.

## Blueprints

Blueprints in [`blueprints/`](blueprints/) may only recommend tools that have an entry in `tools/`, and must link to that entry.

## Corrections

Outdated entries, changed licenses and inaccurate descriptions are corrected through pull requests. Issues may be opened to report a problem without proposing a fix.
