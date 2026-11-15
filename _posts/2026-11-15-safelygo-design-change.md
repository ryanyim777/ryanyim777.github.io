---
title: "SafelyGo: too cute for a safety app, so I changed the design"
date: 2026-11-15 17:00:00 -0600
project: safelygo
topic: Design
---

**What happened:**
My first plan for SafelyGo was a cute cartoon style: pastel colors, emoji, and a dog and cat mascot on the screens.
After I built the Report screen, I looked at it on my phone and something felt off.
It was too cute. A student who just saw someone get hurt doesn't want a playful screen.
They want something that looks calm and trustworthy, like it really goes to campus safety.

So I changed the direction to "friendly but serious."

<!-- ![Report screen before and after the redesign](/assets/images/safelygo/report-before-after.png) -->

**What changed:**

| | Before | After |
|---|---|---|
| Background | Cream pastel | Light gray with white cards |
| Top of the screen | Big title and a cat | A navy header band |
| Report types | Full pastel tiles | White cards with a small colored icon |
| Icons | Emoji | Clean line icons |
| Mascots | On the report screen | Only in friendly moments |
| Red | SOS only | Still SOS only |

I kept the three report colors (orange, purple, yellow), but now they are small icon chips instead of whole tiles.
Each type still has an icon, words, and a color together, so nobody has to rely on color alone.

The mascots didn't go away. They just moved to moments where being friendly fits:
the sign-in screen, the Guardians intro, and the "Thanks for speaking up" screen after you send a report.

**Why it only took a short time:**
Early on, I put all the colors in one file (`theme.ts`) instead of typing them into each screen.
I did the same with icons (`icons.ts`) and made one shared header component.
So changing the whole app mostly meant changing those few files:

```ts
export const Colors = {
  light: {
    background: '#F4F6F8',      // light gray page
    backgroundElement: '#FFFFFF', // white cards
    header: '#0C447C',          // navy band at the top
    primary: '#0C447C',         // normal buttons
  },
};
```

This idea is called design tokens: name each color once and use the name everywhere.
If I had written colors directly in every screen, I would have had to fix each one by hand.

**What I learned:**
- Test the design on a real phone, not just in my head. The problem was obvious once I saw it.
- The look should match the moment. Serious screens for serious actions, friendly touches for the rest.
- Keeping colors and icons in one place makes big changes small.

**Next step:**
During the polish week before judging, I want to replace the emoji mascots with my own drawings
and write a one-page design guide for the app.
