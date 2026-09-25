# Accessibility audit: Bookings (full WCAG review)

**Product:** Vello prototype (`vello-netlify/index.html`), checked against the Vello Design System docs
**Date:** Thursday, Sep 24, 2026
**Standard:** WCAG 2.1 AA, plus the Vello Design System's own accessibility rules
**Method:** Source code review of the unpacked prototype. Contrast ratios computed from the design tokens with the WCAG luminance formula. No live browser or screen reader pass yet (see Limitations).

## Scope

| # | Screen | How to reach it |
|---|---|---|
| 1 | Your bookings, Upcoming | Bottom nav, "Bookings" |
| 2 | Your bookings, Past | "Past" tab on screen 1 |
| 3 | Your booking (confirmed) | "Manage" on an upcoming booking card |

Screen 3 includes the "Cancel booking" confirmation sheet and the toast shown after cancelling, since both open from that screen.

## Summary

**Issues found:** 15 | **Critical:** 1 | **Major:** 7 | **Minor:** 7

Also listed: 5 design system rules the screens break, 4 problems outside accessibility, and 4 errors in the design system docs.

| Screen | Biggest problem |
|---|---|
| 1. Upcoming | "Waiting on reply" badge at 2.84:1 |
| 2. Past | Cancelled card faded to 62% opacity. Ratings shown only as stars, which screen readers can't read |
| 3. Your booking | Cancel sheet doesn't move keyboard focus. The "Booking cancelled" toast isn't announced |
| All | Focus ring nearly invisible (1.5:1). Browser zoom has no effect in the prototype |

## Findings

### Perceivable

| # | Issue | WCAG | Severity | Recommendation |
|---|---|---|---|---|
| 1 | **Browser zoom does nothing (all screens).** The prototype scales the fixed-size phone frame to fit the window. At 200% zoom the scale halves, so text stays the same physical size. On a laptop the frame also starts below 100%, so 11px text renders at about 10px. Pinch zoom on a real phone still works. | 1.4.4 Resize text | 🔴 Critical | For the web prototype, stop auto-scaling above 100% zoom, or let the frame scroll. A native build needs Dynamic Type support instead. |
| 2 | **"Waiting on reply" badge (S1).** Amber-700 on amber-100 is 2.84:1 at 11px. | 1.4.3 Contrast | 🟡 Major | Darken the badge text to `#8A5A0B` (5.18:1), or use ink-900 on the amber tint (15:1). |
| 3 | **Cancelled card (S2) set to `opacity: .62`.** The service line drops to 2.49:1, the "Cancelled" badge to 2.26:1, and the "Book again" button to 2.45:1. "Book again" still works, so the exception for disabled controls doesn't apply. It also looks disabled when it isn't. | 1.4.3 Contrast | 🟡 Major | Remove the opacity. Show the cancelled state with the badge plus a sunken background. The design system also says "do not tint body text with alpha." |
| 4 | **Past ratings shown only as stars (S2).** The "You rated" row uses `starsOnly`. Filled amber stars are 1.80:1 on white, and filled vs. empty stars are 1.22:1. The `aria-label` sits on a plain `<span>`, which screen readers don't reliably read, so VoiceOver likely says just "You rated." | 1.4.11 Non-text contrast, 1.1.1 Non-text content | 🟡 Major | Show the number ("You rated 5.0"). Add `role="img"` to the stars span in the `Rating` component, which also fixes "4.9" being read with no context on S3. |
| 5 | **No headings on any of the three screens.** "Your bookings", "Your booking", the banner title and the provider names in cards are all `<span>` or `<div>`. Screen reader users can't jump between bookings. | 1.3.1 Info and relationships | 🟡 Major | Make the app bar title an `<h1>` and each card's provider name an `<h2>`. The confirmed banner title can be an `<h2>` too. |
| 6 | **Tab count pills and "Completed" / "Cancelled" badges.** Ink-500 on ink-100 is 4.32:1 at 11px. | 1.4.3 Contrast | 🟢 Minor | Use ink-600 `#54564C` for the text (6.40:1). |
| 7 | **Inactive "Upcoming" / "Past" tab label.** 4.51:1 on cream, but about 4.36:1 where the green glow at the top of the phone reaches it. | 1.4.3 Contrast | 🟢 Minor | Check in a browser. Moving to ink-600 removes the doubt. |
| 8 | **Duplicate and unlabeled images.** Avatar photos get `alt` equal to the name right next to the visible name, so the name is read twice. Lucide icons have no `aria-hidden`, so some screen readers announce them as unlabeled images. | 1.1.1 Non-text content | 🟢 Minor | Set `alt=""` on avatars that sit beside a visible name, as the design system asks. Add `aria-hidden="true"` to decorative icons. |

