
  This project uses docToolchain v3.4.1, which wraps several tools together:

  | Output    | Generator                 | Styling Method       |
  |-----------|---------------------------|----------------------|
  | HTML      | Asciidoctor 2.0.18        | CSS/inline styles    |
  | PDF       | Asciidoctor PDF 2.3.4     | PDF theme YAML files |
  | Microsite | jBake 2.6.4 + Docsy theme | GSP templates + CSS  |

  ---
  HTML Styling

  Two ways to customize:

  1. Inline styles in AsciiDoc - Already in use at documentation/internet-banking-system.adoc:14-25:
  ifdef::backend-html5[]
  ++++
  <style>
    /* your CSS here */
  </style>
  ++++
  endif::[]
  2. External CSS - Add these attributes to your AsciiDoc:
  :linkcss:
  :stylesheet: path/to/custom.css

  ---
  PDF Styling

  Currently not configured - the config shows it's commented out in docToolchainConfig.groovy:11-13.

  To enable custom PDF theming:

  1. Create a directory: documentation/pdfTheme/
  2. Add a PDF theme YAML file (e.g., custom-theme.yml)
  3. Uncomment/configure in docToolchainConfig.groovy:
  pdfThemeDir = './pdfTheme'

  The theme YAML controls fonts, colors, margins, page size, headers/footers, etc. See https://docs.asciidoctor.org/pdf-converter/latest/theme/.

  ---
  Microsite Styling

  Configured in docToolchainConfig.groovy:57-150:

  - Theme: Docsy (Hugo theme ported to jBake)
  - Site folder: ../site (relative to documentation folder - would be at project root)
  - Configurable options:
    - title - Site title
    - landingPage - Landing page template (landingpage.gsp)
    - menu - Navigation structure
    - Footer social links (mail, Twitter, GitHub, Slack, StackOverflow)
    - contextPath - Deployment path

  To customize the theme:
  1. Create a site/ directory at project root
  2. Add jBake template overrides (.gsp files)
  3. Add custom CSS
  4. Or set DTC_SITETHEME environment variable to a ZIP URL of a custom theme

  ---
  Key Files to Edit

  | What to Change                    | File                                       |
  |-----------------------------------|--------------------------------------------|
  | Main config                       | docToolchainConfig.groovy                  |
  | AsciiDoc attributes (TOC, images) | documentation/arc42/_config.adoc           |
  | Inline HTML styles                | documentation/internet-banking-system.adoc |
  | PDF theme                         | Create documentation/pdfTheme/*.yml        |
  | Microsite templates               | Create site/ directory with overrides      |

  ---
  Build Commands

  ./dtcw generateHTML      # Build HTML
  ./dtcw generatePDF       # Build PDF
  ./dtcw generateSite      # Build microsite
  ./dtcw previewSite       # Preview on localhost:8042