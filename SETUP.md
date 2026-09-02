# ⚡ Setup — do this before you arrive

**20 minutes.** Do it at your desk, not in the room.

---

## 1. Check what you already have

```bash
node --version   # need v22 or higher
git --version    # any recent version
```

If Node is missing or older than v22, install the **LTS** build from
[nodejs.org/en/download](https://nodejs.org/en/download), then **open a new terminal** and
check again.

> 🔒 **If your laptop blocks installs**, raise the ticket now — approval takes longer than
> the hackathon does. If you have Docker instead, the lab repo ships a dev container that
> includes Node. You only need one of the two.

---

## 2. Install the GitHub Copilot app

Follow [Lesson 1 of the official workshop](https://github-samples.github.io/copilot-workshops/app/1-install-copilot-app/).

Then check:

- [ ] The app launches
- [ ] You're signed in **with your work GitHub account**, not a personal one
- [ ] You can see your organisation's repositories

> 🚨 **App won't sign in?** On Copilot Business or Enterprise this is almost always an admin
> policy, and you can't fix it yourself. **Tell your facilitator today, not on the day** —
> send them [ADMIN.md](ADMIN.md).

---

## 3. Make your copy of the lab app

1. Go to **[github-samples/tailspin-toys](https://github.com/github-samples/tailspin-toys)**
2. **Use this template** → **Create a new repository**
3. ⚠️ Create it in the org your facilitator gave you — **not your personal account**

Write it down so you're not hunting for it later:

```
My repo: github.com/ ______________ / ______________
```

The template seeds its own issue backlog. That backlog is your hackathon material — you don't
have to invent anything.

> 🔒 **"Use this template" doesn't work?** If your company uses Enterprise Managed Users this
> can be restricted. Tell your facilitator — there's a prepared fallback repo.

> 🔁 **Already created it under your personal account?** You don't have to start over.
> Open the repo → **Settings** → **Transfer ownership** → pick the org. Issues, branches and
> history all move with it. Then repoint your clone:
> ```bash
> git remote set-url origin https://github.com/<your-org>/<your-repo>.git
> ```

---

## 4. Prove it runs

```bash
git clone https://github.com/<your-org>/<your-repo>.git
cd <your-repo>
npm install
npm run test:unit
```

Tests running — even with failures — means you're ready. The agent will use them to check its
own work.

> ℹ️ **There is no `npm test` in this repo.** The scripts are `npm run test:unit` (Vitest) and
> `npm run test:e2e` (Playwright). Only the unit tests are needed for setup — the E2E suite
> builds the site and needs a browser download, so leave it for the day itself.

---

## ✅ Ready

- [ ] Node 22+ and git
- [ ] Copilot app signed in with **work** identity
- [ ] My repo exists, in the **right org**
- [ ] `npm install` and `npm run test:unit` have run at least once
- [ ] I know my repo URL

**Bring a laptop that can install things and reach the internet.** If you'll be on guest
wifi, test it in advance.

See you there 🚀
