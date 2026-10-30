# Unified Supplier — data preparation flow

A clickable HTML prototype of the "Prepare to adopt Unified Supplier" flow: the
four-step wizard a customer walks through to review field mappings, resolve data
discrepancies, and set sub-object matching keys before migrating to the unified
supplier record.

It is a single self-contained HTML file plus an `assets/` folder of SVGs. No build
step, no dependencies, no server.

## Running it

Open `supplier-data-sync-flow.html` in a browser. A dark toolbar across the top
lists every screen so you can jump straight to one; the happy path starts at
**Setup** and follows the in-page buttons from there.

You can also deep-link to a screen with a URL fragment, e.g.
`supplier-data-sync-flow.html#step2b`.

## The flow

| Screen | Toolbar button | What it covers |
| --- | --- | --- |
| Setup | `Setup` | The Coupa Setup page the flow is entered from |
| Step 1 | `1 · unchecked` / `1 · checked` | Review sync settings and custom fields; the checkbox gates **Continue** |
| Step 2 | `2 · Details` / `2 · Addresses` | Custom field comparison — connected, unique, type-mismatched and inactive fields |
| Step 3 | `3 · Discrepancies` | Every standard and custom field with a per-field discrepancy count, CSV report and corrections upload |
| Step 4 | `4 · Sites & Remit-to` | Sub-object matching keys for sites, remit-to, contacts and addresses |
| Errors | `E · …` | The four error and validation states |

## What is interactive

- **Step 1** — the verification checkbox switches **Continue** between its inert and
  active states.
- **Step 2** — the Details / Addresses tabs swap the comparison tables.
- **Step 3** — each row is independent: downloading that field's CSV is what enables
  its upload control, and uploading shows the file and a **Remove** link. Rows do
  not affect each other.
- **Step 4** — each of the four cards is a small state machine. The first answer
  decides whether a follow-up question appears and which alert resolves the card;
  changing the first answer resets the follow-up.
- **Confirm Changes** opens the confirmation modal and returns to Setup.

## Fidelity notes

Layout, spacing and colour come from the Figma source and were verified by
pixel-comparing rendered output against the design frames. A few deliberate
departures:

- Step 4 cards grow with their content instead of reproducing the design's fixed
  card height, because the design's leftover space varies between variants
  (19–82px) in ways that read as unintentional.
- Step 4 cards keep their own titles in answered states; some design variants
  revert them to the first card's title.
- The step 3 table has no Clarity table component to draw on, so it reuses the
  MUI-based table already in the design, styled with Clarity tokens.
- The step 3 download and upload controls are text buttons — the equivalent
  Clarity icons were not available to export.

`render/` holds reference screenshots of each screen.
