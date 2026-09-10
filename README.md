# Featured Courses Widget — ACD U

This repository hosts the **Featured Courses** widget that appears on the
OpsReady / ACD U pages. It shows five course cards, each with its own
artwork, and a **Start learning** button that opens the matching course
catalogue in Docebo.

This guide is written for a non-technical editor. You do **not** need to
know how to code to update it. If you can edit text carefully and click a
few buttons, you can maintain this widget.

---

## 1. How the whole thing fits together

There are three pieces:

1. **This GitHub repository** — stores the widget file (`index.html`).
2. **GitHub Pages** — a free GitHub feature that turns `index.html` into a
   live web address (a URL) that anyone's browser can open.
3. **Docebo** — the page where the widget actually appears. Docebo doesn't
   contain the widget; it simply *embeds* the live URL from GitHub Pages
   using something called an **iframe** (think of it as a window on the
   Docebo page that shows the GitHub-hosted widget inside it).

So the flow is:

    You edit index.html here  →  GitHub Pages publishes it  →  Docebo shows it

Because Docebo only points at the live URL, **you edit in one place (here),
and every page that embeds the widget updates automatically** the next time
someone loads it. You never edit anything inside Docebo to change the
courses.

---

## 2. The live web address

Once GitHub Pages is switched on (Settings → Pages), the widget is published at:

    https://destackai.github.io/opsready-widget/

That URL is what Docebo embeds. You can also open it directly in a browser
to preview the widget exactly as visitors see it.

> This is the live address once GitHub Pages is switched on
> (Settings → Pages → Deploy from branch → main / root).

---

## 3. What's in this repository

| File        | What it is                                         |
|-------------|----------------------------------------------------|
| `index.html`| The widget itself. **This is the only file you edit.** |
| `README.md` | This guide.                                        |

Everything the widget needs — its styling, its artwork, and the list of
courses — lives inside `index.html`. There are no other files to manage.

---

## 4. Editing the courses

All the editable content sits in one clearly marked section near the top of
`index.html` called **CONFIG**. You'll find it just after the line:

    const CONFIG = {

Each course is a block that looks like this:

    {
      id: 101,
      slug: "regclear-accidental-release-reporting-rule",
      link: "https://acdlearning.docebosaas.com/learn/catalog/view/8",
      art: "regclear",
      tag: "RegClear",
      title: "RegClear — Accidental Release Reporting Rule",
      lang: "EN", duration: "06m 00s", type: "E-learning",
      credit: "Micro-course",
      rating: null,
      thumb: ""
    },

Here's what each line controls:

| Field      | What it does                                                                 |
|------------|------------------------------------------------------------------------------|
| `link`     | **Where the Start learning button goes.** Paste the Docebo catalogue or course URL here. This is the most important field. |
| `art`      | Which artwork the card shows. Must be one of: `regclear`, `rd`, `hazmat`, `safety`, `regulatory`. |
| `tag`      | The small grey label at the top of the card (e.g. "Hazmat").                 |
| `title`    | The course name shown on the card.                                           |
| `lang`     | Language label, e.g. `"EN"` or `"ES"`.                                       |
| `duration` | Length shown next to the clock, e.g. `"30m 00s"`. Leave as `""` to hide it.  |
| `type`     | Usually `"E-learning"`.                                                      |
| `credit`   | The small yellow ribbon on the artwork, e.g. `"EPCRA"`. Leave as `""` to hide it. |
| `rating`   | A star rating, e.g. `"5.0"`. Set to `null` (no quotes) to hide the star.     |
| `id`, `slug`, `thumb` | Leave these as they are unless instructed otherwise.             |

### The golden rules for editing

Because this is a code file, a couple of small things must stay intact or the
widget won't load:

- **Keep the quotation marks.** Text values are wrapped in `"double quotes"`.
  Change the words *between* the quotes, never the quotes themselves.
- **Keep the commas.** Each line ends in a comma. Don't delete them.
- **`null` has no quotes.** For `rating`, either `"5.0"` (with quotes) or
  `null` (without). Never `"null"`.
- **Don't touch anything below the CONFIG section** — that's the widget's
  engine and artwork.

If in doubt, copy an existing course block, paste it, and change only the
words inside the quotes.

---

## 5. How to make an edit (step by step)

You can edit directly on the GitHub website — no software to install.

1. Open this repository on github.com.
2. Click **`index.html`** in the file list.
3. Click the **pencil icon** (top-right of the file view) to edit.
4. Scroll to the **CONFIG** section and make your change.
5. Scroll to the bottom and click **Commit changes**.
6. Wait about one minute, then refresh the Docebo page (or the live URL) to
   see the update.

That's it. GitHub Pages republishes automatically every time you commit.

> **Tip:** If you're making a big change, it's worth pasting the CONFIG
> section into <https://jsonlint.com> first to check the punctuation is
> valid before committing. (Choose "validate" — it will flag a missing
> comma or quote.)

---

## 6. Embedding it in Docebo

This only needs doing once per page. In a Docebo **Custom Content (HTML)**
block, switch to the code view (the `< >` button) and paste:

    <iframe id="opsready-featured"
        src="https://destackai.github.io/opsready-widget/"
        title="Featured Courses" loading="lazy" scrolling="no"
        style="width:100%;border:0;display:block;height:560px"></iframe>
    <script>
      window.addEventListener('message', function (e) {
        if (e.data && e.data.type === 'opsready:height' && e.data.height) {
          document.getElementById('opsready-featured').style.height = e.data.height + 'px';
        }
      });
    </script>

The small script lets the widget resize itself so there's no inner
scrollbar on any screen size. If your Docebo setup removes the `<script>`
part, the widget still works — it just stays at a fixed 560px height.

---

## 7. Frequently asked questions

**Do I have to change anything in Docebo when I update a course?**
No. Edit `index.html` here, commit, and every Docebo page that embeds the
widget updates on its own.

**Will editing the ID automatically update the title, duration, etc.?**
No. Every field is typed in by hand. If you change which course a card
points to, update its `title`, `duration`, `tag` and so on to match.

**I clicked the card image and nothing happened — is that broken?**
No, that's intended. Only the **Start learning** button is clickable.

**I made an edit and the widget disappeared.**
Almost always a missing comma or quotation mark. On GitHub, open
`index.html`, click the **History** link, and you can view or restore the
previous working version. Then re-do your edit more carefully.

**Is this page public?**
Yes — GitHub Pages URLs are publicly viewable. The widget only contains
course titles and links that are already published on your live pages, so
there's nothing sensitive in it.

---

## 8. Who built this

Built by DESTACK/Joe Sayers for CSG Creative / Alliance for Chemical Distribution.
For structural changes (new artwork themes, layout changes, more than five
cards), contact the developer rather than editing the engine directly.
