# Cover Charge Slider Design Spec
**Date:** 2026-06-01  
**Feature:** Add cover charge slider to review booking page  
**Scope:** Gift a Meal flow — review your booking page

---

## Overview

High-intent users gifting a dining experience need to decide the per-person table cover charge upfront. This ensures the guest has no out-of-pocket expenses and only confirms the final bill amount.

**User Story:** As a gifter, I want to set a per-person cover charge so the guest doesn't have to worry about any dining costs when they visit.

---

## Review Page Structure (Updated)

Final layout order:
1. Header (back button + "Review your booking")
2. Gift banner (prepaid gift value notification)
3. Booking details card (restaurant, date, guests, location, offer)
4. **About your gift section** (NEW — cover charge slider + info cards)
5. Seating + Special requests
6. Booking summary (gift value + cover charge + to be paid total)
7. Your details (name + phone)
8. Confirm booking button

---

## "About Your Gift" Section Design

### Visual Structure

**Main Card (with slider):**
- Background: `#1e1e20` (matches booking summary card)
- Border radius: `16px`
- Padding: `16px`
- Header: 🎁 icon + "About your gift" title (16px, 600 weight)
- Subtext: "Cover the table charge—they'll have nothing to worry about." (14px, regular weight, dim color)

**Slider UI:**
- Label: "Cover charge per guest"
- Range: ₹0 to ₹500
- Real-time display: "₹__ per guest (X guests) = ₹__ total"
- Slider styled with blue accent color (`#0B70D5` / oklch 60% 0.24 265)
- Updates "To be paid" total in booking summary in real-time

**Three Info Cards (stacked below slider, always visible):**

Each card:
- Background: `rgba(220, 220, 220, 0.05)` (slightly elevated from main bg)
- Border: `1px solid rgba(220, 220, 220, 0.12)` (subtle separation)
- Border-radius: `12px`
- Padding: `12px`
- Left border: `3px solid #0B70D5` (blue accent for "informational")
- Display: flex, gap: 12px

**Card 1: Easy refunds & modifications**
- Icon: 🔄
- Title: "Easy refunds & modifications"
- Copy: "You can modify or cancel anytime before the booking date."
- Font size: 12px (smaller, secondary information)
- Color: `#fafafa` for title, `#77777e` for copy

**Card 2: What if amounts differ?**
- Icon: ⚠️
- Title: "What if amounts differ?"
- Copy: "If the final bill exceeds your cover charge, your guest pays the difference. If it's less, you get refunded the extra."
- Font size: 12px
- Color: Same as Card 1

**Card 3: Share with your guest**
- Icon: 📱
- Title: "Share with your guest"
- Copy: "They'll receive the redemption code and booking details via SMS immediately after you confirm."
- CTA Button: "Share details" (inline, right-aligned)
- Button styling: Blue text on transparent, 14px, 600 weight

---

## Interactions

### Slider
- **Drag interaction:** User drags thumb left/right to set ₹0–₹500 per guest
- **Real-time updates:**
  - Display updates: "₹X per guest (Y guests)"
  - Total below slider updates: "Total cover charge: ₹Z"
  - Booking summary's "To be paid" recalculates: Gift Meal + Cover Charge total
- **Keyboard support:** Arrow keys adjust ±₹10 (accessibility)
- **Touch friendly:** Slider thumb is large enough for mobile (48px minimum hit area)

### Share Details Button (Card 3)
- **On click:** Opens bottom sheet modal
- **Modal shows:**
  - SMS preview: "Hi [guest name], I've booked you a meal at [restaurant]. Here's your redemption code: [code]. No payment needed—just confirm the final bill on arrival."
  - "Copy to clipboard" button
  - Social share options (WhatsApp, Email, etc.)
  - "Share after booking" toggle (user can defer sharing until after confirmation)

---

## Booking Summary Integration

Update the booking summary section to show:
```
Gift Meal value:     ₹1500
Cover charge:        ₹200 (₹100 × 2 guests)
─────────────────────────────
To be paid:          ₹1700
```

- Cover charge line appears only if slider value > ₹0
- All values update in real-time as slider moves
- Sub-text on cover charge line: "(₹X per guest × Y guests)"

---

## Removed Elements

- **"Gifting to..." section** — removed from review page (contextual enough via gift banner)
- **"Cancellation & Refund" section** — replaced entirely by "About your gift" (covers refund info + modifications)

---

## Copy & Tone

- **Warm, confident, reassuring** — avoids legal/formal language
- **Trust-building** — emphasizes user control (modify, cancel anytime)
- **Guest-centric** — frames cover charge as gift benefiting the guest
- **Clarity on edge cases** — explains variance scenarios without jargon

---

## Responsive Design

- **Mobile (375px width):** All elements stack vertically, full-width cards
- **Slider:** Takes full width of card, touch-friendly
- **Info cards:** Full-width, no side padding squeeze
- **Button:** Full-width in modal, centered text

---

## Technical Notes

- Slider implemented using native `<input type="range">` or a custom range slider component (maintains premium feel)
- Real-time updates use JavaScript listeners on slider input
- Modal uses existing phone shell's overlay system (consistent with existing UI patterns)
- State: Cover charge value stored in component state, syncs with booking summary total

---

## Success Criteria

✓ Cover charge slider is prominent and easy to adjust  
✓ Real-time total updates in booking summary  
✓ All info cards visible (no hidden/collapsed content)  
✓ Share flow is intuitive and quick  
✓ Scales correctly with number of guests  
✓ Maintains premium brand aesthetic throughout  
✓ Refund/modification messaging gives user confidence  
