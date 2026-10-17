<div align="center">

# The Shahram File

A personal portfolio built as an interactive detective evidence board, with draggable cards, red-string connections and a UV lamp.

![HTML5](https://img.shields.io/badge/HTML5-Single%20File-E34F26?style=flat-square&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-3D%20Transforms-1572B6?style=flat-square&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-Vanilla-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![Vercel](https://img.shields.io/badge/Hosted%20on-Vercel-000000?style=flat-square&logo=vercel&logoColor=white)

</div>

## Overview

The Shahram File is my personal portfolio, presented as a case file instead of a standard page. A scroll-driven 3D door opens onto a corkboard where experience, projects, education and skills are pinned as cards and tied together with red string. The whole site is one hand-written `index.html` using HTML, CSS and vanilla JavaScript, with no frameworks, no dependencies and no build step.

## Demo

Live site: **[the-shahram-file.vercel.app](https://the-shahram-file.vercel.app)**

Scroll to break the seal on the evidence room door, or use the Skip Intro button to go straight to the board.

## Key Features

- **Scroll-scrubbed 3D door intro:** scroll position drives the police tape tearing away, the two door panels swinging open with CSS `rotateY`, and the camera pushing through (`scrubDoor` in `index.html`).
- **Draggable evidence cards with live red strings:** cards move with Pointer Events and the connecting SVG curves are redrawn on every move, with a gentle sag and a highlight on the strings of the hovered card (desktop widths).
- **Case-file dossiers:** every card opens a modal with facts, links and a verdict stamp. Cards are keyboard reachable (Enter or Space to open, Escape to close) and focus returns to the card on close.
- **UV lamp mode:** a toggle button, or a hidden spinning switch on the board, flips the page to a dark UV theme and reveals notes written in invisible ink.
- **Flashlight and tilt:** a light spot follows the mouse pointer across the board and the frame tilts slightly with pointer position (disabled for reduced-motion users).
- **Tip line contact form:** name, email and message are posted to the Web3Forms API with a honeypot field, and a failed send falls back to a direct email message.
- **In-page document viewer:** the resume and a completion letter open in a full-screen iframe overlay instead of a new tab.
- **Case-closed outro and responsive layout:** a second scroll-scrubbed sequence (bars, stamp, typed verdict) ends the page. At 1080px wide and below the board becomes a vertical list, and `prefers-reduced-motion` turns the scrubbing off.

## Tech Stack

| Area | Technology |
|---|---|
| Markup | HTML5, a single `index.html` |
| Styling | CSS3: custom properties, 3D transforms and perspective, `clip-path`, gradients, media queries for `max-width: 1080px` and `prefers-reduced-motion` |
| Scripting | Vanilla JavaScript with Pointer Events, IntersectionObserver and ResizeObserver, no framework or library |
| Graphics | Inline SVG for the red strings, plus data-URI SVG noise textures |
| Fonts | Google Fonts: Special Elite and Caveat |
| Contact form | Web3Forms API (`https://api.web3forms.com/submit`) |
| Hosting | Vercel, static files |

## Project Structure

```text
portfolio-website/
|-- index.html                 # The whole site, no build step
|   |-- <style>                # Theme variables, 3D door, board, dossier modal, outro, responsive rules
|   |-- <body>                 # Intro door, case header, board container, outro, dialogs
|   `-- <script>               # Card data (items, links), rendering, strings, drag, form, scroll scrubbing
|-- img.png                    # Portrait used on the polaroid card
|-- resume.pdf                 # One-page resume, opened in the in-page viewer
|-- *-completion-letter.pdf    # Internship letter, opened in the in-page viewer
`-- .gitignore                 # Ignores the .vercel folder
```

## Getting Started

### Prerequisites

- A current desktop browser (the page uses CSS 3D transforms, Pointer Events, IntersectionObserver and ResizeObserver).
- Internet access for Google Fonts and the contact form.
- Optional: any static file server.

### Installation

```bash
git clone https://github.com/shahramshafiq/portfolio-website.git
cd portfolio-website
```

There is nothing to install: no package manager, no dependencies.

### Run

Open `index.html` in your browser, or serve the folder with any static file server, for example:

```bash
python -m http.server 8000
```

Then visit `http://localhost:8000`.

### Configuration

The code reads no environment variables. The contact form uses a Web3Forms access key stored in the hidden `access_key` input inside `index.html`. To receive messages in your own inbox, replace that value with your own Web3Forms key.

## Usage

- **Drag** any card on a desktop-width screen and watch the red string follow it.
- **Click** a card (or focus it and press Enter) to open its dossier, and press Escape to close it.
- **Toggle the UV lamp** with the header button or the spinning switch near the top right of the board.
- **Scroll to the end** for the case-closed sequence, then use the Reopen button to jump back to the top.
- **Add or edit a card** by changing the `items` array in the script, and connect cards with an entry in the `links` array (a third value of `true` draws a dashed string):

```js
{id:'example', kind:'manila', x:40, y:20, rot:-1, z:30, tag:'LABEL', title:'Card title', body:'Short summary',
 dossier:{tab:'LABEL', title:'Card title', sub:'Subtitle', meta:'META LINE', facts:['One fact'], verdict:'STAMP TEXT'}}
```

`x` and `y` are percentages of the board, `rot` is the tilt in degrees, and `kind` selects the card style (`manila`, `polaroid`, `note`, `index`, `tipline`, or the default paper card).

## Limitations and Roadmap

- Dragging and the red strings are desktop-only. At 1080px wide and below the board turns into a static vertical list with strings and dragging switched off.
- All card text, dossiers and links are hard-coded in the `items` and `links` arrays in `index.html`, so a content change means editing the file and redeploying.
- Google Fonts and the Web3Forms API need network access. Offline, the fonts fall back to generic monospace and cursive, and a failed form submission shows a direct-email message.
- No automated tests are included.

## Author

**Shahram Shafiq** - [GitHub](https://github.com/shahramshafiq) | [LinkedIn](https://www.linkedin.com/in/shahramshafiq/)
