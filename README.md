# Security+ Drill

A spaced-repetition study site for 1,003 SY0-701 practice questions. You sign in, and your progress is saved to your account, so it follows you between your phone and laptop.

- **GitLab Pages** hosts the site.
- **Supabase** (free plan) handles sign-in and stores your progress.

## Files

| File | What it is |
|---|---|
| `index.html` | The study site |
| `questions.json` | The question bank |
| `config.js` | Where you paste your two Supabase values |
| `supabase.sql` | Creates the progress table and its privacy rules |
| `.gitlab-ci.yml` | Tells GitLab to publish the site |

## Setup (about 20 minutes)

### 1. Create the Supabase project

1. Go to supabase.com, sign up, and click **New project**. Name it `secplus-drill`, set a database password (save it somewhere), pick the region closest to you, and click **Create**.
2. When it's ready, open **SQL Editor** → **New query**. Paste the whole contents of `supabase.sql` and click **Run**. It should say "Success. No rows returned."
3. Open **Project Settings** → **API**. Copy the **Project URL** and the **anon public** key.
4. Open `config.js` and paste them in place of the two `PASTE_…` placeholders. Save the file.

### 2. Put the site on GitLab

1. On gitlab.com, click **New project** → **Create blank project**. Name it `secplus-drill`, set **Visibility** to **Private**, and create it.
2. Upload all five files (including `.gitlab-ci.yml`, which starts with a dot and may be hidden in your file browser). You can drag them in with **+** → **Upload file**, or push them with git.
3. Go to **Build** → **Pipelines** and wait for the `pages` job to pass (about a minute).
4. Go to **Deploy** → **Pages** to find your site's address. It looks like `https://secplus-drill-xxxx.gitlab.io`.
5. Keep it private: go to **Settings** → **General** → **Visibility, project features, permissions**. Under **Pages**, choose **Only Project Members** and save. Only you (signed in to GitLab) can open the site now.

### 3. Connect the two

1. In Supabase, open **Authentication** → **URL Configuration**.
2. Set **Site URL** to your GitLab Pages address from step 2.4, and add the same address under **Redirect URLs**. Without this, the confirmation and password-reset emails link to the wrong place.

### 4. Make your account

1. Open your site, tap **New here? Create an account**, and sign up with your email.
2. Click the confirmation link in the email, then sign in.
3. Lock the door behind you: in Supabase go to **Authentication** → **Sign In / Providers** → **Email** and turn off **Allow new users to sign up**, so nobody else can create an account.

### 5. Put it on your phone

Open the site on your phone and sign in. Then add it to your home screen: in Safari, tap Share → **Add to Home Screen**; in Chrome, tap ⋮ → **Add to Home screen**.

## How saving works

- Your progress saves to your account about a second after each question you rate. The status next to your email shows **Saving…**, **Saved**, or a retry message if you're offline.
- The site also keeps a copy on each device. If you study offline, it catches up the next time you're online. When two devices have different progress, each question keeps whichever answer you gave most recently.
- **Reset progress** erases your progress on every device.

## Changing things

- **New questions per day:** change `NEW_PER_DAY` in `config.js` and upload it again.
- **After any change:** upload or commit the changed file to GitLab, and the site republishes itself in about a minute.