### Operable

| # | Issue | WCAG | Severity | Recommendation |
|---|---|---|---|---|
| 9 | **Focus ring is nearly invisible.** `--focus-ring` is olive at 32% opacity: 1.49:1 on cream, 1.53:1 on white. It applies to every DS `Button` and `IconButton`: Manage, Message, Book again, Leave a rating, Message Maya and Back. | 2.4.7 Focus visible, 1.4.11 Non-text contrast | 🟡 Major | Use a solid 2px green-700 outline with a 2px offset (5.90:1 on cream, 6.60:1 on white). One token change fixes the whole app. |
| 10 | **"Cancel booking" sheet (S3).** It has the right `role="dialog"` and `aria-modal`, but focus stays on the button behind the dim overlay. Tab then runs through the covered page before it reaches the sheet. Escape doesn't close it, and after closing, focus is lost to the page body. | 2.4.3 Focus order, 2.1.1 Keyboard | 🟡 Major | On open, move focus to "Keep booking". Trap Tab inside the sheet, close it on Escape, and return focus to the button that opened it. |
| 11 | **Small buttons are 36px tall** (Manage, Message, Leave a rating, Book again). This passes WCAG 2.2 AA (24px minimum), but it breaks Vello's own rule: "tap targets never below 44px; `sm` is for dense desktop toolbars." The 44px criterion (2.5.5) is AAA in WCAG 2.1, not AA. | 2.5.5 Target size (AAA), DS rule | 🟢 Minor | Use `size="md"` (46px) on mobile cards. |

### Understandable

| # | Issue | WCAG | Severity | Recommendation |
|---|---|---|---|---|
| 12 | **Repeated button labels.** With two cards, a screen reader's button list reads "Manage, Message, Manage, Message", with no way to tell whose booking each one belongs to. | 2.4.6 Headings and labels | 🟢 Minor | Use `aria-label="Manage booking with Maya Rivera"` and similar, or `aria-describedby` pointing to the card's heading. |

### Robust

| # | Issue | WCAG | Severity | Recommendation |
|---|---|---|---|---|
| 13 | **Toasts aren't announced.** "Thanks, we'll pass it to Marcus" (S2) and "Booking cancelled" (S3) have no live region and disappear after 2.4 seconds. On S2 the toast is the only feedback. | 4.1.3 Status messages | 🟡 Major | Give the toast container `role="status"`. Keep it mounted and swap its text in and out, rather than creating it each time. |
| 14 | **Tabs are incomplete.** `tablist`, `tab` and `aria-selected` are correct, but there's no `tabpanel` or `aria-controls`, and no arrow-key support (which the DS docs promise). The count likely runs into the label ("Upcoming2"). | 4.1.2 Name, role, value | 🟢 Minor | Add a `tabpanel`, arrow keys and roving `tabIndex`. Give each tab an `aria-label` that includes the count ("Upcoming, 2"). |
| 15 | **Bottom nav "Messages" badge.** The badge comes before the label in the markup, so the name is "2 Messages" (or "2Messages"), with no "unread." | 4.1.2 Name, role, value | 🟢 Minor | Use `aria-label="Messages, 2 unread"`, as the DS docs specify. |

## Color contrast check

Screen background is `#F6F2E7` (paper). Cards are `#FFFFFF`.

