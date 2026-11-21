# MakeFun Zero to First Bounty

**The Beginner’s Field Guide to Building With AI Agents**

MakeFun runs contests called **bounties**. Each gives you a task, a deadline, and rules for scoring your work. An AI coding agent can edit files and run checks while you decide what to build and whether it meets the brief. For your first bounty, aim for something you can inspect yourself, like a short guide another person can follow.

**[Create a MakeFun account through my referral link](https://make.fun/r/42d49ccz)**

I’m `@adeodu-yinka`, the author of this guide. If MakeFun verifies an eligible signup through my link (`42d49ccz`), it can improve this guide’s ranking. Qualifying referrals may also earn me rewards. The link is optional. [Browse MakeFun directly](https://make.fun/)

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/lastborn04/makefun-zero-to-first-bounty/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/lastborn04/makefun-zero-to-first-bounty/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

[Pick a bounty](#choose-a-bounty) · [Open Codespaces](#open-the-workspace) · [Collect transcripts](#collect-evidence-and-check-the-entry) · [Fix an error](#fix-a-blocked-step) · [Checklist](#first-bounty-checklist)

## What you’re working toward

| You’ll see | What it means |
| --- | --- |
| Bounty brief | The task, entry format, rules, and deadline. |
| Entry | The work you send for review. A repository is a project folder on GitHub. A commit identifies one saved version. |
| Transcript | The original session log your coding agent records as it works. MakeFun can compare it with your entry. |
| Ranking | Entries ordered by the bounty’s scoring rules. A live position can change after final checks. |
| Prize | A reward for an eligible winning entry, paid in USDC on Solana. USDC is a dollar-denominated digital token. |

A first milestone you can control is getting an entry through validation. A paid place depends on the final results and payout rules. [How MakeFun works](https://make.fun/how-it-works)

## Choose a bounty

1. Open the signup link above and choose **Sign in**. If you already have an account, use it. The competition permits one account per person.
2. Open your MakeFun profile. If your bounty requires GitHub, sign in with GitHub or link GitHub from the profile. Check that the username shown there is the one you’ll use to own the entry repository.
3. Open a bounty and read **Before you start**, the full brief, and the scoring and payout sections. Write down the deadline with its time zone, the files or URLs you owe, and any required software.

Try this test before picking a bounty. Finish the sentence **“I’ll know my entry is ready when I can show ___.”** For a writing bounty, the blank might be “a stranger can follow my first three steps and explain what they would submit.” For a coding bounty, it might be “the kit’s practice test accepts my smallest working example.” Choose a brief with a result you can verify and time left to fix it.

**On an iPad?** Read the brief in your browser first. If a bounty requires desktop-only software, choose one whose whole entry can be built and checked in a browser-based workspace. Check that your GitHub account can create a Codespace and that your Codex sign-in is available before committing to the deadline. [MakeFun prerequisites and kits](https://make.fun/skill.md)

## Build in your browser

This path uses GitHub Codespaces for the terminal and Codex CLI for the recorded build. The example assumes a bounty that accepts a GitHub repository and a transcript bundle. Use the current bounty’s rules for its exact license, wallet, and entry requirements.

### Open the workspace

After the bounty opens, create a fresh repository under your linked GitHub account. Select the visibility the bounty requires. For a public GitHub entry, choose **Public** and use the repository creation form to add an initial README and an approved license, such as MIT, when required. Start the agent session after the opening time.

1. On the GitHub repository page, choose **Code**, then **Codespaces**, then **Create codespace** for the branch with your README. Wait for the browser editor to finish loading.
2. In the editor, use **Terminal → New Terminal**. If the menu is collapsed, open the menu in the top-left corner first. Tap inside the terminal panel before pasting a command.
3. On an iPad, try landscape orientation and keep the bounty brief open in a second tab. If Safari reloads the editor, reopen the same workspace from your Codespaces list so you can find the files and session logs that are already there.

Run these commands in the terminal. `pwd` prints your current folder, and the Git command shows the remote repository that your local folder points to. Commands in blocks labeled `sh` go in the terminal. The assignment below goes in the Codex chat.

```sh
pwd
git remote -v
node --version
```

Check that the remote shows the repository you intend to enter. For the MakeFun kit, use a compatible Node release. MakeFun documents a minimum of Node 22.18 and an incompatibility with Node 23.0–23.7. Check your kit’s own requirements. [Create a Codespace](https://docs.github.com/en/codespaces/developing-in-a-codespace/creating-a-codespace-for-a-repository) · [MakeFun agent documentation](https://make.fun/skill.md)

### Download the kit outside the repository

From the repository terminal, replace `replace-with-bounty-slug` with the part after `/bounty/` in your bounty’s URL. For example, this guide’s bounty uses `bring-the-humans-02`. Keep this terminal open. `REPO` remembers your entry folder for the life of that terminal.

```sh
SLUG='replace-with-bounty-slug'
REPO="$(pwd)"
mkdir -p "$HOME/makefun-kits" &&
  cd "$HOME/makefun-kits" &&
  curl -fL "https://make.fun/c/$SLUG/kit" -o "$SLUG.tar.gz" &&
  tar -xzf "$SLUG.tar.gz" &&
  cd "$SLUG-kit"
```

Run `pwd` and `ls`. The folder should end in `-kit`, and the listing should include `RULES.txt`, `kit.json`, and `cli`. Copy the folder path for your Codex assignment. Run `less RULES.txt` to read the file and press `q` to return to the terminal. Check the entry format, transcript policy, and **Check it locally** or **Grade locally** section. The competition name and file inventory are in `kit.json`. [Official MakeFun kit instructions](https://make.fun/skill.md#3-get-the-kit)

### Connect the two sign-ins

**MakeFun** pairs the kit’s command line with your existing MakeFun account. From inside the kit, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

1. Open the MakeFun approval link from the terminal in a browser tab. Check that the site is `make.fun`, you’re signed in to the intended account, and the code on the page matches the one printed in the terminal.
2. Review the permissions and approve. If the terminal says it’s still waiting and returns to the prompt, rerun the same command. The CLI can resume polling the same approval until its code expires. If the approval has expired, follow the new code from a fresh run.
3. Look for the CLI’s connection confirmation and verify your MakeFun handle. The CLI may create a Solana signing keypair. Keep it outside GitHub and keep access to the signing wallet if your bounty uses it to claim a prize.

**Codex** uses its own sign-in. Return to the entry folder, then check whether Codex is installed.

```sh
cd "$REPO"
codex --version
```

If the command is missing, install Codex in the Codespace using OpenAI’s Linux CLI instructions, then run `codex --version` again. For a remote terminal like Codespaces, OpenAI documents device-code sign-in. Enable it in your ChatGPT security settings if your account permits it. Run the login command, open the link printed in the terminal, and enter the one-time code on the official sign-in page. Run `codex` after authentication succeeds.

```sh
codex login --device-auth
codex
```

[MakeFun pairing guide](https://make.fun/skill.md) · [Install Codex CLI](https://developers.openai.com/codex/cli) · [Codex authentication](https://developers.openai.com/codex/auth)

### Give the agent a small first task

When the Codex input box appears, paste the assignment below and replace the bracketed text with the full path you copied, ending in `/RULES.txt`. Read Codex’s approvals before accepting them. If the kit path is inaccessible, open the rules in a second terminal and give Codex the specific requirement it needs to continue.

```text
Read the rules at [full path to RULES.txt].
Tell me the required deliverables and how each is checked.
Build the smallest version I can inspect in this repository.
Show the files changed and one way to check the result.
Pause for review before pushing or submitting.
```

Read what the agent produced. Pick one real improvement based on something you observed. For example, if a reader needs to guess which folder a command runs in, ask the agent to say where to run it and what successful output looks like. Have the agent make the edit in the same recorded session. For some bounties, the transcript must show both an initial write and a later edit.

## Collect evidence and check the entry

Open a second terminal so you can keep the Codex session available. The commands below assume that terminal starts at your repository root. Replace the slug with your own and check `pwd` first.

```sh
REPO="$(pwd)"
SLUG='replace-with-bounty-slug'
cd "$HOME/makefun-kits/$SLUG-kit"
node cli/makefun.mjs bundle --repo "$REPO" --dry-run
```

Run the dry run after Codex’s first edit. Look for the recorded Codex session and read the **run record** summary. The dry run writes no bundle. Fix a missing session while you still have access to the Codespace that recorded it.

Include the genuine logs for all sessions that worked on the entry and any parent or worker sessions the rules require. MakeFun’s run record needs your original opening prompt, agent client and version, model and effort, instruction files and system prompt, and the MCP servers used. If the CLI flags a missing field, supply the value from your actual run. For example, use `--effort default` only if the client used its default. Keep the bundle outside GitHub and review what MakeFun will receive. [MakeFun transcript and run-record instructions](https://make.fun/skill.md)

When the files are ready, review the staged changes and commit only the intended entry files. From inside the kit, save the transcript bundle and check the commit you plan to enter. If the dry run needed extra flags, use those same flags on the bundle command.

```sh
BUNDLE="$PWD/transcripts.tar.gz"
COMMIT="$(git -C "$REPO" rev-parse HEAD)" &&
  node cli/makefun.mjs bundle --repo "$REPO" --out "$BUNDLE" &&
  node cli/makefun.mjs check --kit . --repo "$REPO" \
    --commit "$COMMIT" --transcripts "$BUNDLE"
```

**Local check.** The command above checks the saved commit and your transcript bundle. Saving an edit in the editor does not change that commit. If the kit offers `grade-local`, follow its rules for a practice score. This referral bounty scores on MakeFun’s server.

**Official entry.** For a GitHub submission, push the intended commit and verify that GitHub displays it. Use the bounty’s **Enter** form or the route named in the kit and attach the bundle. Follow the bounty’s wallet signing instructions. Save the receipt and open entry status to see MakeFun’s server verdict. The receipt confirms MakeFun received the entry. Review can still reject it, even after a passing local check. Check the quota and replacement rule before retrying. [Official entry workflow](https://make.fun/skill.md)

## Fix a blocked step

**`No such file or directory` or `Cannot find module …/cli/makefun.mjs`.** Run `pwd` and `ls`. For MakeFun commands, switch to the folder containing `RULES.txt` and `cli`. Start Codex in the entry repository.

**`curl` returns HTTP 404, or the kit won’t unpack.** Check the slug against the bounty URL. Try downloading the kit from the bounty page if the terminal download fails. After unpacking, confirm the competition name in `kit.json` before you run its CLI.

**The CLI reports a missing `node:zlib` export.** Run `node --version` and compare it with the kit’s runtime requirements. Switch to a supported release before retrying. [MakeFun runtime notes](https://make.fun/skill.md)

**Codex sign-in loops in the browser.** Try the documented device-code flow from the Codespace. Confirm that device-code sign-in is enabled for your ChatGPT account or allowed by your workspace. If it’s unavailable, follow OpenAI’s authentication options or use a supported local setup. [Codex authentication](https://developers.openai.com/codex/auth)

**MakeFun pairing expires or shows another handle.** Check which MakeFun account is open in the approval tab. Run the kit’s `login` flow again and verify the handle when it finishes. Use your existing account.

**GitHub says permission denied or the checker rejects the owner.** Use `git remote -v` to check where the push goes. Compare the repository owner with the linked account shown in your MakeFun profile, and confirm your GitHub session has write access. Check visibility and the creation date against the brief.

**The bundler finds zero sessions.** Run it in the environment where Codex wrote the logs and use the actual path to the entry repository. Read `bundle --help` for discovery options, including `--session` for a genuine file the kit missed. Keep the original timestamps and messages. An ordinary chatbot account export does not satisfy MakeFun’s transcript requirement.

**Validation names a missing file or the wrong commit.** Run `git -C "$REPO" status --short` to see uncommitted changes and `git -C "$REPO" ls-tree --name-only HEAD` to see the files in the commit. Fix the named file, commit it, and rerun the check. For this guide bounty, the README, license, and actual public GitHub screenshot belong at the repository root.

## Read the result and claim a prize

A bounty can rank by test results, a judging rubric, or a metric such as verified referrals. For **Bring the humans again**, signup counts shown during the contest are provisional. MakeFun verifies eligible new signups and rechecks repository ownership, visibility, identity, and referral code before the result. An accepted entry can finish outside a paid place. [Official scoring and final check](https://make.fun/bounty/bring-the-humans-02)

If the official result shows you won, check your MakeFun profile for the claim and its deadline. For this bounty, the prize is held in Solana escrow and the winning entry’s signing wallet claims it. For other bounties, check **Payout** for the wallet, claim window, and any verification or payout details requested. Keep your recovery phrase or keypair private throughout. [Official MakeFun requirements and payout information](https://make.fun/api/competitions/bring-the-humans-02/requirements)

## First-bounty checklist

- [ ] I picked an open bounty I can finish with my device and budget.
- [ ] I checked the deadline, scoring, account links, and required files.
- [ ] I started a recorded agent session after opening and checked that the kit finds it.
- [ ] I inspected the build, asked for a meaningful improvement, and reviewed the result.
- [ ] I prepared the required commit and a genuine transcript bundle, then ran the checks.
- [ ] I know which wallet, if any, must sign and how to check my receipt after entering.

## FAQ

**Can I do this on an iPad?** You can read briefs and manage your account in a browser. In this walkthrough the terminal and files live in a Linux Codespace. Use GitHub’s browser instructions if the editor behaves differently on your device. A bounty with desktop-only prerequisites needs a suitable device or a different bounty. [GitHub Codespaces browser instructions](https://docs.github.com/en/codespaces/developing-in-a-codespace/creating-a-codespace-for-a-repository)

**Do I need programming experience?** You can start with a small writing or build task. You’ll still need to read the rules, review what your agent changed, and know how to tell whether it works.

**What could it cost?** Check the bounty’s entry-fee rules, your Codex access or model usage, and GitHub Codespaces compute and storage billing. Stop the Codespace when you’re done. Keep needed logs and wallet access before deleting the environment. [GitHub Codespaces billing](https://docs.github.com/en/billing/managing-billing-for-your-products/managing-billing-for-github-codespaces/about-billing-for-github-codespaces)

**Who can enter?** Read the eligibility terms for your specific bounty. This one requires entrants to be at least 18 or the age of majority where they live, and has sanctions and local-law restrictions. It also requires a public repository owned by your linked GitHub account. [Official bounty rules](https://make.fun/bounty/bring-the-humans-02)

**Who sees my work and session logs?** A public repository can be read by anyone. MakeFun says it keeps submitted transcripts private from the public and uses them for checks and review. Keep secrets out of the agent chat, shell commands, repository, and screenshot. Inspect the bundle for sensitive material and use the official redaction options for personal details when needed. [MakeFun transcript policy](https://make.fun/skill.md)

**Can I count on a payout?** Budget as if you’ll earn zero. A successful check tells you about the entry requirements. The official ranking, eligibility checks, and claim rules determine whether you receive a prize.
