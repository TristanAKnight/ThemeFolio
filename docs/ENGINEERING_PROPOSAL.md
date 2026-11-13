> Public GitHub edition. Internal grading and self-assessment material from the working review copy has been omitted. Technical scope, evidence boundaries, acceptance criteria, risks, and release gates are preserved.

# ThemeFolio
Executive Product and Engineering Proposal — Revision 3.0
Prepared: November 12, 2026
Review audience: Joint project owners, Tristan, senior engineering reviewers, prospective contributors
Status: Specification and technical-contract proposal; the ThemeFolio application has not been built
Requested decision: Authorize a restricted browser-local prototype only after Gate 0 contract review
Provisional project name: ThemeFolio (name, package namespace, and trademark clearance pending)
Proposed license: MIT for original application code; demo artwork and third-party materials licensed separately
Revision note (November 12, 2026): This version consolidates the verified prior engineering specification with the later research brief. It is a newly produced document, not the missing original Deep Research attachment. Technical claims about unbuilt features are acceptance requirements, not observations of working software.
## 1. Executive determination
ThemeFolio is an offline, browser-based tool for designing, previewing, validating, and exporting reusable visual themes for note-like web interfaces. It provides designers with a reliable way to turn background art, typography, spacing, colors, and visual states into a versioned developer handoff without publishing their personal notes or relying on a cloud service.
Product promise: Create a notes-inspired theme, preview it at realistic sizes, and export a package that a web developer can integrate without guessing how the colors or assets map to the interface.
ThemeFolio is not a notes application, browser extension, theme marketplace, image generator, or automatic installer for Apple Notes, Notion, Obsidian, or any other named product. The first release targets only an intentionally documented generic HTML/CSS consumer. Compatibility with specific note-taking applications requires separately built, tested adapters and explicit authorization from their users.
Executive recommendation: Approve an isolated, offline proof that establishes a correct two-variant theme-pack contract, an accessible preview, safe image processing, and one independently developed sample host consuming the output. Do not authorize a general-purpose theme editor or third-party integrations before the proof passes.
What success looks like: A designer imports an original local illustration, adjusts tokens and positioning in a preview, sees honest accessibility findings, exports a privacy-sanitized ZIP, and a developer uses its CSS and assets in an independent sample notes UI. No artwork is silently modified at its original location; no personal note data or network request is required.
## 2. Problem, user, and evidence hierarchy
A wallpaper or stationery image is not by itself an application theme. Developers also need background layout rules, readable text colors, focus indication, selection and control states, responsive positioning, source-asset permissions, and a documented format. Designers often supply a reference PNG without these specifications, and programmers improvise missing decisions. This costs iteration time and may damage the creative design.
Primary persona: A digital stationery / creative UI designer who wants to deliver a portable, developer-ready visual treatment. The user is comfortable selecting assets and colors but may not know JSON, CSS, Git, or Node.js.
Secondary persona: A web developer integrating a design into a notes or journaling interface. The developer expects predictable file references, semantic tokens, CSS classes, and explicit limitations.
Excluded initial persona: A consumer who wants a one-click theme installation into an unrelated proprietary app.
Observed problem evidence: Repeated production requests involving decorative parchment backgrounds, editable note areas, mobile/desktop wallpaper proportions, and strict visual continuity show that the founder workflow exists. This supports exploration, not a claim of community demand. Independent usability testing must determine whether ThemeFolio saves more time than an HTML page and a CSS-variable template.
Hypotheses and proposed falsification:
H1 — usability: A designer can create a coherent light/dark theme and export it without writing code. Falsify if fewer than 8 of 10 users finish independently after a short README-based introduction.
H2 — portability: A developer can render both variants using only published pack documentation, without reading ThemeFolio's internal source. Falsify if the independent sample host requires undocumented token mapping or private helper code.
H3 — privacy: A normal export omits all tested EXIF/XMP/IPTC/device/location metadata and never sends the asset to a remote service. Falsify with one verified leak.
H4 — incremental value: At least five of ten pilot participants identify a measurable advantage over a manually written CSS template. Otherwise consider releasing a lightweight starter template rather than a new app.
## 3. Differentiation and competitive baseline
Niche: Local-first, image-aware, developer-handoff themes for notes-style HTML/CSS interfaces, especially designs with decorative borders or illustrated stationery. The novelty claim is workflow integration, not a novel token standard, compression algorithm, or accessibility evaluator.
Competitive test: Give users the same synthetic background and requirements; compare ThemeFolio against a manual HTML/CSS starter. Record first-export time, number of invalid outputs, time to integrate into a separate host, perceived friction, and the number of visual or accessibility discrepancies found. Predeclare criteria before recruitment.
## 4. Locked scope for the first release
4.1 v0.1.0 — mandatory features
Offline editor: A static, prebuilt web application that opens from a downloaded distribution without requiring Node.js, a remote server, an account, a CDN, or telemetry. Development may use TypeScript and Vite; end users must receive bundled files.
Three synthetic preview screens: blank page, prose note, and checklist. Text remains selectable, editable in the preview where appropriate, and represented as actual DOM text rather than a flattened PNG.
Two required variants: explicit light and dark themes, each with all required semantic colors and spacing tokens; an accessible system-theme default and an explicit override.
Curated theme controls: theme name, known system-font stack, text size, line height, spacing, radii, six required semantic colors, optional decoration opacity/position and locally selected image.
Static raster input: JPEG or PNG only, single image at a time for v0.1. WebP, SVG, GIF, animated formats, image-to-image editing, masks, font-file uploads, and user-authored HTML/CSS are excluded.
Preview versus export distinction: Preview the local original without modifying it. Export a new, sanitized, bounded image copy or fail closed; never silently overwrite the source.
Portable pack: ZIP with manifest.json, two DTCG-2025.10-compatible token subset files, theme.css, preview.html, a processed image when present, a rights notice, and a file-integrity index.
Deterministic structural validation: schema checks, exact path references, color and dimension constraints, generated CSS sanity, image decoding limits, and verification that every referenced artifact is packaged.
Accessibility diagnostics: calculate WCAG 2.2 text contrast for declared opaque color pairs, check focus/UI contrast in the sample preview, flag image-backed reading areas for manual inspection, and provide an evidence-based accessible-report summary.
Usability and security tests: keyboard-only flows, safe-file handling, zero network requests, sanitized output, and correct handling of restrictive/browser file-URL environments.
4.2 Explicitly out of scope
No direct host-app installation, note sync/storage, personal notes import, theme-pack import, arbitrary ZIP unpacking in the editor, arbitrary CSS, JavaScript or SVG upload, third-party typefaces, marketplace, billing, collaboration, image generation, social sharing, AI-assisted design, unattended publication, or blanket WCAG conformance certification.
Correction from the previous proposal: Tests for malicious ZIP imports and ZIP bombs in uploaded packs are removed from the v0.1 acceptance set because ZIP import is not shipped. Tests for escaping generated output names, ZIP-entry membership, safe extraction by the QA harness, and maximum output size remain mandatory.
4.3 Later releases — not current promises
v0.2 candidates: More token types, art-background presets, validated host adapter for one explicitly selected open-source notes app, non-destructive re-import of ThemeFolio's own manifest, and deliberate export presets.
Future research only: Marketplace and subscriptions, paid asset packs, automatic accessibility assistance for image-backed text, collaborative editing, or externally sourced templates.
Each later feature requires a separate contract, risk review, testing budget, and user-demand evidence.
## 5. Normative theme-pack contract (version 1.0.0)
Artifact identity: A ZIP produced by ThemeFolio is a generic web theme package. Its format identifier is themefolio-pack-1; schemaVersion belongs to the pack manifest, while each DTCG-compatible token document declares the supported producer profile separately in the manifest.
5.1 Fixed ZIP structure
my-theme.themefolio.zip
  manifest.json
  tokens/light.tokens.json
  tokens/dark.tokens.json
  theme.css
  preview.html
  LICENSES.md
  validation-report.json
  SHA256SUMS.txt
  assets/background.png              # only when an image is selected
