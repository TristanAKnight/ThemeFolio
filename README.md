# ThemeFolio

ThemeFolio is a proposed offline browser tool for designing, previewing, validating, and exporting reusable visual themes for note-like web interfaces.

**Current status:** engineering and technical-contract specification. The ThemeFolio application has not yet been built.

## Goal

ThemeFolio is intended to turn background art, typography, spacing, color tokens, and visual states into a versioned developer handoff without requiring a cloud service or exposing personal note content.

## Proposed v0.1

- prebuilt offline browser editor
- blank-page, prose-note, and checklist previews
- explicit light and dark theme variants
- curated semantic color, spacing, radius, and typography controls
- local JPEG/PNG preview with sanitized export copies
- portable ZIP pack with manifest, token files, CSS, preview, integrity index, and rights notice
- deterministic structural validation
- WCAG 2.2 contrast diagnostics for supported opaque color pairs
- explicit manual-review status for image-backed reading areas
- zero expected network traffic or telemetry during normal use

## Explicit boundaries

ThemeFolio is not a notes app, browser extension, theme marketplace, image generator, or automatic installer for Apple Notes, Notion, Obsidian, or other named products. The first release targets a documented generic HTML/CSS consumer.

## Evidence standard

The repository currently contains the specification, not proof that browser packaging, metadata stripping, deterministic ZIP output, accessibility behavior, or cross-browser resource limits have passed release testing.

## Decision gate

Gate 0 defines the pack contract and threat model. Gate 1 is a restricted offline editor proof. If users gain little over a conventional CSS-variable starter, the project should publish the simpler template and stop expanding the application.

## Documentation

- [Engineering proposal](docs/ENGINEERING_PROPOSAL.md)

The Drive copy remains the archival working document. This repository contains the public engineering edition.
