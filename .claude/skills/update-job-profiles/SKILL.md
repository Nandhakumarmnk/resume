---
name: update-job-profiles
description: Sync Nandhakumar M's job-search profiles (LinkedIn, Naukri, Indeed, and any other job board) to the current master résumé, and attach that résumé everywhere. Use when the user says "update my profile", "update LinkedIn/Naukri/Indeed", "upload my resume everywhere", "sync my profiles", or after regenerating the résumé to a new version.
---

# Update Job Profiles

Bring every job-search profile into agreement with the **current master résumé**, and attach that
résumé file on each platform.

The single most valuable thing this skill does is **consistency**. Recruiters cross-check. A profile
saying "Fresher" next to a résumé saying "5+ years", or ".NET Core = 3" on one site and "5" on
another, costs more than an incomplete profile does.

---

## Step 0 — Establish the master résumé (never skip)

Do not trust a filename. Find the newest versioned résumé and read its **actual content**:

```bash
ls -t "D:/Resume and Jobs Application/resume/"*Resume*.pdf | head -5
```

The master as of **2 Sep 2026** is `Nandhakumar_M_Senior_DotNet_FullStack_Resume_v5.pdf` — identical
to v4 except the contact line adds *Open to Relocate: Hyderabad / Bangalore / Coimbatore / Chennai +
Remote*. Read its HTML source to extract text:

```bash
sed -e 's/<[^>]*>//g' "D:/Resume and Jobs Application/resume/Nandhakumar_M_Senior_DotNet_FullStack_Resume_v5.html" \
  | sed '/^[[:space:]]*$/d'
```

Ready-made copy blocks prepared from v5 (headlines, summaries, per-skill years, per-platform steps)
live in `D:/Resume and Jobs Application/resume/Job_Portal_Profile_Update_Sheet.md` — prefer them over
composing new text.

Then fill in the canonical facts table below from what you actually read, and use it for every
field on every platform. If a platform already disagrees with it, the platform is wrong.

### Canonical facts — verify against the résumé each run

| Field | Value |
|---|---|
| Name | Nandhakumar M |
| Title | Senior .NET Full Stack Developer & Technical Lead |
| Experience | 5+ years |
| Phone | +91 80721-27298 |
| Email | nandhakumarmurugesan45@gmail.com |
| Location | Namakkal, Tamil Nadu, India (637302) |
| Relocation | Hyderabad · Bangalore · Coimbatore · Chennai (+ Remote) |
| LinkedIn | linkedin.com/in/nandhakumar-m-dotnet |
| GitHub | github.com/Nandhakumarmnk |
| Portfolio | nandhakumarmnk.github.io/portfolio/ |
| Education | B.E. Electrical & Electronics Engineering, Karpagam College of Engineering, 2016–2020, CGPA 7.5/10 |
| Current employer | Spark IT Tech, Tiruppur — Senior .NET FS Dev & Technical Lead (Apr 2023–present); .NET FS Dev (Aug 2021–Mar 2023) |
| Notice period | 15 days or less — immediate |
| Current CTC | ₹5,52,000 fixed |
| Languages | Tamil (native/bilingual) · English (professional working) |

### Skill claims — keep these identical everywhere

**Has:** C# · .NET Core · ASP.NET Core 8 · ASP.NET MVC 5 · RESTful Web APIs · EF Core 8 · EF 6 ·
LINQ · ADO.NET · SQL Server · T-SQL · JavaScript · jQuery · AJAX · TypeScript · Bootstrap ·
**React** · JWT · Hangfire · SAP integration · IIS · Azure DevOps · Git · OWASP

**Years to claim:** C# **5** · .NET Core **5** · ASP.NET / ASP.NET MVC **5** · SQL Server **5** ·
EF Core **4–5** · React **1** · overall **5**

**Does NOT have — always answer 0 / No:** Angular · AWS · Azure (upskilling only) · Vue.js · GCP ·
Blazor · Docker/CI-CD (upskilling only)

> Never inflate these to fit a JD. It surfaces in the technical round. Applying honestly to a role
> that lists Angular is fine; claiming Angular is not.

---

## Step 1 — LinkedIn

Profile: `https://www.linkedin.com/in/nandhakumar-m-dotnet`

### Known behaviour — read before editing

- **Write throttle.** After roughly 20 profile writes in one session, writes start failing. Symptoms:
  edit-form URLs return *"Something went wrong on our end"*, list pages render blank, modals spin
  forever. **Reads keep working**, which is how you tell it apart from a browser problem. Restarting
  Chrome does not help. It clears on its own in a few hours. Plan for ~15 writes per sitting.
- **Save needs two clicks.** With `form_input`, the first click on Save only focuses the button.
  Click Save, wait ~4s, screenshot; if the modal is still open, click again. This is normal, not a
  failure.
