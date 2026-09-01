# 1 — Attendee setup

**Audience:** everyone attending
**When:** before you walk into the room
**Time needed:** 20–30 minutes

Please complete this beforehand. Session time is short and it is far better spent building
than installing.

---

## What you need

- [ ] A GitHub account **with an active Copilot seat** (Business, Enterprise, Pro, Pro+, or Student)
- [ ] macOS, Windows, or Linux
- [ ] **Node.js 22 or newer**
- [ ] **git**
- [ ] The **GitHub Copilot app**, installed and signed in

> 🏢 **On a corporate GitHub account?** Sign in with your **work identity**, not a personal
> GitHub account. If your company uses Enterprise Managed Users, a personal account will not
> have access to your organisation's repositories or your Copilot seat.

---

## Step 1 — Node.js and git

Check what you already have:

```bash
node --version
git --version
```

If `node` reports **v22** or higher, you're done with this step.

Otherwise install the **LTS** build from [nodejs.org/en/download](https://nodejs.org/en/download).
Accept the defaults; on Windows keep **Add to PATH** selected. Then **open a new terminal**
and check the version again.

> 🔒 **If installation is blocked** by your company's device policy, raise a ticket now
> rather than on the day — approval usually takes longer than the session does.
> Alternatively, if you have Docker, the lab repository includes a dev container that
> bundles Node for you. You don't need both.

---

## Step 2 — Install the GitHub Copilot app

Follow [Lesson 1 of the official workshop](https://github-samples.github.io/copilot-workshops/app/1-install-copilot-app/).

Then confirm it actually works:

- [ ] The app launches
- [ ] You are signed in **with your work identity**
- [ ] You can see your repositories

> ⚠️ **If the app won't sign in and you're on Copilot Business or Enterprise**, this is
> almost certainly an administrator policy, not something you can fix. Tell your facilitator
> immediately and point your admin at [0-admin-setup.md](0-admin-setup.md).

---

## Step 3 — Create your copy of the lab repository

1. Go to **https://github.com/github-samples/tailspin-toys**
2. Click **Use this template** → **Create a new repository**
3. ⚠️ **Create it in the organisation your facilitator specified** — not your personal
   account. Write the exact target org in the box below before you start.
4. Note the full path you created: `___________________ / ___________________`

The template automatically seeds a backlog of issues. You'll work from those — there's
nothing to write yourself.

> 🔒 **If "Use this template" fails or the org isn't available to you**, stop and tell your
> facilitator. On Enterprise Managed Users this step is sometimes restricted and there is a
> prepared fallback repository.

---

## Step 4 — Verify the project runs

Clone your new repository and confirm it builds:

```bash
git clone https://github.com/<your-org>/<your-repo>.git
cd <your-repo>
npm install
npm test
```

If the tests run — even if some fail — you're ready. The agent will use these later to check
its own work.

---

## Ready-to-go checklist

- [ ] `node --version` shows v22 or higher
- [ ] `git --version` works
- [ ] Copilot app installed, signed in with **work identity**
- [ ] My copy of the lab repository exists, in the **correct org**
- [ ] `npm install` and `npm test` have run at least once
- [ ] I know my repository path

**Bring a laptop that can install software and reach the internet on the day.** If you're
joining on a guest network, test it in advance if you possibly can.
