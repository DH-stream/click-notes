# Click Notes

Click Notes is a lightweight browser extension for collecting visual UI feedback directly on local and hosted web projects.

The workflow is intentionally simple:

```txt
Click an element → write a note → save → repeat → copy all notes
```

The tool is designed for personal development workflows where visual feedback needs to become clear, structured build notes for ChatGPT, Codex, GitHub issues, pull requests, or project documentation.

## Why this exists

When reviewing UI work, it is often hard to describe exactly which element needs attention.

Instead of writing vague feedback like “the thing at the top feels wrong”, Click Notes lets the reviewer point directly at an element in the browser, write their own comment, and export all notes as a structured handoff.

The user-written comment is the source of truth. Element metadata is only included to make the comment easier to locate and implement.

## Intended use

Click Notes is primarily intended for the owner’s own projects, including:

- Localhost development builds
- Vercel preview deployments
- Vercel production deployments
- Design-heavy web apps
- Personal developer tooling

It is not intended to be a public analytics tool, tracking tool, or general-purpose feedback widget for external users.

## MVP scope

The first version should focus on a fast, reliable capture flow:

- Start capture mode from the browser extension popup
- Highlight hovered page elements
- Click an element to open a comment box
- Let the user write their own note
- Save multiple notes during the same review session
- Show a count of saved notes
- Optionally show numbered pins on the page
- Copy all notes as Markdown
- Clear notes when finished

## Export should include

Each exported note should include useful context such as:

- Page URL
- Page title
- Viewport size
- Element tag
- Best available selector
- Element text, when available
- Element position and size
- Optional data attributes such as `data-note`, `data-component`, or `data-testid`
- The user-written comment

The exported output should be readable by both humans and AI coding tools.

## Preferred export style

The copied output should be Markdown-first.

Example:

```md
# Visual build notes

Page: http://localhost:3000/dashboard
Viewport: 1440x900

## Note 1

Element:
- Tag: button
- Text: Save
- Selector: button.primary-action
- Position: x=1024 y=720 w=120 h=44

Comment:
This button should feel more prominent and easier to notice.
```

## Development approach

The first implementation should stay boring and simple.

Prefer:

- Manifest V3 browser extension
- Plain HTML, CSS, and JavaScript for the MVP
- No backend
- No database
- No login
- No AI processing
- Local browser storage only
- Manual copy-to-clipboard export

Avoid overengineering the first version. The goal is to quickly create a working personal tool that can be tested on real projects.

## Supported targets

Initial browser permissions should be limited to development and personal deployment URLs, such as:

- `http://localhost/*`
- `http://127.0.0.1/*`
- `https://*.vercel.app/*`

Additional project domains can be added later if needed.

## Future ideas

Possible future improvements:

- Screenshot thumbnail per note
- JSON export in addition to Markdown
- Copy as ChatGPT prompt
- Copy as Codex prompt
- Export as GitHub issue body
- Group notes by URL
- Edit/delete saved notes before copying
- Session history
- Better selector generation
- React component hints via `data-component`
- Support project-specific metadata
- Optional local endpoint integration for custom tooling
