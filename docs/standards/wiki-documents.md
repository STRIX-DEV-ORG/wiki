---
description: What you should do when creating a new wiki document entry.
tags: [documentation, wiki]
---

# STD - Wiki documents

## Objective

To create readable, understandable and standarized documents for the STRIXDEV wiki.

## Content

As a member of STRIXDEV you have the ability to modify the wiki, but you need to stick to these standards and rules to do so.

### Writing

- Use clear and concise language. Avoid jargon, slang, and colloquialisms.
- Follow the standard structure given by the corresponding template, if no template is available for the document, create one.
- Use headings, subheadings, bullet points, and numbered lists to organize and present information in a logical and readable way.
- Use consistent formatting, font, spacing, and alignment throughout the document.
- Cite and reference any sources of information, data, or ideas that are not your own. Create links to the sources of information if required.
- Use appropriate tone and voice for the purpose of the document. Be respectful and professional.
- Use active voice and strong verbs whenever possible. Avoid passive voice and weak verbs such as be, have, do, etc.
- Use correct grammar, spelling, punctuation, and capitalization. Proofread and edit your document before submitting or publishing it.
- Use tables, graphs, charts, images, or other visual aids to illustrate or support your points. Make sure they are relevant, clear, and labeled properly.
- If your document contains several information that might be useful for any other document, separate that information into its own document and create liks where needed.
- Use transitions and connectors to link your sentences and paragraphs. Make sure your document flows smoothly and coherently.
- Use specific and concrete examples, facts, statistics, or quotations to support your document. Avoid vague or general statements.
- Use parallel structure and consistent tense throughout your document. Make sure your verbs agree with your subjects and your pronouns agree with their antecedents.
- Avoid stereotypes, biases, or offensive terms based on gender, race, ethnicity, religion, disability, etc.
- Use feedback and suggestions from others to improve your document. Be open to constructive criticism and revision.
- If the document you are creating requires a placeholder, you can use capital letters or other symbols like dashes, just make sure that it follows your example needs. But if several words are continuous, use kebab case.

### Naming conventions

Every document type has its own naming convention, you need to follow that convention and stick to it. If no convention is being followed for naming a document type, create one and add it to the [templates](/docs/category/templates).

### Tags

Every wiki document can and should have at least one tag associated to it, but those tags need to follow the next:

- Use descriptive and relevant words or phrases that capture the main idea or theme of the document. Avoid using too many or too vague tags that do not help to find or understand the document.
- Use lowercase letters for all tags.
```txt title="Examples"
❌ DEPLOYMENT
❌ Deployment
❌ NodeJS
✅ deployment
✅ nodejs
```
- Use hyphens (-) to separate words within a tag, and commas (,) to separate multiple tags. Do not use spaces, underscores (_), or other punctuation marks in or between tags.
```txt title="Examples"
❌ root user
❌ root_user
✅ root-user
```
- Use singular nouns and verbs for tags, unless the plural form is more appropriate or common.
```txt title="Examples"
❌ deployments
❌ branches
✅ deployment
✅ branch
```
- Use consistent and standardized tags across similar or related documents. Avoid using synonyms, variations, or abbreviations of the same tag. You can take a look on the [tags page](/docs/tags).
- Use tags that are specific and avoid using tags that are too general or common.

### Descriptions

Every document must have a brief meta description, this will be used to have a quick understanding of the document contents, it must be the first thing you write on the document, even before the tags:
```md
---
description: This is the doucment's description
tag: [here, you, have, comma, separated, tags]
---
```

### Modifications

The documents will change over time, but every modification needs to be documented with a version, each version must have a brief description of the changes made, who made those changes and the update date.

If the modifications are small additions or fixes, then you should just add a decimal to the version:
```md
| Version | Description               | Responsibles                     | Date       |
|---------|---------------------------|----------------------------------|------------|
| 1.0     | Standard creation         | Emmanuel Antonio Ramirez Herrera | 03/01/2024 |
| 1.1     | Fixed several misspelings | Emmanuel Antonio Ramirez Herrera | 04/01/2024 |
| 1.1     | Added comments section    | Emmanuel Antonio Ramirez Herrera | 05/01/2024 |
```

But if the modifications are major changes to the document, go to the next integer version:
```md
| Version | Description                                          | Responsibles                     | Date       |
|---------|------------------------------------------------------|----------------------------------|------------|
| 1.0     | Standard creation                                    | Emmanuel Antonio Ramirez Herrera | 03/01/2024 |
| 2.0     | Reworked standards to fit current organization needs | Emmanuel Antonio Ramirez Herrera | 04/01/2024 |
```


### Non-Markdown documents

From time to time you might need to create non-markdown documents, this wiki has no support to render non-markdown documents, so:
- It is a must to create one markdown document per non-markdown document. 
- The non-markdown document needs to be placed in the `/static/` directory. 
- The markdown document needs to describe the contents and objectives of the non-markdown document.
- The markdown document must provide a download link of the non-markdown document.
```md title="Download linking with markdown"
<a target="_blank" href={ require("/non-static-folder-path-to.file").default } download>Your text</a>
<a target="_blank" href="/static-folder-path-to.file" download>Your text</a>
``` 

### Linking documents

You will need to link documents between them, but there are 2 ways we link those documents, one would be with a simple link:
```mdx
Either with normal markdown syntax
[text of your link](/some-path)
Or with html syntax
<a href="/some-path">text of your link</a>
```
And the other one would be with embeded markdowns with mdx "accordions":
```mdx
import SomeDocument, { someDocumentTitle } from '/path-to-markdown-file.md';

<details>
  <summary>{someDocumentTitle}</summary>
  <SomeDocument />
</details>
```
If your document will only be mentioned as extra reference material, use the simple links, but if the document will be an essential part, use the "accordion" instead.

## Versions

| Version | Description                                               | Responsibles                     | Date       |
|---------|-----------------------------------------------------------|----------------------------------|------------|
| 1.0     | Standard creation                                         | Emmanuel Antonio Ramirez Herrera | 05/01/2024 |
| 1.1     | Add modifications section                                 | Emmanuel Antonio Ramirez Herrera | 05/01/2024 |
| 1.2     | Add non-markdown documents and linking documents sections | Emmanuel Antonio Ramirez Herrera | 08/01/2024 |