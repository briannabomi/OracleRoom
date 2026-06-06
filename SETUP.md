# The Oracle Room — Kit + Vercel setup

Two short jobs: connect the form to Kit so signups get the `Oracle_Room` label and the
email + Zoom link, then put the page live on Vercel. ~15 minutes total.

## Files in this folder
- `oracle-room.html` — the page (this is the one you edit/deploy)
- `vercel.json` — makes Vercel serve the page at your root domain `/`
- `hero-hands.jpg` — your hands hero image (add this; see "Hero image" below)

---

## 1. Kit (ConvertKit)

### a. Make the label
Kit > **Subscribers** > **Tags** > **Create Tag** → name it exactly `Oracle_Room`.
(Kit calls labels "tags." This is the label every Oracle Room signup gets.)

### b. Create the form that feeds it
1. Kit > **Grow** > **Landing Pages & Forms** > **Create New** > **Form** > pick any
   inline template (you won't show Kit's design — your page is the design).
2. Open the form > **Settings** > **Incentive / After subscribe** isn't needed yet.
3. Form **Settings** > **Subscriber settings** (or the form's automation) > **Add tag on
   subscribe** → `Oracle_Room`. This is what attaches the label automatically.
4. Save. Look at the form's URL: `app.kit.com/forms/XXXXXXX`. That number is your
   **form ID**.

### c. Add the custom fields (so the extra answers are saved)
Kit > **Subscribers** > **Custom fields** > add these four, named exactly:
`full_name`, `state_now`, `present_percent`, `notes`.
(Email is built in. If you'd rather use Kit's built-in first-name field, that's fine too —
the page just sends `full_name` as a custom field.)

### d. Drop the form ID into the page
Open `oracle-room.html`, find this line near the bottom and paste your number:
```js
var KIT_FORM_UID = "YOUR_KIT_FORM_ID";
```

### e. Send the email + Zoom link
Kit > **Automations** > **Visual Automations** > **New** >
trigger **"Is added to a tag" → `Oracle_Room`** > action **Email** (or a Sequence) that
contains your welcome note and the Zoom link. That's the email that goes out the moment
someone signs.

> The page posts straight to your Kit form, so no API key lives in the page (nothing to
> leak). On success it shows the "You're in" panel instead of bouncing to a Kit page.

---

## 2. Vercel

Easiest path, no command line:
1. Put this folder in a GitHub repo (or use Vercel's drag-and-drop: **Add New… > Project
   > Deploy** and drop the folder).
2. In Vercel, **Import** the repo → **Deploy**. No build step; it's a static site.
3. `vercel.json` already points `/` at `oracle-room.html`, so your root domain shows the
   page. Add your custom domain under the project's **Domains** tab.

CLI alternative: `npm i -g vercel`, then run `vercel` in this folder and follow prompts.

---

## Hero image
Save your treated hands photo in this folder as **`hero-hands.jpg`**. The hero is wired to
it; until it exists, a dark gold/oxblood gradient stands in (the page still looks finished).
Ask me and I'll crop your photo to hands-only and apply the candlelit treatment once the
original file is in this folder.

## Test before you share
Open the live URL, tick all eight, submit with your own email, and confirm: (1) you land on
the "You're in" panel, (2) you appear in Kit with the `Oracle_Room` label, (3) the automation
email with the Zoom link arrives.