- **Never type into fields with `computer:type`.** LinkedIn re-renders and silently discards it.
  Always `find` the field, then `form_input` with the ref.
- **`details/*` pages render blank at random.** Don't conclude data is missing from a blank
  `details/skills` or `details/projects` page — verify on the **main profile page** instead, which
  renders reliably (scroll down, then `get_page_text`).
- **A skill edit URL that 500s while other writes succeed** means that skill no longer exists.

### Direct form URLs (faster than clicking through)

```
Add project    https://www.linkedin.com/in/nandhakumar-m-dotnet/edit/forms/project/new/
Add language   https://www.linkedin.com/in/nandhakumar-m-dotnet/edit/forms/language/new/
Add skill      https://www.linkedin.com/in/nandhakumar-m-dotnet/skills/edit/forms/new/
Edit a skill   https://www.linkedin.com/in/nandhakumar-m-dotnet/details/skills/edit/forms/<id>/
Featured       https://www.linkedin.com/in/nandhakumar-m-dotnet/details/featured/
```

### What to sync

Headline, About, Experience (both Spark IT Tech roles under **one** company entry so LinkedIn draws
the promotion), Education, Projects, Languages, Skills (pin ASP.NET Core · C# · Microsoft SQL Server),
Open-to-Work titles and locations.

The old `LinkedIn_Profile_Content.md` no longer exists. Use the copy blocks in
**`D:/Resume and Jobs Application/resume/Job_Portal_Profile_Update_Sheet.md`** — headline (§1a),
summary (§1b), employment descriptions (§3a/3b), and the five project blocks (§3d) — verbatim rather
than composing new text.

### Known blockers — hand these to the user, don't burn turns

- **Featured → Add a link** rejects the portfolio URL (*"Please enter a valid link"*) even though the
  site loads fine. LinkedIn's crawler, not the URL.
- **Featured → Add a document** calls `input.click()` on a hidden input → native OS file picker.
  Cannot be driven, and clicking it **freezes the browser session**. Always manual.

---

## Step 2 — Naukri

`https://www.naukri.com/mnjuser/profile`

Recruiters filter on Naukri's **structured fields**, not the attached PDF. A perfect PDF behind a
"Fresher" profile gets zero calls — this profile was in exactly that state before Aug 2026.

Sync in this order: Resume headline → Key skills → IT skills (with years) → Employment history →
Education → Projects → Preferred locations → Current CTC & notice period → Personal details.

Then attach the master résumé under **Resume** (Naukri's upload does work through the DOM).

**Known issue to check each run:** Personal details → Work permit has read *"US TN Permit Holder"*,
which is only issued to Canadian and Mexican citizens. Clear it if still set.

---

## Step 3 — Indeed

`https://profile.indeed.com/`

- **Résumé replace is MANUAL.** The `...` menu → *Replace file* triggers a native OS picker.
  Uploading to the hidden `input[type=file]` via `file_upload` **does attach the file** (verifiable
  via `javascript_tool`: `document.querySelector('input[type=file]').files[0]`) but Indeed's React
  handler only responds to trusted user events, so a synthetic `change` dispatch does nothing and the
  profile keeps showing the old file. Do not keep retrying — tell the user to do it themselves.
- **`profile.indeed.com/qualifications` frequently hangs** on load (script injection times out).
  Retry twice; if it still hangs, report it rather than looping.
- `/preferences` holds desired pay, job titles and locations.

Indeed's structured **Qualifications** (skills, work experience, education) are what its matching
engine uses — worth filling whenever the page will load.

---

## Step 4 — Other platforms

Same pattern for Monster, Shine, Hirist, Instahyre, Foundit, Glassdoor, or a company ATS:

1. Attach the master résumé.
2. Make headline and years-of-experience match the canonical table.
3. Fill structured skill fields — these drive search ranking far more than the PDF.
4. Set preferred locations to the four cities + Remote.

---

## Step 5 — Report

Always finish with an explicit per-platform status, and be precise about what did **not** happen:

```
LinkedIn  — Projects ✅ 6/6 · Languages ✅ · Skills ✅ · Featured ❌ (needs manual upload)
Naukri    — Profile ✅ · Résumé ✅ v5 attached
Indeed    — Résumé ❌ still v2, native picker (manual) · Qualifications ❌ page hangs
```

Never report a field as updated unless you saw it render on a reloaded page or got an explicit
success toast. LinkedIn in particular shows *"Save was successful"* — quote that as the evidence.

---

## Guardrails

- **Never enter** PAN, Aadhaar, passport, bank, or government ID numbers. A form asking for a PAN at
  *application* stage is a known recruitment-fraud pattern — stop and tell the user.
- Changing salary expectations, notice period, or accepting relocation/shift terms is the user's
  call. Use what the table already records; ask before inventing a new commitment.
- Log every profile change so the tracker and the résumé stay in agreement.
