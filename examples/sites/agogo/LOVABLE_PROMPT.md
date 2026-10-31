# Prompt Lovable: refonte de la page d'accueil Agogo Store

Mode d'emploi :
1. Ouvrez le projet Agogo Store dans Lovable.
2. Joignez `index.html` et `theme.css` (ce dossier) comme fichiers de référence.
3. Envoyez d'abord le prompt en mode Plan (« Chat mode »), relisez le plan, puis lancez.
4. Le prompt est en anglais : c'est la langue où l'agent Lovable suit le plus fidèlement des consignes détaillées.

---

## Prompt à copier

```
Redesign the Home page only. The attached index.html and theme.css are the
approved design reference: match their layout, spacing, colours and behaviour,
but build it with this project's existing stack (React, TypeScript, Tailwind,
shadcn/ui) and existing data. Do not copy the static HTML in.

HARD CONSTRAINTS
- Keep every existing route, the cart, the wishlist, auth, the product data
  source and the checkout flow exactly as they work today. Change presentation only.
- Products, prices, ratings and categories come from the existing database
  queries, never hardcoded. The reference uses real catalog items as placeholders.
- No emoji anywhere. Icons come from lucide-react.
- No native <select>. Use the existing shadcn components.
- Every colour, radius, spacing and duration goes through the theme tokens below.
  No hex values or arbitrary Tailwind values in components.
- Mobile first: base styles are the phone layout, wider screens add min-width
  breakpoints. Nothing may scroll horizontally between 280px and 1440px.
- Light and dark mode both work, from the same tokens.

1. THEME TOKENS (index.css CSS variables + tailwind.config, converted to the
   format the project already uses)
Light:
  page #FBF6EE, card #FFFDF9, tile #F4EADB, chip #EFE3D1
  text primary (navy) #182B5C, text secondary #4E5468, text accent #9B3208
  action primary #B83C0B, hover #9B3208, active #822905, text on action #FFFFFF
  band (navy sections and footer) #182B5C, band text #FBF6EE, band text secondary #C9CEDC,
  band border #34477A
  hover background #F2E7D6, selected background #182B5C with text #FBF6EE
  border default #E6D9C5, border strong #7D7466, error #B42318, success #2F6B3A,
  rating star #B8650B
  brand fruit #F26B21 and leaf #E8A317: logo only, never behind text
  product tiles (same in both themes, text on them always #182B5C):
  blush #F2D9D2, sage #DDE6D6, butter #F3E7C6, lilac #E4DCEE, sky #D8E3EF, peach #F6DCC8
Dark:
  page #131726, card #1C2135, tile #232943, band #0D1120
  text primary #F5EFE6, text secondary #B7BCCB, text accent #FFB088
  action primary #FF8A4C, hover #FFA574, active #FFBF9C, text on action #1A1206
  hover background #262C48, selected background #F5EFE6 with text #131726
  border default #2F3656, border strong #8D93A8, rating star #FFB547
Why: the current orange button (about #F26B21) with white text is about 3:1 and
fails WCAG AA. #B83C0B with white is 5.69:1.
Type: display serif "Iowan Old Style", Palatino, Georgia, serif for headings;
Inter / system-ui for UI. Hero title 44px phone, 60px tablet, 72px desktop,
line-height 1.04. Section titles 30px phone, 48px desktop. Body 16px.
Radii: 6px small, 12px inputs, 20px cards, 28px large panels, full for pills.
Spacing on a 4px scale. Page gutter 16px phone, 32px tablet, 40px desktop.
Max content width 1280px.

2. HEADER (sticky, page background, hairline bottom border)
- Row 1: logo left; on desktop the search bar sits in the centre (max 640px,
  pill, search icon left, submit arrow button right, placeholder
  "Search serums, collagen, perfume"); right: theme toggle (moon/sun, aria-pressed),
  account, wishlist with count badge, bag with count badge. All icon buttons 44x44
  with an aria-label that includes the count ("Bag, 2 items").
- On phone the search bar drops to its own full-width row under the logo.
- Remove the notifications bell from the home header.
- Row 2: category nav with ALL categories from the database (Skincare, Makeup,
  Haircare, Fragrance | Supplements, Wellness | New, Bestsellers), pill links,
  current page = navy filled pill with aria-current="page". On phone it scrolls
  horizontally with a fade on the right edge as the scroll cue.
- Remove the separate orange "Shop all" pill.

3. HERO (two columns from 960px, stacked below)
- Left: eyebrow "Beauty and wellness, curated" (small caps, accent colour,
  sparkles icon); H1 "Beauty that moves with you" with "with you" in italic
  accent colour; lede "Clean skincare, joyful makeup and daily wellness rituals,
  chosen by Agogo Store so you can skip the guesswork."
- ONE primary button "Shop bestsellers" with arrow, 52px tall, then a text link
  "Find your daily ritual" that scrolls to the rituals section. No second button.
- Proof row under a hairline: five stars + "4.9 out of 5 from 12,400+ reviews",
  shield icon "Clean-tested formulas", leaf icon "Cruelty-free".
- Right: featured product card on the blush tile, large radius: product imagery
  (use the product photo from the database for the featured product; the
  reference uses SVG placeholders), tag "Glow from within", and a white inner
  card with product name (serif), one-line description, rating, brand, price and
  a "See the ritual" link to the product page. Feature the Beauty Glow product
  (make the featured product configurable).
- Remove the empty space above the headline: the title starts near the top.
- Remove the floating "Ask Agogo AI", WhatsApp and purple chat bubbles from the
  home page. They move into section 7.

4. SHOP BY WHAT YOU NEED (category bento)
- Title "Shop by what you need", sub "Six shelves, one standard: every formula is
  clean-tested and cruelty-free."
- Desktop 4 columns: Wellness is the lead tile spanning 2 columns and 3 rows
  (sage tile, serif 48px title, description, product image, arrow button).
  The other 5 categories are smaller tiles, each on its own pastel, with name,
  short description and a round arrow; the last tile is "Shop everything" on
  the navy band colour linking to the full shop. Phone: 1 column below 384px,
  2 columns above, lead tile full width. Tiles in a row share the same height.
- Hover: lift 2px with a soft shadow; respect prefers-reduced-motion.

5. BESTSELLERS THIS MONTH
- Title + "Ranked by what customers reorder most." + "View all bestsellers" link.
- Filter chips (toggle buttons with aria-pressed, selected = navy fill) built
  from the categories present in the list, each with a count; a polite live
  region says "Showing N products". Filtering is client-side.
- Grid: 2 columns phone, 3 at 768px, 4 at 1152px; show 8 products.
- Card: 4:5 pastel image tile with the product image, optional badge top-left
  ("Top rated" when rating >= 4.9, "Bundle of 3" for bundles), wishlist heart
  button top-right (44x44, aria-pressed, filled when saved, wired to the
  existing wishlist). Below: brand in small caps, product name linking to the
  product page, short description (hidden on phone), price, star rating, and an
  outline "Add" button wired to the existing cart: on success it shows a check
  and "Added" for about 2 seconds, updates the bag badge and announces
  "<name> added to your bag" in a live region. Show a loading spinner with
  aria-busy while the add is in flight; never dim it like a disabled button.

6. RITUALS BAND (full-width navy section, id="rituals")
- Left (sticky on desktop): eyebrow "Rituals, not routines", serif title
  "One day, three bundles", text "Each bundle is built for a moment of the day,
  so you know what to take and when."
- Right: an ordered timeline (not three equal cards), rows separated by
  hairlines: Morning (sunrise icon) Daily Health Bundle, Afternoon (zap icon)
  Energy Bundle, Evening (moon icon) Sleep Bundle. Each row: time label, name,
  one-line description, price, rating, "See what is inside" link.

7. NOT SURE WHERE TO START? (help)
- Lead panel (2/3 width on desktop, tile background): "Ask Agogo AI" with a
  labelled input "What would you like help with?" and a primary "Get suggestions"
  button, wired to the existing AI assistant. Empty submit shows an inline error
  with an icon: "Type a question first, or pick one of the examples below."
  Three example chips fill the input when clicked: "Which collagen is right for
  me?", "Help me sleep better", "A gift under $60".
- Quiet panel (1/3, hairline border): "Prefer a person?" "Our team answers
  product and order questions on WhatsApp." with links "Chat on WhatsApp"
  (existing WhatsApp link) and "Track an order".

8. FOOTER (navy band)
- Logo + "Clean skincare, joyful makeup and wellness rituals, thoughtfully
  curated."; columns Shop / Help / Agogo with the existing links; bottom line
  with the store name and "Supplements are not intended to diagnose, treat or
  cure any condition."

ACCESSIBILITY AND STATES (required)
- Skip link to main content. One H1. Headings never skip a level.
- Every interactive element has default, hover, visible focus ring (2px page-colour
  gap + 2px ring in text colour; on the navy band the ring is the band text colour),
  active and disabled states. Inputs have an error state.
- Text contrast at least 4.5:1, UI borders and icons at least 3:1, in both themes
  and in hover and focus states.
- Touch targets at least 44x44 for buttons, at least 24x24 for anything else.
- Decorative images and icons are aria-hidden; product images have alt text.
- prefers-reduced-motion turns off the lifts and transitions.
- No colour-only meaning, no coloured border on just one side of a card.

When done, list what you changed per file and anything you could not wire up.
```