| Element | Foreground | Background | Ratio | Required | Pass? |
|---|---|---|---|---|---|
| Badge "Waiting on reply" (11px) | `#C77F12` | `#FCEFCF` | 2.84:1 | 4.5:1 | ❌ |
| Cancelled card, service line | ink-500 at 62% | faded white | 2.49:1 | 4.5:1 | ❌ |
| Cancelled card, "Cancelled" badge | ink-500 at 62% | faded ink-100 | 2.26:1 | 4.5:1 | ❌ |
| Cancelled card, "Book again" | white at 62% | faded olive | 2.45:1 | 4.5:1 | ❌ |
| Filled star (graphic) | `#F4B740` | `#FFFFFF` | 1.80:1 | 3:1 | ❌ |
| Filled vs. empty star | `#F4B740` | `#D6D6C6` | 1.22:1 | 3:1 | ❌ |
| Focus ring | olive at 32% | cream / white | 1.49 / 1.53:1 | 3:1 | ❌ |
| Tab count, neutral badges (11px) | `#6E7064` | `#EFEEE1` | 4.32:1 | 4.5:1 | ❌ |
| Inactive tab over the top glow | `#6E7064` | `#EBF1DB` | 4.36:1 | 4.5:1 | ❌ borderline |
| Inactive tab on cream | `#6E7064` | `#F6F2E7` | 4.51:1 | 4.5:1 | ✅ barely |
| "Cancel booking" link | `#6E7064` | `#F6F2E7` | 4.51:1 | 4.5:1 | ✅ barely |
| Screen title | `#1B1C18` | `#F6F2E7` | 15.31:1 | 4.5:1 | ✅ |
| Neighbor name, price | `#1B1C18` | `#FFFFFF` | 17.13:1 | 4.5:1 | ✅ |
| Service line, row labels (13px) | `#6E7064` | `#FFFFFF` | 5.04:1 | 4.5:1 | ✅ |
| Badge "Confirmed" | `#466621` | `#EBF1DB` | 5.70:1 | 4.5:1 | ✅ |
| Date and distance chips | `#466621` | `#F5F8EC` | 6.13:1 | 4.5:1 | ✅ |
| Active tab label | `#466621` | `#F6F2E7` | 5.90:1 | 4.5:1 | ✅ |
| Active tab underline (non-text) | `#557E26` | `#F6F2E7` | 4.27:1 | 3:1 | ✅ |
| Primary buttons | `#FFFFFF` | `#557E26` | 4.77:1 | 4.5:1 | ✅ |
| Banner title / text (S3) | `#1B1C18` / `#3D3F37` | `#EBF1DB` | 14.80 / 9.23:1 | 4.5:1 | ✅ |
| Banner check icon (non-text) | `#F6F2E7` | `#557E26` | 4.27:1 | 3:1 | ✅ |
| Nav labels (inactive / active) | `#6E7064` / `#466621` | `#FFFFFF` | 5.04 / 6.60:1 | 4.5:1 | ✅ |
| Nav unread badge, as rendered | `#FFFFFF` | `#557E26` | 4.77:1 | 4.5:1 | ✅ |
| Nav unread badge, DS persimmon | `#FFFFFF` | `#F0623B` | 3.22:1 | 4.5:1 | ❌ |

The nav badge note: the prototype's Tweaks panel overrides `--accent` to olive by default, so the badge renders at 4.77:1. With the design system's real persimmon accent it would fail at 3.22:1.

## Keyboard navigation

| Element | Tab order | Enter / Space | Escape | Arrow keys |
|---|---|---|---|---|
| Tabs Upcoming / Past | 1 and 2 (both are Tab stops) | Switches tab ✅ | n/a | Nothing ❌ |
| Manage / Message (per card) | In card order | Works ✅ (focus ring hard to see) | n/a | n/a |
| Leave a rating / Book again | In card order | Works ✅ | n/a | n/a |
| Create (+) button | After the cards | Opens a sheet with the same focus problems as #10 | Doesn't close ❌ | n/a |
| Bottom nav | Last | Works ✅, `aria-current` set | n/a | n/a |
| S3 Back arrow | 1 | Goes to Home, not Bookings | n/a | n/a |
| S3 Message Maya / Cancel booking | After the summary | Works ✅ | n/a | n/a |
| S3 Cancel sheet | Focus not moved ❌ | Buttons work once reached | Doesn't close ❌ | n/a |

## Screen reader

Predicted from the markup. Confirm with VoiceOver.

