# Agent-Supported Development with Bob

This lab provides a hands-on experience of how Bob supports you across a variety of development tasks. You'll explore an unfamiliar web application, fix security issues, and enhance the application with new features — all supported by Bob.

---

## Lab Overview

In this lab, you will:

| # | Activity | Bob Capability |
|---|---|---|
| 1 | **Onboard** to an unfamiliar code base | Ask mode, architecture analysis |
| 2 | Fix **vulnerabilities** in the application | Security scanning, findings |
| 3 | Implement a **new feature** — reading time indicator | Plan → Agent mode workflow |
| 4 | Use Bob's **literate coding** to quickly extend the app | Inline intent-driven generation |

> 💡 **Tip:** If you lose your place, refer back to this file at any time.

---

## Step 1: Onboarding

You've been asked to join the team of an existing application called _bobverse_. Unfortunately, all your teammates have left for Disneyworld this week, so there's no one around to help you understand it. Let's see whether Bob can help...

1. In the Bob chat view, ensure you're in **Ask** mode.
2. Type in _"What is the purpose of this application?"_
3. Bob starts analyzing the file structure and identifies key files in the frontend and backend.
4. Bob quickly arrives at the high-level purpose. **Spoiler:** bobverse is a full-stack implementation of a social blogging platform.
5. But only seeing is believing, so:
   1. Start a new task.
   2. Type in _"How do I start this application?"_
6. Bob analyzes key files like READMEs and Makefiles, and comes up with clear steps.
7. In the terminal, enter the following commands **step-by-step**:
   ```bash
   make setup
   make init-db
   make start
   ```
8. Open your browser at **http://localhost:30402/**
9. While you explore the UI, start a new task in Bob.
10. Type in _"Explain the application architecture."_
11. This will run for some time, but it's worth the wait — Bob will produce a comprehensive architecture overview, including Mermaid diagrams for component structure and dataflow.
12. Browse through the analysis. Feel free to ask follow-up questions in the same task — Bob will reuse the architecture context it gathered.
13. Now let's save this information for subsequent interactions:
    1. Switch to **Agent** mode.
    2. Type in _"Store this information under `context/architecture.md`"_

✅ **Congratulations!** You now know what bobverse is about, and are ready to enhance it!

---

## Step 2: Fix Vulnerabilities

Not all is well in the bobverse code base... A careless colleague has sprinkled security issues and vulnerabilities all over. But with Bob, you'll be able to fix them in no time!

1. Switch to **Agent** mode.
2. Open `bobverse/infrastructure/repositories/user.py`
3. Check `search_users_by_keyword` — someone got a little sloppy with SQL...
4. Let's see if Bob can help fix this. We'll use a file reference in the chat:
   - Type in _"Please analyze @bobverse/infrastructure/repositories/user.py for security vulnerabilities and add to findings"_
5. The first finding should relate to a **SQL injection** vulnerability.
6. Ask Bob for options to fix it:
   - _"Please give me options to address the SQL injection vulnerability"_
7. Ask Bob to implement the recommended solution (which should be SQLAlchemy with `ilike` or parameterized queries).
8. After Bob finishes, click **Show all** next to _1 file changed_ at the bottom of the chat. This shows the diff of the changes Bob implemented.

✅ **Congratulations!** The vulnerability is fixed!

---

## Step 3: Implementing a New Feature — Reading Time Indicator

The articles published in bobverse lack an indicator of how long they take to read. Let's add this — through Bob.

### Bob suggests an approach

1. Switch to **Plan** mode. As always, there is more than one way to implement this. Let's have Bob weigh in...
2. Start a new task.
3. Type in:
   > _"The requirement is to show an estimated reading time in the UI, both for each article and in the feed lists. Create two implementation approaches and describe their pros and cons. Speed of implementation is important."_
4. You may notice Bob uses a skill to create a plan, and may launch a sub-agent to analyze the codebase. The sub-agent approach keeps your main task's context window from growing too large.
5. Bob comes up with several approaches, including:
   - Calculating reading time in the **frontend** (client-side)
   - Calculating reading time in the **backend** (server-side)
6. Bob describes the pros and cons for each.
7. We'll go with the **frontend implementation** — it's faster to implement and deploy. Bob most likely agrees. 😄

### Bob implements the feature

8. If Bob ends the task with buttons for your design choices, choose the **Pure Frontend Utility** approach.
9. Otherwise, do this manually:
   1. In the same task, switch to **Agent** mode.
   2. Staying in the same task ensures Bob retains the required context.
   3. Type in: _"Implement the frontend calculation approach"_
10. Bob goes ahead and starts the implementation.
11. Once complete, open your browser at **http://localhost:30402/** (run `make start` in the terminal if the app isn't running).
    - Articles now show an estimated reading time.
    - Add a new article and see how the reading time changes with article length:
      1. Click **New Article** in the top right.
      2. Fill out the form and click **Publish**.
      3. You should see the reading time calculated based on the content.

### Bob reviews the implementation

12. Let's check the implementation before committing — and have Bob do it.
    > **Note:** These instructions work if you cloned this codebase from a repository. If not, just ask Bob to review the code and continue the discussion in chat.
13. On the far-left toolbar, select the **Source Control** icon, then open the **Review** panel (at the bottom) and select **Start Review**.
14. Bob reviews your changes step-by-step.
15. Bob publishes the findings in the **Bob Findings** view.
16. Explore the findings view — by default it's organized by file.
17. Select a finding and click **Go To Location** to see it in context.
18. If desired, click **Fix with Bob**.
19. A new task opens automatically where Bob addresses the issue.
20. When the task is complete, the finding status switches from _open_ to _resolved_.
21. Explore other findings at your leisure.

✅ **Congratulations!** You implemented your first bobverse feature!

---

## Step 4: Literate Coding

Sometimes you just want to describe your ideal feature in plain language. This is where Bob shines with **literate coding**.

Let's try it by adding a toggle to filter articles published within the last 24 hours.

1. Open `frontend/src/widgets/articles-feed/articles-feed.ui.tsx`
2. Turn on **Literate Coding** mode by clicking the magic wand icon (✨) in the editor toolbar.
3. On **line 71**, enter the following intent:
   ```
   Add toggle to show latest articles created in the last 24 hours
   ```
4. Now add a unique empty-state message. Jump to **line 81** in the same file and enter:
   ```
   Add unique message when toggle enabled
   ```
5. Click **Generate**.
6. Bob creates code according to your intent. Review it in the diff view that appears.
7. Click **Accept all**.
8. Save the file.
9. Open your browser and reload bobverse at **http://localhost:30402/**.
   - Notice the new toggle at the top of the article list.
   - Enable the toggle to filter to only the most recent articles.

✅ **Congratulations!** You've completed the lab!