manifest.json explicitly maps each variant to its own token file. No fallback or implicit inheritance between light and dark modes is permitted in v0.1. Missing required tokens in either mode block export. The generated theme.css has a fixed mapping for all required semantic tokens. A host needs only the pack, not the ThemeFolio application, to read and render its contents.
5.2 Required semantic token vocabulary
All sRGB components are finite numbers in [0,1], with optional 6-digit hex fallback consistent with the components up to rounding tolerance. No user-defined aliases, color spaces beyond sRGB, composite tokens, or arbitrary token names are accepted in v0.1. This is a restricted compatible subset of the DTCG format, not a claim of full DTCG resolver conformance. The 2025.10 community report is not a W3C Recommendation.
Font controls: Font-family choice belongs to ThemeFolio's typed manifest setting, not to an invented DTCG token. v0.1 supports a short, fixed list of system stacks (system-ui, Georgia, serif, Arial, sans-serif). Font size and line height are constrained style settings (14–24 px; 1.35–2.0); the pack's export validator converts these to fixed CSS properties after range validation. Font files are never imported or bundled.
5.3 Normative variant resolution
data-theme="light" on the host's document root wins and uses only the light tokens.
data-theme="dark" wins and uses only the dark tokens.
With no explicit data-theme, prefers-color-scheme: dark selects dark; otherwise select light.
A missing token, conflicting mode definition, unknown schema major version, nonnumeric component, or invalid CSS-setting enum is a blocking export error.
A host that does not provide the expected [data-theme] attribute receives the system-preference fallback. preview.html demonstrates the same exact logic and selectors.
No token value is inferred from the other variant or from background-image color sampling.
CSS mapping, normative: color.paper -> --tf-paper; ink -> --tf-ink; mutedInk -> --tf-muted-ink; border -> --tf-border; focus -> --tf-focus; accent -> --tf-accent; dimension.padding -> --tf-padding; dimension.radius -> --tf-radius. The exporter serializes values from a typed and allowlisted representation. CSS URLs can only point to generated local asset names, never external URLs or input strings.
5.4 Example manifest (illustrative source for a separately validated fixture)
{
  "schemaVersion": "1.0.0",
  "format": "themefolio-pack-1",
  "id": "example-parchment",
  "name": "Example Parchment",
  "variants": {
    "light": "tokens/light.tokens.json",
    "dark": "tokens/dark.tokens.json"
  },
  "stylesheet": "theme.css",
  "preview": "preview.html",
  "style": {
    "fontStack": "georgia",
    "fontSizePx": 16,
    "lineHeight": 1.6,
    "backgroundPosition": "center",
    "decorationOpacity": 0.20
  },
  "background": null,
  "outputPolicy": "metadata-sanitized"
}
A background-enabled manifest replaces null with a typed generated asset record containing a safe path, PNG MIME type, pixel dimensions, sha256 of exported bytes, and a separate license/rights declaration. The original file path, camera information, local source hash, or personally identifying note text is never placed in a public pack manifest.
5.5 Portable sample host requirement
A second, independently implemented sample notes UI must load the generated theme.css and asset references from an extracted pack, render both modes, and demonstrate the three preview components. The host must not import ThemeFolio's internal TypeScript modules. This is the central proof of format portability.
No host-app compatibility is implied until a particular adapter has been separately coded and tested against its actual API.
## 6. Offline architecture and distribution
Proposed development stack: TypeScript (strict), Vite for reproducible builds, a small DOM-driven UI without mandatory framework overhead, Ajv or a comparably reviewed schema validator, a vetted ZIP writer, and Playwright plus axe-core for testing. Vendor dependencies are pinned and license-reviewed. No backend, account system, or API key is required.
Modules: model, schema, tokens, image-inspection, image-sanitization, contrast, preview, css-export, pack-export, file-integrity, and ui.
Data flow: Local user file -> validate image signature, decode and resource limits -> obtain temporary in-browser object URL -> update controlled CSS variables -> validate semantic tokens/contrast -> sanitize a copy for export -> verify sanitized image metadata -> construct canonical pack -> unpack-and-validate in the test runner. No file crosses a network boundary.
Distribution contract: End users download a prebuilt themefolio-offline.zip containing index.html, compiled JavaScript/CSS, and locally bundled dependencies. They can open index.html in supported desktop browsers without Node/npm; any file-URL restriction in a supported browser is a release blocker or must be solved by a supported local launcher included in the distribution. A GitHub Pages demo may be optional later, but the offline build is the source of truth.
Browser support to prove, not assume: Current stable Chromium, Firefox, and Safari desktop releases; an automated matrix plus manual smoke on Windows/macOS/Linux where practical. Mobile is a preview viewport in v0.1, not a certified mobile editor. Offline egress must be measured by browser request interception and network-disconnected launches.
State lifecycle: Files are in memory during the session; no service worker, IndexedDB, cookie, third-party analytics, or localStorage persistence in v0.1. Revoke object URLs after replacement/export/unmount. On page reload, users intentionally reselect sources. Display unsaved-change messaging before refresh only when browsers allow it, but do not claim crash recovery.
6.1 Offline distribution acceptance contract (clarified)
The end-user build must be delivered as a documented, self-contained index.html bundle (or an equivalently packaged no-install desktop wrapper). The design cannot depend on fetch() of local JSON, ES module imports blocked under file://, external Google Fonts, remote icons, or service-worker registration in a browser context that disallows it. The release must prove a first-run from an extracted folder with Wi-Fi disabled, not merely a Vite development-server preview. An installation-free, no-network fallback is a first-class requirement; if all supported browsers cannot execute the chosen bundle safely under file://, revise the product claim and choose a documented self-contained installer before launch. A reference demonstration in a development browser is not sufficient.
Performance/incident contract: The release must include a test fixture at the maximum allowed raster size; stop decode or export on budget failure; revoke temporary image URLs; and preserve the original input bytes unmodified. Report memory peaks and failure modes by browser/device class rather than asserting universal responsiveness.
## 7. Image-input and metadata-security protocol
v0.1 accepted: single static PNG or JPEG image, one active image per theme. Max original file 10 MiB, max dimensions 4096 x 4096, max decoded 12 megapixels, and max total image-memory budget 128 MiB on the reference desktop browser. Reject multi-frame/animated sources, unsupported image types, malicious signatures, truncated files, size bombs, and decoders that cannot prove a successful bounded decode. Do not trust extensions or supplied MIME type alone. The numbers are initial policy limits, subject to measured prototype validation; raising them requires an explicit ADR.
Metadata/privacy contract:
Local preview may display the source image as selected. The application must not rewrite it or upload it.
Before export, render the correctly oriented decoded image into a fresh pixel buffer, convert to sRGB under an explicitly tested policy (or block export if color handling cannot be validated), and encode a new, metadata-minimal PNG through a pinned, tested encoder.
Strip EXIF, XMP, IPTC, location, device strings, thumbnails, comments, arbitrary text chunks, and unknown ancillary metadata from the exported copy. Only specifically needed visual/color information may be retained, after an allowlist review.
Reopen the exported PNG using an independent metadata inspector in QA. Any unexpected chunk or metadata field is a blocking privacy failure.
The user receives an explicit warning that color appearance, compression size, and file bytes may change during export. The original remains unchanged. A new output hash describes exported bytes, not the input file. The app never labels sanitized files exactly preserved.
When sanitization or metadata verification cannot be completed safely, fail closed: no export of a possibly sensitive original by default.
There is no preserve-original-metadata switch in v0.1. If a private archival export is desired, develop it as a separate future feature with explicit confirmation and a distinct non-shareable status.
File names: Output image is generated from a safe tool-controlled slug such as assets/background.png. User-provided file names, EXIF tags, and original absolute paths never determine ZIP entry names. Input filename is shown as escaped text only in the local editor.
ZIP export safeguards: The exporter emits only the fixed list of known relative paths. It sorts paths, refuses duplicates, forbids ../absolute/backslash paths, caps total uncompressed pack size at 20 MiB, and validates a clean extraction in QA. ZIP import into ThemeFolio is out of scope, so malicious ZIP import and decompression-bomb tests are reserved for a future import feature.
7.1 Public-export metadata and color-policy gate
A public-distribution ZIP may include only re-encoded, sanitized copies of user-supplied raster images. The export pipeline must intentionally exclude EXIF, GPS, IPTC, XMP, PNG textual chunks, embedded thumbnails, and any unreviewed freeform metadata. ICC profiles are also metadata, but removing them may change color interpretation: users must be warned and the sanitized copy must pass a defined visual-fidelity review on supported browsers. The system must not claim universal visual preservation from metadata stripping alone. If a source format or color profile cannot be handled without uncontrolled metadata disclosure or unacceptable display changes, fail the public export with a specific error. Never silently modify the original.
Personal-use local export and public-redistribution export are different actions. A personal pack may carry the rights status unverified with a prominent warning; a public pack requires an explicit rights declaration by its distributor. That declaration records user intent, not a legal finding made by ThemeFolio.
## 8. Portable CSS and generated preview security
CSS generation: Never concatenate arbitrary user-defined CSS. Validate all token values through typed enums and numeric bounds; generate CSS with a fixed template and escaped, allowlisted local asset references. No @import, external url(), JavaScript, embedded fonts, or remote assets. Generated preview.html uses static text and elements, a local stylesheet, and no inline user-supplied script or HTML. DOM fields are inserted using safe text APIs in the app.
CSP: Offline app and generated preview must enforce a tested restrictive Content Security Policy appropriate to file/localhost distribution, without unsafe-eval or untrusted inline script. connect-src 'none', disallow remote fonts and frames, and allow only expected local static resources and session-local image blobs. CSP is a defense layer, not a replacement for typed serialization. The delivery build and the generated preview may need different policies; document both and test in each supported browser.
Pack integrity: SHA256SUMS.txt covers every pack file except itself, with LF-delimited, sorted relative paths and SHA-256 hashes of final bytes. The QA harness extracts the ZIP into an isolated directory, checks each hash, validates the schemas, and renders the preview offline. These hashes detect accidental changes, not authentic authorship. Published release provenance needs a separate release-signing policy.
Determinism: The exporter fixes entry ordering, timestamps, filename encoding, line endings, JSON key serialization, and ZIP compression settings. Byte-identical ZIPs are targeted only within the same pinned encoder/runtime/build after tests demonstrate it. Across browsers, require equivalent extracted files, schema validity and content hashes rather than falsely guaranteeing the same compressed archive bytes.
## 9. Accessibility contract and evidence
The preview's live text must be keyboard selectable and responsive; theme settings cannot obscure content or cause horizontal scrolling at the defined viewports.
Measured solid-surface requirements: Under WCAG 2.2 Level AA, normal text requires at least 4.5:1, large text 3:1, and visually necessary nontext UI boundaries/focus states generally 3:1 against adjacent surfaces. Focus indicators must be visible, states must not rely on color alone, and keyboard-only editing must be supported. Semantic CSS tokens for ink, mutedInk, accent (when used for text), border, and focus are checked against their intended opaque surfaces. Transparent overlay math, when used, must calculate actual composited colors rather than comparing uncomposited foreground/background tokens.
Illustrated backgrounds: A color-token contrast pass cannot certify legibility over a textured photograph. ThemeFolio places real editable text on the opaque semantic paper surface by default. Decorative images appear behind or outside that reading surface. If users enable text-over-art preview, label it manual visual review required with no “accessible” badge, even if a heuristic sample happens to pass.
Accessibility acceptance set: keyboard tab order, visible focus, screen reader labels, no color-only state distinctions, support for 200% browser zoom, minimum 320 CSS px viewport without lost editing controls, meaningful display in high-contrast or forced-colors modes, prefers-reduced-motion, and no unexplained content clipping. Automated axe-core tests plus manual keyboard and screen-reader inspection are mandatory; automated tests are not presented as blanket WCAG certification.
Preview viewports for QA: 375 x 812 CSS px phone, 768 x 1024 tablet, and 1440 x 900 desktop, plus 320 px narrow viewport at 200% zoom. These are test targets, not claims that theme packages automatically work in every host.
## 10. Normative error, validation, and output contracts
Validation results have independent fields: schemaStatus, themeCompleteness, contrastFindings, assetStatus, privacyStatus, and packStatus. An export can be structurally valid but still fail a contrast rule or a privacy scan. No single green status hides these distinctions.
Issue model: Each finding uses a stable code, severity (error, warning, info), file/token location, and plain-English remediation. Examples: VARIANT_TOKEN_MISSING, COLOR_COMPONENT_INVALID, TEXT_CONTRAST_LOW, IMAGE_METADATA_PRESENT, ZIP_ENTRY_UNSAFE, PACK_REFERENCE_MISSING, and OFFLINE_EGRESS_DETECTED.
Export decision: Block when required light/dark tokens or semantic mappings are missing, an asset cannot be sanitized, the pack has unsafe entries or failed checksums, a required reading-surface text color falls below AA contrast, or unexpected network access occurs during validation. Warnings (e.g. image-backed manual contrast review, explicit unsupported host) remain visible in the required validation-report.json included in the pack. The tool never reports host-app compatibility as a passing test without a specific adapter.
Export status values: ready | blocked | unsupported for each independent check. The final pack is released only if every required check is ready, with all nonblocking warnings preserved in the mandatory validation-report.json. Errors contain no private file paths or embedded source metadata. The validation report schema is versioned alongside the manifest; it records only the result codes, broad locations, and redacted messages, not source filenames or user notes.
Backward compatibility: Unknown major pack versions fail with a descriptive message; minor additions must preserve existing required keys or require a new major version. Schema migrations are out of v0.1. All example outputs are checked against the exact same schemas that ship with the tool.
10.1 Reproducible export contract (release detail)
ZIP generation must define exact entry names and order (UTF-8, lexicographic), fixed timestamps, a pinned ZIP compression implementation and mode, normalized line endings, no platform-specific permission or owner fields, and no unrelated file attributes. A manifest hash index covers every packaged entry other than the index itself; the hash index uses a stable canonical order. Two exports in the same pinned supported build with identical inputs must produce byte-for-byte identical ZIP files, or the release is blocked. Cross-runtime byte identity is a separate acceptance claim requiring comparison across browser and operating-system builds. Invoking zip -X alone is not proof of deterministic output from a browser application.
## 11. Acceptance tests — release-blocking
Test scope correction: There are no ZIP-import tests in v0.1. Future pack-import support would require fresh work on entry limits, path traversal, decompression bombs, and trust boundaries.
Quality bar: All G1/G2 blocking fixtures pass before public beta, 100% of security-critical assertions pass, no verified metadata leak or network egress, no uncaught decode errors, no source mutations. Component/unit coverage target >=90% for token validation, pack manifest, CSS generation, and image sanitizer; metrics supplement rather than replace adverse-case tests.
## 12. Benchmarks, support matrix, and failure budgets
Representative baseline hardware: Midrange 4-core laptop, 8 GiB RAM, current stable desktop browser, SSD, offline. A fixture corpus contains 50 synthetic images including high-resolution valid files, malformed signatures, EXIF/XMP-heavy JPEGs, PNG ancillary chunks, edge-case colors and alpha, animated images, and graphics with intentional copyright-safe demonstration content.
Proposed initial thresholds (not measured results):
Start prebuilt offline editor and display synthetic preview in <=3 seconds on baseline hardware (cold start, cached files disabled).
Preview a valid <=6 MP imported image and respond to token changes within 500 ms after decode; no network requests.
Complete an export with one <=10 MiB input in <=10 seconds on baseline hardware, or provide a nonblocking progress state and explicit failure.
Keep peak heap <=256 MiB and object URLs revoked after replacement/close. Monitor browser memory where available and document measurement limitations.
Preserve input bytes (SHA-256 before/after) with zero deliberate writes to selected source files.
If targets fail, record why and revise the specification through review rather than claim a passing benchmark. Do not promise identical timing on low-powered phones not in the supported editor matrix.
Support matrix: Chrom(e|ium), Firefox, Safari desktop on current stable releases where supported by OS. Required checks on Windows, macOS, Linux for feasible browsers; Safari is macOS-only. The CI matrix identifies simulated versus actual OS/browser runs. No “tested on every platform” statement before logs exist.
## 13. Delivery milestones, ownership, and budget control
Estimates are engineer-days, not calendar promises, and are subject to Gate 0 prototype findings.
Ownership: Technical maintainer owns security-critical export code, schema versioning, dependencies, CI, and release artifacts. Creative/product maintainer owns note-screen usability, sample themes, accessibility design review, explanatory text, interviews, and review of public-safe imagery. Both owners approve licensing, public examples, release publicity, and scope changes. A second reviewer is required for changes to sanitization, generated HTML/CSS, or published schemas.
Cost assumptions: No hosted backend or paid API. Costs are engineering effort, browser/device QA, design/accessibility reviews, and ongoing maintenance. Optional static project website is not required for the actual editor to function.
## 14. Pilot design and go/no-go metrics
Recruit 10 independent participants representing designers and developers. Test each using only newly created, license-cleared synthetic note backgrounds. Give participants a simple task: select a background, produce two accessible variants, export, and use the pack in a documented sample host. Compare against a conventional CSS-variables template with the same assets.
Record: time to first preview and export, whether participant needed coaching, exported validation errors, incorrectly inferred host support, missing/unclear rights notices, time for a developer to integrate the output, and whether both variants reproduce the reference preview.
Proceed if: >=8/10 finish core editing/export unaided; >=8/10 understand that the output is not an Apple Notes/Notion/Obsidian installer; zero privacy/security acceptance failures; all sample hosts integrate both variants; >=5/10 identify measurable advantage over manual CSS or reduced handoff ambiguity. These are pragmatic exploratory thresholds, not statistical market proof.
Pivot/stop if: Manual CSS starter gives equivalent results with less friction, image sanitization cannot be validated safely at reasonable effort, file-URL offline distribution proves unreliable without unacceptable installation steps, or no maintainer will assume long-term responsibility.
## 15. Legal, intellectual property, and release governance
Public repository: New clean Git history; original source, synthetic assets, demo note text, versioned schemas, test fixtures, public license metadata, README, CONTRIBUTING.md, SECURITY.md, changelog, and test instructions. Never include private notes, proprietary game art, character reference imagery, client files, private project logs, passwords, or previous proprietary repository history.
Code licensing: Proposed MIT, subject to co-owner agreement and dependency review. Demo artwork receives separate and explicit terms. Users may preview their own images locally without the tool adjudicating ownership, but exported packs must label redistribution rights honestly. A rights value of unverified is allowed for a personal local export and is not sufficient to present the pack as cleared for public redistribution. The tool does not grant rights to any user-supplied artwork.
Release safety: Pin direct dependencies, review transitive licenses, use least-privilege CI, publish checksums, maintain a supported-browser policy, issue a security disclosure mechanism, and document patch/maintenance ownership. ThemeFolio is not authorized to make changes to users' GitHub repositories or Google Drive unless asked separately in a later task.
Name availability: ThemeFolio remains provisional. Package-name, repository-name, and trademark searches must occur before public branding; this proposal does not assert clearance.
## 16. Risk register and stop conditions

