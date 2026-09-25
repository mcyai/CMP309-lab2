# Assignment 2 – HTML & CSS Boxes

A single HTML page that shows two different layouts depending on which
stylesheet it links to. Only HTML and CSS are used (no JavaScript, no external
libraries).

## File Organization

```
assets/
├── index.html   # The page: six boxes (A–F) inside a .boxes container
├── styleA.css   # Version A: boxes stacked vertically and centered
├── styleB.css   # Version B: boxes in a row, last box in the bottom right corner
└── README.md
```

`index.html` links to `styleA.css` by default. To see Version B, comment out the
`styleA.css` link in the `<head>` and uncomment the `styleB.css` link.

### Version A (`styleA.css`)
- The `.boxes` container is a column **Flexbox** with `justify-content: space-evenly`,
  so the vertical spacing between boxes changes when the window is resized.
- `min-height: 100vh` lets the container grow when the window is too short, and
  `flex-shrink: 0` keeps each box at 100×100 px, so boxes never overlap or shrink.
- `:nth-child(even)` gives the alternating colors, and `:last-child` styles box F
  (4px black border, text centered vertically with Flexbox).

### Version B (`styleB.css`)
- The `.boxes` container is a row Flexbox with `flex-wrap: nowrap` and a 10px `gap`;
  `flex-shrink: 0` stops the boxes from shrinking, so A–E always stay on one line.
- `box-sizing: border-box` keeps each box at exactly 100×150 px, including the
  10px dotted left border and the 10px padding around the letter.
- Box F uses `position: fixed; right: 10px; bottom: 10px;` so it stays in the
  bottom right corner when the window is resized.
- `:hover` changes the cursor to a hand and the colors to yellow / goldenrod.

## Challenges

- **Equal spacing without overlap (A):** With a fixed height the flex items
  shrank and overlapped in a short window. Using `min-height` instead of `height`
  and `flex-shrink: 0` on the boxes fixed this.
- **Styling the last box (A):** Box F is the 6th child, so the `:nth-child(even)`
  color rule also matched it. The `:last-child` rule has the same specificity, so
  it has to come after the even rule to win.
- **Keeping the boxes on one line (B):** Flex items shrink by default when the
  window is narrow, so the boxes had to be given `flex-shrink: 0`.
- **Box size with border and padding (B):** With the default `content-box`,
  the padding and dotted border made the boxes bigger than 100×150 px.
  `box-sizing: border-box` keeps the given size.
- **One HTML file for both styles:** Both layouts had to come from the same
  markup, so the HTML only has a container and six boxes, and all layout
  decisions live in the stylesheets.
