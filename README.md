# Haoneng Lin — Personal Website

Personal academic homepage of **Haoneng Lin (林昊能)**, PhD Student at the School of Nursing, The Hong Kong Polytechnic University. Built as a static site for GitHub Pages.

- Live: https://haonenglin.github.io/ *(update after deployment)*
- Contact: lhn987745283@gmail.com / haoneng.lin@connect.polyu.hk

## Pages

| Path | Description |
| --- | --- |
| `index.html` | About me, news, selected publications, professional activities |
| `publications.html` | Full publication list (auto-rendered from `data/publications.bib`) |

## Project Structure

```
.
├── index.html              # Home page
├── publications.html       # Publications list page
├── css/
│   ├── main.css            # Site-wide styles
│   └── publications.css    # Publications layout
├── js/
│   ├── navigation.js       # Top navigation bar
│   ├── footer.js           # Site footer
│   ├── bibtex-parser.js    # BibTeX -> JS object parser
│   ├── publications.js     # Renders publication cards
│   ├── news.js             # Loads news from JSON
│   └── animations.js       # Scroll animations
├── data/
│   ├── publications.bib            # All publications in BibTeX
│   ├── publication-config.json     # Cover image / pdf / select flag per paper
│   ├── coauthor.json               # Coauthor display names / homepages
│   └── news.json                   # News feed
├── images/
│   ├── site/me.jpg                 # Profile photo
│   └── publications/*.png          # Paper thumbnails
└── README.md
```

## Editing Workflow

### Add or update a publication
1. Append the BibTeX entry to `data/publications.bib`.
2. Add a matching record in `data/publication-config.json` keyed by the citation key, e.g.
   ```json
   "lin2026newpaper": {
     "select": true,
     "image": "images/publications/lin2026newpaper.png",
     "pdf": "https://arxiv.org/abs/XXXX.XXXXX",
     "github": "https://github.com/haonenglin/repo"
   }
   ```
3. Drop the cover image into `images/publications/` using the same filename.

### Bold your name in the author list
`js/publications.js` has a single source of truth:

```js
const SITE_OWNER_NAME = 'Haoneng Lin';
```

Make sure every BibTeX `author` field writes the name exactly as `Haoneng Lin` (Firstname Lastname, no comma) for the bolding to take effect.

### Update news
Edit `data/news.json`. Each entry supports `date` and `content_html` (HTML allowed). Add `"pin": true` to keep an entry at the top.

### Mark co-first / corresponding authors
In `data/publication-config.json`, add arrays to a paper entry:

```json
"co_first_authors": ["Haoneng Lin", "Another Author"],
"corresponding_authors": ["Jing Qin"]
```

A `*` (co-first) or `✉` (corresponding) marker will be appended automatically.

## Local Preview

The site is plain static HTML; any static server works:

```bash
# Python 3
python -m http.server 8000

# Node.js
npx serve .
```

Then open http://localhost:8000.

## Deployment

Push to a GitHub repository named `<username>.github.io` and the site will be served at `https://<username>.github.io/`. No build step is required.

## Credits

Template forked and adapted; original site UI inspired by classic academic homepages.