## 18. Final recommendation for Tristan
Approve Gate 0 and a bounded Gate 1 prototype, not a full product commitment. The MVP is intentionally smaller, its claims are testable, its export format has a normative definition, and its critical privacy and accessibility boundaries are explicit. The crucial launch proof is an independently consumable light/dark theme pack containing only safe, properly licensed demonstration assets.
If the independent host cannot read the pack or a privacy test identifies unremoved metadata, halt release until corrected. If users gain little over a CSS-variable template, publish the template and stop expanding the application.
The contribution worth making publicly is a dependable, honest design-to-developer handoff for notes-style themes—not an unrealistic promise of universal theme installation.
## Standards and background sources
Design Tokens Community Group, Format Module 2025.10, Final Community Group Report: https://www.w3.org/community/reports/design-tokens/CG-FINAL-format-20251028/
Design Tokens Community Group, Color Module 2025.10, Final Community Group Report: https://www.w3.org/community/reports/design-tokens/CG-FINAL-color-20251028/
W3C, Web Content Accessibility Guidelines (WCAG) 2.2: https://www.w3.org/TR/WCAG22/
MDN, Content Security Policy: https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/CSP
OWASP, File Upload Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html
GitHub Docs, Licensing a repository: https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository
Document control: ThemeFolio Revision 3.0 / November 12, 2026 / independent technical review requested / software not yet implemented.
Research review and verification note
The proposed designs rely on published technical standards and recognized security guidelines, but the application-specific engineering choices require testing. ThemeFolio references the Design Tokens Community Group format and WCAG 2.2; SiteCustody references JSON Schema, OWASP guidance, and ICANN registrar-information policy. All claims of market demand, usability savings, metadata safety, deterministic exports, and implementation readiness remain subject to the explicit gate tests above. This document intentionally does not award its own 105-point rating.
Alternative
Strength
Where ThemeFolio may add value
What ThemeFolio does not replace
Manual HTML and CSS variables
Free, flexible, universally understood by developers
No-code visual editing, responsive previews, safe pack export, validation
General web development
Full design editors (e.g. Figma)
Rich layouts and collaboration
Smaller offline handoff with no account, notes-specific preview components
Collaborative design suites
Existing notes apps and themes
Actual in-app experience
Host-neutral design assets a developer can incorporate
The apps or their plugin systems
General design-token tools
Token resolution and broad interoperability
A curated semantic subset, visual note templates, export privacy rules
Comprehensive DTCG tooling
Token path in each variant
Type
Usage
Requirement
color.paper
DTCG color (sRGB)
Opaque note reading surface
Required; alpha = 1
color.ink
color
Normal text
Required; 4.5:1 against paper
color.mutedInk
color
Secondary text
Required; 4.5:1 against paper if normal size
color.border
color
Meaningful boundary
Required; 3:1 when conveying structure
color.focus
color
Focus ring / visible selection
Required; 3:1 at relevant adjacent surface
color.accent
color
Link/control emphasis
Required; >=4.5:1 when used as normal link text; not sole state signal
dimension.padding
DTCG dimension in px
Content inset
Required, 12–64 px
dimension.radius
dimension in px
Panel radius
Required, 0–32 px
ID
Scenario
Expected result
Gate
TF-01
Valid light/dark token documents and manifest
Export allowed; each token resolves to documented CSS
G1
TF-02
Missing color.ink only in dark mode
VARIANT_TOKEN_MISSING, export blocked
G1
TF-03
Invalid DTCG sRGB component or unsupported token
Explicit error, no guessed coercion
G1
TF-04
No data-theme, system prefers dark
Dark tokens applied; light selected otherwise
G1
TF-05
data-theme="light" overrides dark system preference
Light CSS wins; no cascade conflict
G1
TF-06
Import valid static PNG/JPEG
Preview succeeds, original bytes unchanged
G1
TF-07
SVG, HTML pretending to be image, animated source
Rejected without executing content
G2
TF-08
Corrupt or over-limit image
Bounded error; no uncontrolled allocation
G2
TF-09
EXIF GPS/device, XMP, IPTC, PNG text chunks
Exported copy independently verifies metadata-free
G2
TF-10
Sanitizer fails or inspector detects metadata
Export blocked, original unchanged
G2
TF-11
Attempt path traversal via original filename
Export uses tool-generated safe path
G2
TF-12
ZIP output has missing, duplicate or unsafe entries
Blocked; no ZIP import required
G2
TF-13
Unpack pack and recompute SHA-256 index
All exported file hashes verify
G2
TF-14
Export identical inputs twice in pinned runtime
Byte-identical archive under tested runtime; extracted contents equivalent across browsers
G2
TF-15
Load exported pack in independent sample host
Both variants render with no ThemeFolio internal imports
G2
TF-16
Regular text contrast 4.49:1
Error; export blocked on required reading surface
G1
TF-17
Large text/nontext thresholds and focus ring
Correct threshold and labeled errors
G2
TF-18
Text over illustrated image
Manual review finding, no automated accessibility certification
G2
TF-19
Keyboard, reduced motion, zoom, forced colors
No lost functionality in defined matrix
G2
TF-20
No Internet, offline launched from distribution
Editor and exported preview operate offline
G2
TF-21
Browser network instrumentation
Zero outbound traffic, no telemetry
G2
TF-22
XSS/CSS injection strings in theme name/settings
Escaped/denied; no script or arbitrary URL execution
G2
TF-23
Asset with rights marked unverified
Cannot be labeled redistribution-cleared; warning remains in local pack
G2
TF-24
Public example image license inventory
All shipped public fixtures have deliberate permission metadata
G3
TF-25
Schema and golden-pack regression across builds
Compatible semantic content or explicitly versioned change
G3
TF-26
Manual release build / code signing, dependency audit
Auditable artifact checksum, pinned versions, clean install
G3
Gate
Deliverable
Estimate
Objective go/no-go
G0 — contract
Full pack JSON Schema, two-variant token fixture, CSS map, threat model, benchmark plan
3–5 days
Independent reviewer can consume pack contract without internal knowledge
G1 — editor proof
Offline UI, three previews, two variants, token validation, WCAG solid-color checker
8–12 days
TF-01–06 and TF-16 pass; no undocumented variant behavior
G2 — safe export
Sanitized static images, bounded ZIP, independent sample host, security/accessibility QA
9–15 days
TF-07–23 pass; no leaks or unwanted network requests
G3 — community/release
Pilot tests, bug fixes, packaging, README/security/license review
4–7 days
TF-24–26; user trial threshold and clear maintainer assignment
Total
Conditional release candidate
24–39 engineer-days
All gates pass or project is simplified/stopped
Risk
Probability / severity
Mitigation
Stop/review trigger
Feature adds little over CSS template
Medium / high
Measured competitor workflow
Trial finds no improvement
Export leaks EXIF, XMP or private fields
Medium / critical
Re-encode and independently inspect; fail closed
Any verified metadata leak
Theme pack cannot be consumed independently
Medium / high
Sample host written separately
Host requires private ThemeFolio internals
Overstated accessibility claims
Medium / high
Solid-color verification + manual image checks
Automatic tool certifies image-backed text
Offline build works only in developer environment
Medium / high
Prebuilt artifact and per-browser offline tests
End user must install Node/network runtime
Unbounded image decoding / memory exhaustion
Medium / high
Strict caps, decoding budgets and worker isolation when justified
Browser crash or uncontrolled allocation
Token standard drift
Medium / medium
Versioned subset and spec-based fixtures
Unsupported tokens silently coerced
Licensing confusion
Medium / high
Separate source/demo/user-art rights and export notices
Unverified user art marketed as reusable
No maintainer availability
Medium / medium
Signoff responsibilities and issue policy
No accountable release owner
