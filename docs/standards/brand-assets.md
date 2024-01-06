---
description: Standards about how to use branding
tags: [brand, assets, logo, typography, color-palette]
---

# STD - Brand assets

## Objective

Describe the standards to follow to implement STRIXDEV branding correctly.

## Content

The main assets that are strictly related to STRIXDEV are the name, the color palette, the typographies and the logotype.

### Name

Every time you need to make reference to STRIXDEV, you need to write it with all capitals and all together.
```txt title="Examples"
❌ Strixdev
❌ Strix dev
❌ STRIX DEV
✅ STRIXDEV
```

### Color palette

If you need to generate any resource that belongs to STRIXDEV, you need to make sure you are implementing the color palette that is composed of the next colors:
- <span style={{width: "1rem", height: "1rem", background: "#EBF4FA", display: "inline-block"}}></span> <strong>Light</strong>: <code>#EBF4FA</code>
- <span style={{width: "1rem", height: "1rem", background: "#008EE8", display: "inline-block"}}></span> <strong>Primary</strong>: <code>#008EE8</code> 
- <span style={{width: "1rem", height: "1rem", background: "#000000", display: "inline-block"}}></span> <strong>Secondary</strong>: <code>#000000</code>
- <span style={{width: "1rem", height: "1rem", background: "#276D9B", display: "inline-block"}}></span> <strong>Accent</strong>: <code>#276D9B</code>

### Typography

There are two different typographies that are used by STRIXDEV, Iceland and Montserrat, Iceland is used for titles, labels and buttons. and Montserrat is used for body copy, labels, buttons, etc.
You can download both from next links:
- <a target="_blank" href={ require("/src/css/fonts/Iceland/Iceland-Regular.woff2").default } download>Iceland</a>
- <a target="_blank" href={ require("/src/css/fonts/Montserrat/Regular/Montserrat-Regular.woff2").default } download>Montserrat</a>

If you are using the typographies for a development and the tool supports multiple fallbacks, provide as many as you can, we recommend using [Transfonter](https://transfonter.org/) to generate those fallbacks.

### Logo

Logo will be used for business cards, letterheads, envelopes, websites, mobile applications, desktop applications and every item or feature developed for STRIXDEV, so it maintains a consistent branding either on printed or digital products.
Here you have some basic rules you need to follow when using the STRIXDEV logo:

- Make sure that the logo is not distorted and maintains a required aspect ratio and integrity.
- Vector formats are prefered (SVGs or EPSs) to avoid quality loss. 
- Ensure the colors in the logo are reproducted accurateley.
- You can use either the primary color or the light color, choose the color according to the best contrast.
- Make sure that the logo is not placed on a busy or clashing background. The background should be a complement and keep the logo visible, not hide it or distract from it.
- Use the right file format for the medium, color formats might vary from medium to medium. Using the wrong file format can lead to loss of quality or compatibility issues.
- Respect the minimum margin of the STRIXDEV logo to other elements: 32px.
- Always use the most up-to-date version of the STRIXDEV logo.

To download the SVG logo file, <a target="_blank" href="/img/logo.svg" download>click here.</a>

## Versions

| Version | Description       | Responsibles                     | Date       |
|---------|-------------------|----------------------------------|------------|
| 1.0     | Standard creation | Emmanuel Antonio Ramirez Herrera | 04/01/2023 |