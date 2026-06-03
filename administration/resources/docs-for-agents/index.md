---
title: Documentation for AI agents
description: Learn how to use Tealium documentation with AI agents and large language models.
url: https://docs.tealium.com/administration/resources/docs-for-agents/
---
Tealium documentation is available in formats optimized for AI agents and large language models (LLMs). In addition to standard HTML pages, all documentation is available as structured index files (llms.txt) and markdown versions of individual pages.

These formats reduce token usage, improve parsing accuracy, and make it easier for AI agents to discover and process Tealium documentation.

## llms.txt

The `llms.txt` format is a structured, machine-readable index that lists documentation sections and page links in a way AI agents can reliably parse. It improves discovery and retrieval of Tealium docs while reducing token overhead compared to crawling full HTML pages.

### Main index

The main llms.txt file is a top-level directory of all documentation areas. It lists each area with a description and a link to its section index.

* [/llms.txt](/llms.txt)

### Section indexes

Each documentation area has its own llms.txt file containing a full index of pages within that area:

* [Tag Management](/iq-tag-management/llms.txt): Client-side tag management documentation.
* [Server-Side](/server-side/llms.txt): Server-side documentation including events, audiences, functions, data sources, and insights.
* [APIs](/api/llms.txt): Developer API documentation and reference guides.
* [Web Install](/platforms/web-install/llms.txt): Web platform installation guides including JavaScript library and tag manager integrations.
* [Mobile Install](/platforms/mobile-install/llms.txt): Mobile platform installation guides including iOS SDK, Android SDK, and cross-platform frameworks.
* [Client-Side Tags](/client-side-tags/llms.txt): Documentation for individual client-side tags and vendor integrations.
* [Server-Side Connectors](/server-side-connectors/llms.txt): Documentation for individual server-side connectors and vendor integrations.
* [Administration](/administration/llms.txt): Platform administration including user access, permissions, and security settings.
* [Consent](/consent/llms.txt): Consent capture, interpretation, and enforcement across client-side and server-side environments.
* [Guides](/guides/llms.txt): Practical guides and strategies for using Tealium effectively.
* [Predict](/predict/llms.txt): Predict ML documentation for machine learning-powered audience predictions.
* [Partners and Industries](/partners-and-industries/llms.txt): Industry-specific integrations and partnership documentation.

## Markdown

Every documentation page is available as a markdown file. These files contain the page content without HTML markup or other site-specific syntax.

Markdown versions provide several advantages over HTML for AI agent processing:

* Fewer tokens: Plain markdown is more compact than HTML.
* Explicit structure: Headings, lists, and code blocks are unambiguous.
* Better parsing: No need to strip tags or handle rendering artifacts.
* Consistent formatting: All pages follow the same markdown conventions.

### Access markdown versions

To access the markdown version of any documentation page, append `/index.md` to the page URL.

Example:

* HTML version: [/iq-tag-management/getting-started/what-is-tealium-iq/](/iq-tag-management/getting-started/what-is-tealium-iq/)
* Markdown version: [/iq-tag-management/getting-started/what-is-tealium-iq/index.md](/iq-tag-management/getting-started/what-is-tealium-iq/index.md)

## Language support

All llms.txt indexes and markdown pages are available in English and Japanese.

For llms.txt indexes:

* English main index: [/llms.txt](/llms.txt)
* Japanese main index: [/ja/llms.txt](/ja/llms.txt)

Section indexes follow the same pattern:

* English: `/{area}/llms.txt`
* Japanese: `/ja/{area}/llms.txt`

For markdown pages:

* English: `/{path}/index.md`
* Japanese: `/ja/{path}/index.md`


