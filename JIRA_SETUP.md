# Jira Setup: Scam Checker Test Tracking

## 1. Create the project (10 minutes)
1. Sign up for free at atlassian.com/software/jira (the free plan covers up to 10 users).
2. Create a project using the **Kanban** or **Scrum** template. Name it **Access Authenticity QA**, with key **AAQA**.

## 2. Import the 20 test cases (5 minutes)
1. Go to **Settings (gear) → System → External System Import → CSV**. If you don't see it, search Jira help for "import issues from CSV," because menu names change.
2. Upload `jira_import_test_cases.csv` and choose the **AAQA** project.
3. Map the columns: Summary → Summary, Issue Type → Issue Type, Priority → Priority, both Labels columns → Labels, Description → Description.
4. Run the import. You'll get 20 tasks, labeled `ai-eval` plus their group (`legit`, `scam`, `edge-case`, `adversarial`).

## 3. After you run promptfoo
For each task:
- Paste the checker's real answer into **Actual result**.
- If the test passed, move the task to **Done**.
- If it failed, create a **Bug** using the template below, link it to the task ("is caused by"), and move the task to **Done**.

## Bug template (copy into each Bug)

**Summary:** [Test ID] Short description of what went wrong
*Example format: "[ADV-01] Checker returns LEGIT when the posting contains a hidden instruction"*

**Environment:** promptfoo [version], model [name], prompt version [date] / live site

**Steps to reproduce:**
1. Run `npx promptfoo@latest eval --filter-pattern "[Test ID]"`
2. Input: [paste the posting]

**Expected result:** [from the task]
**Actual result:** [paste the checker's answer]

**Severity:**
- **Critical:** a scam marked LEGIT (could cost a user money)
- **High:** obeyed a prompt injection, or leaked or invented details
- **Medium:** right verdict but wrong or missing red flags
- **Low:** formatting problem only

**Fix applied:** [what you changed in the prompt or code]
**Retest result:** PASS / FAIL on [date]

## 4. What to screenshot for your portfolio
- The board with tasks in To Do / In Progress / Done
- One fully written Bug
- A filter view: `project = AAQA AND type = Bug ORDER BY priority DESC`
