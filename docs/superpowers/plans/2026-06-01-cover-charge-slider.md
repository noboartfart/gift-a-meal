# Cover Charge Slider Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a cover charge slider to the review booking page that lets users set per-person table cover charges, with real-time total updates and supporting info cards.

**Architecture:** Single-file HTML prototype. Add new styles for the "about your gift" section, slider, and info cards. Replace removed sections. Add JavaScript to handle slider interactions, calculate totals, and manage share modal.

**Tech Stack:** Vanilla HTML, CSS, JavaScript (no frameworks)

---

## File Structure

**Modify:** `index.html`
- Remove: `rv-gift-comms` section (gifting to... card)
- Remove: `rv-refund-snippet` section (cancellation & refund)
- Add: `ag-section` (about your gift) with slider + 3 info cards
- Add: `ag-share-modal` (share details modal)
- Update: `rv-summary-card` to show cover charge breakdown
- Add: CSS for new sections + slider styling
- Add: JavaScript for slider logic + modal interactions

---

## Implementation Tasks

### Task 1: Remove "Gifting to..." Section

**Files:** `index.html` (lines ~4970-4995)

- [ ] Step 1: Locate the section by searching for `<div class="rv-gift-comms">`
- [ ] Step 2: Delete entire section including preceding comment
- [ ] Step 3: Commit with message "remove: gifting to section from review page"

### Task 2: Remove "Cancellation & Refund" Section

**Files:** `index.html` (lines ~5070-5125)

- [ ] Step 1: Locate section by searching for `<div class="rv-refund-snippet">`
- [ ] Step 2: Delete entire section including preceding comment
- [ ] Step 3: Verify next element is `<!-- Your details -->`
- [ ] Step 4: Commit with message "remove: cancellation and refund section from review page"

### Task 3: Add Styles for "About Your Gift" Section

Add CSS for:
- `.ag-section`, `.ag-card`, `.ag-header`, `.ag-subtext`
- `.ag-slider-group`, `.ag-slider-label`, `.ag-slider`
- `.ag-slider::-webkit-slider-thumb` and `.ag-slider::-moz-range-thumb`
- `.ag-slider-value`, `.ag-slider-total`
- `.ag-info-cards`, `.ag-info-card`, `.ag-info-icon`, `.ag-info-content`
- `.ag-info-title`, `.ag-info-text`, `.ag-share-btn`

Commit: "style: add about your gift section styles"

### Task 4: Add Share Modal Styles

Add CSS for:
- `.ag-share-modal-overlay`, `.ag-share-modal`
- `.ag-modal-header`, `.ag-modal-title`, `.ag-modal-close`
- `.ag-modal-content`, `.ag-sms-preview`, `.ag-sms-preview-label`, `.ag-sms-text`
- `.ag-modal-buttons`, `.ag-modal-btn`, `.ag-modal-btn-secondary`
- `.ag-modal-toggle`, `.ag-toggle-label`, `.ag-toggle-switch`, `.ag-toggle-dot`

Commit: "style: add share modal styles"

### Task 5: Add "About Your Gift" HTML Markup

Insert before `<div class="rv-card-alt">`:
- Main card with header, subtext
- Slider group with input range, label, display
- Three info cards (easy refunds, amount differ, share with guest)

Commit: "markup: add about your gift section with slider and info cards"

### Task 6: Update Booking Summary to Show Cover Charge

After "Gift Meal value" divider, add:
- Cover charge row (hidden by default)
- Cover charge divider
- Update to show "(₹X × Y guests)" sublabel

Commit: "markup: add cover charge row to booking summary"

### Task 7: Add Share Modal HTML Markup

Add modal overlay with:
- Modal header with title and close button
- SMS preview box
- Action buttons (copy, WhatsApp, email)
- Share after booking toggle

Commit: "markup: add share details modal"

### Task 8: Add JavaScript for Slider Logic

Add:
- `coverChargePerGuest` and `numberOfGuests` state variables
- `initCoverChargeSlider()` function with slider event listener
- `updateBookingSummaryTotal()` function
- DOMContentLoaded initialization

Commit: "js: add cover charge slider event listeners and calculations"

### Task 9: Add JavaScript for Share Modal

Add:
- `openShareModal()`, `closeShareModal()` functions
- `copySmsToClipboard()` function
- `shareViaWhatsApp()`, `shareViaEmail()` functions
- `initShareToggle()`, `initShareModal()` functions
- Event listener initialization

Commit: "js: add share modal interactions and handlers"

### Task 10: Update Guest Count Tracking

In `confirmGuests()` function, add:
- Update `numberOfGuests` when guests are selected
- Trigger slider input event to recalculate

Commit: "js: sync guest count with cover charge calculations"

### Task 11: Test the Feature

Manual testing:
- Slider interaction (drag, verify display updates)
- Guest count sync (change guests, verify cover charge scales)
- Info cards visibility (verify all 3 cards visible)
- Share modal (open, copy, share, toggle, close)
- Visual appearance (styling, animations, responsive)
- Removed sections (confirm they're gone)

Commit: "test: verify cover charge slider feature end-to-end"

---

## Success Criteria

✓ Cover charge slider is prominent in "About your gift" section
✓ Real-time updates work (slider input → display + booking summary total)
✓ All info cards visible (no hidden/collapsed content)
✓ Share modal is intuitive and functional
✓ Cover charge scales correctly with number of guests
✓ Premium brand aesthetic maintained
✓ Removed sections no longer appear
✓ Touch-friendly on mobile (48px+ hit areas)
