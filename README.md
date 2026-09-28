# AppCatalog.Divooka.Com
A static host of available apps, including catalog and actual app programs as bundled .dvk files.
# Publishing for Divooka Viewer

`index.json` is the versioned catalog consumed by Divooka Viewer. Category names are case-sensitive; the Calculator is published in `Examples` and its files are under `/Examples/`. This repository intentionally hosts release binaries as static website content.

Build the Calculator from Divooka Explore's `Examples/GUI/Calculator.dvk` using Parcel NExT's `Automation/DivookaViewer/BuildDivookaViewer.ps1 -Distribution <Explore-distribution> -Target Catalog`. Copy the generated `Catalog/index.json`, `.dvk` and `.dvkapp` files here. Review the diff and publish through the main-branch Pages workflow. Do not upload the build-tools distribution or generated C# files. Preserve existing catalog entries when adding an app.

A `.dvkapp` is a flat ZIP with `manifest.json`, `app.dvk`, `graphs.json` and its compiled .NET assembly. The source and graph render models come from the same document. Runtime v1 supports compiled `GUIApplication` graphs without desktop-only host dependencies; run the Parcel verification program before publishing. Every package must be reviewed: downloaded code runs with Viewer’s permissions, not in an isolated sandbox. Describe any network access or data collection in the app description. Calculator has neither.

Use a new version and file name for each release, calculate `bytes` and lowercase SHA-256 from the finished package, and update the catalog last. The schema is in `catalog.schema.json`. Viewer rejects unsupported schema/runtime versions, invalid sizes, unsafe archives and URLs outside the official HTTPS catalog origin. Keep older release files available so cached catalog entries continue to download.