| Element | Announced as | Issue |
|---|---|---|
| Screen title | "Your bookings" (plain text) | Not a heading |
| Provider photo | "Maya Rivera, image", then "Maya Rivera" | Name read twice |
| Shield mark | "Background-checked, image" | Good. Sighted users get no text label |
| Past rating | "You rated" | Score missing |
| Manage button | "Manage, button" | No context |
| Toasts | Nothing | Not announced |
| Cancel sheet | "Cancel Maya's visit?, dialog", if VoiceOver follows `aria-modal` | Focus stays behind it |

## Priority fixes

| Priority | Fix | Who it helps |
|---|---|---|
| 1 | Replace the focus ring token with a solid green-700 outline (#9) | Every keyboard user, on every screen, from one change |
| 2 | Add focus handling and Escape to the cancel sheet (#10), and make toasts a live region (#13) | Keyboard and screen reader users, who now get no clear path or confirmation when cancelling |
| 3 | Remove the cancelled-card opacity and darken the amber badge text (#2, #3) | Low-vision users, who can't read booking status |
| 4 | Show ratings as a number and add headings (#4, #5) | Screen reader users, who can't follow the Past tab |
| 5 | Fix zoom in the web prototype (#1) | Anyone who needs larger text in the demo |

## Design system rules the screens break (not WCAG)

| Rule | Where |
|---|---|
| Body text never below 14px | Service line, row labels and banner text are 13px. "You rated" is 12.5px |
| Tap targets never below 44px | All `sm` card buttons (#11) |
| Honour `prefers-reduced-motion` | No reduced-motion handling anywhere in the app |
| No spring easing on destructive or financial actions | The cancel sheet slides in with `--ease-spring` |
| Label the trust mark on its first appearance on a screen | Cards show only the bare shield |

## Other problems found (not accessibility)

| Problem | Impact |
|---|---|
| A pending booking opens as "Confirmed". Devon's card says "Waiting on reply", but "Manage" opens the confirmed state with the "You're all set" banner and a Confirmed badge | Tells the user something false about a booking |
| The cancel sheet says "She's expecting you" and the address error says "send her to", whoever the provider is. Devon gets "she" | Hard-coded pronouns misgender providers. Use the provider's name instead |
| "Manage" shows the "You're all set" banner meant for a booking just made | Confusing when you're only reviewing an existing booking |
| The back arrow on "Your booking" goes to Home instead of Bookings | Breaks the user's path back |

## Errors in the design system docs

Worth raising with the design system team:

| Doc page | What it says | What the numbers show |
|---|---|---|
| Rating | "Amber on cream meets 3:1 as a graphical object" | 1.61:1 on cream, 1.80:1 on white |
| Button, Accent usage | White on persimmon (3.3:1) "passes at the 16px semibold weight buttons use" | 3.22:1. WCAG large text is 18.66px bold or 24px regular, so 16px semibold needs 4.5:1 |
| Badge | "Every variant meets 4.5:1 for its text on its tint" | Warning is 2.84:1, neutral is 4.32:1 |
| IconButton | "Tap target is 44×44 at every size" | The `sm` size renders at 34px |

The prototype also bundles an older version of the design system (13 components against the documented 17). It is missing `VerifiedBadge`, `ScrollRow`, `EmptyState` and the `accent-outline` button, so the app builds its own versions of those.

## Compared with the earlier audit

`accessibility-audit_bookings.md` in this folder checked contrast, touch targets and color-alone, and left the cancel flow out of scope. The numbers match where the two overlap. Differences:

| Topic | Earlier audit | This review |
|---|---|---|
| Scope | Contrast, touch targets, color-alone | All of WCAG 2.1 AA, plus the design system's rules. Includes the cancel sheet |
| Nav unread badge | Fail at 3.22:1 (persimmon) | Renders at 4.77:1 because the Tweaks default overrides the accent to olive. It fails once the real accent is restored |
| "Cancel booking" link target | Flagged at about 22pt | Not measured here. The earlier finding stands |
| Active bottom nav item | Borderline color-alone | Not covered here. The earlier finding stands |
| Manage screen | Passes | Passes on contrast, but has focus, heading, dialog and toast issues |

## Limitations

- Findings come from the source code, not a live device. Contrast in the glow area, zoom behavior and all screen reader output are predictions, and a short pass in Chrome plus VoiceOver would confirm them.
- Ratios use the design token hex values. Ratios for faded elements were computed by blending the 62% opacity over the paper background.
- Booking data, unread counts and badges are sample data, so other states may show different results.
