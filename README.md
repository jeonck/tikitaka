# TikiTaka

An English speaking-practice site built with [Hugo](https://gohugo.io/) and the
[Hextra](https://github.com/imfing/hextra) theme, deployed to GitHub Pages.

**Live site:** https://tikitaka.metacog.co.kr/

## The idea

Textbooks give you one correct answer per question. In a real conversation that answer
ends the exchange, because the other person has nothing to pick up.

Tiki-taka — short, quick passes that keep possession moving — is the better model. Every
question on this site has **three routes back**, and every answer carries a *pass back*
so the rally continues.

| Route | What it does |
| --- | --- |
| **Return** | Short, safe, instant. |
| **Add** | One concrete detail they can grab. |
| **Flip** | Turns the question around. |

## How the practice loop works

The full answers are hidden behind a collapsed `<details>` block. Only the **trigger
phrase** is visible — *Can't complain —*, *Actually, something —* — because recognising a
sentence and producing one under time pressure are different skills, and only the second
one helps in a real conversation.

Read the question → look at the trigger only → say your own full answer out loud → *then*
open the card and compare.

## Content

16 situations × 10 questions × 3 routes = 480 answers.

**Everyday exchanges** — Small Talk · Weekend & Free Time · Food · Making Plans · Wrapping Up

**Your life** — Work · Home & Neighborhood · Family & People · Health & Energy · Travel & Places

**Things you have opinions about** — Feelings & Opinions · Screens & Sound · Tech & Online ·
Money & Shopping

**The harder ones** — Learning & Language · Awkward Moments

## Local development

```bash
hugo server
```

Requires Hugo **extended** v0.151.0 or later. The theme is committed directly under
`themes/hextra` (not a submodule), so no extra setup is needed.

## Adding a question

Cards are built from two custom shortcodes in `layouts/_shortcodes/`:

```
{{< tk q="How's it going?" ctx="A colleague in the hallway." >}}
{{< tkline tone="Return" hint="Can't complain —"
           say="Can't complain. Same old, same old."
           back="How about you?"
           why="The safest answer in English." >}}
{{< /tk >}}
```

| Param | Where it appears |
| --- | --- |
| `q` | Question, always visible |
| `ctx` | Who asks and when, always visible |
| `cue` | Badge text, defaults to `they ask` |
| `tone` | Route label — `Return`, `Add` or `Flip` |
| `hint` | **Visible trigger phrase** — the speaking cue |
| `say` | Full answer, hidden until expanded |
| `back` | The pass back. Leave empty when the ball should stop |
| `why` | Short note on why the answer works |

## Deployment

Pushing to the site branch triggers `.github/workflows/deploy.yml`, which builds with
Hugo and publishes to GitHub Pages.

FlexSearch is vendored at `assets/js/vendor/flexsearch.bundle.min.js` rather than fetched
from a CDN at build time, so builds are hermetic and do not depend on jsDelivr.

## Licence

Site content: © jeonck. Hextra theme and FlexSearch retain their own licences
(`themes/hextra/LICENSE`, `assets/js/vendor/flexsearch.LICENSE`).
