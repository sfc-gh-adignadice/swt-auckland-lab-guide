# Bonus Exercises

## Bonus 1 - Create repeatable workflows using Skills.

Often you will want to be able to re-run certain analyses or workflows rather than entering a series of prompts into CoWork. A Skill helps package a repeatable workflow. CoWork can then leverage that skill to perform the workflow or task.

Category Managers need to submit an executive briefing on their product category each week. Imagine if we could have Snowflake CoWork generate that for us? 

!!! action "Create an automation to prepare the executive briefing each Monday"
    1. In the left hand menu click **New Chat**
    2. Then click the **+** button in bottom left hand corner of the chat box 
    2. Hover over the **Skills** option then click **/executive_brief**
    3. You will see **/executive_brief** appear in the chat box. 
    4. Click the **Send** button 

![](./assets/bonuscocoskill.png)

**What to expect:**  The Skill contains a set of instructions that guide CoWork through creating a Category Insights Executive briefing. It will:

1. Gather data about category revenue, channel performance and generate as set of category metrics.
2. Try to identify relevant trends and patterns over the last week.
3. Identify possible risks and issues that might need to be investigated and addressed.
4. Generate a set of recommendations.
5. Produce a concise report suitable for briefing the executive.
 

**New feature — Skills:** Skills allow you to capture a workflow or set of instructions that can get CoWork to run. The skills can be associated with the agent, like the example you just used, or users can build there own skills. 

---

## Bonus 2 - Schedule CoWork to do work via Automations

You may have tasks or workflows that you need to run every day, or once week, or once a month. You can define a prompt then ask CoWork to schedule it for you. These are called automations. Lets create a new automation to automatically prepare your executive briefing each Monday morning.

!!! action "Create an automation to prepare the executive briefing each Monday"

    ```text
    Schedule the Category Executive briefing to run each Monday morning at 9am and email me the output
    ```

**What to expect:**  Snowflake CoWork will set up a new **Automation**. This will run automatically every Monday at 9am , call the **executive brief** skill, and then email you the output. You can see you Automations by clicking **Automations** in the left hand menu in CoWork.


**New feature — Automations:** Get CoWork to take a one off prompt, report, or analysis and turn it into a recurring one.

## Bonus 3 - Governance Demo

> *Instructor-led demonstration. Participants watch on the projector.*

The instructor asks the same question using two different roles:
!!! action "Ask the same question with two different roles"
```text
What is total revenue across all departments this year?
```

| Role | Result |
|------|--------|
| HOL_ATTENDEE_ROLE | Returns only Home & Kitchen |
| ACCOUNTADMIN | Returns all four departments |

> *"Same agent, same question, same data. The only difference is the role. Jordan sees their world. The Commercial Director sees everything. No one configured this per-agent — it's inherited from the row access policy your admin already set up."*

**New feature — Row-Level Security inheritance:** CoWork doesn't have its own security model. It inherits whatever RBAC and row access policies your admin already configured in Snowflake. See [Row Access Policies documentation](https://docs.snowflake.com/en/user-guide/security-row-intro).

---

## Bonus 4 - Cost and Monitoring

> **For admins and SE conversations:** CoWork interactions consume Cortex AI credits. Usage is fully observable:

```sql
-- Monitor CoWork usage by user (admin query — not part of this lab)
SELECT USER_NAME, COUNT(*) AS INTERACTIONS, SUM(CREDITS) AS TOTAL_CREDITS
FROM SNOWFLAKE.ACCOUNT_USAGE.CORTEX_AI_FUNCTIONS_USAGE_HISTORY
WHERE FUNCTION_NAME = 'AGENT'
GROUP BY USER_NAME
ORDER BY TOTAL_CREDITS DESC;
```

Key points:
- Every interaction is metered and attributable to a specific user and role
- Admins can set budgets and alerts using Snowflake's standard cost governance
- Deep Research consumes more credits than standard Q&A (multiple sub-queries)
- No opaque per-seat licensing — you pay for what you use

See [Cortex AI Usage History](https://docs.snowflake.com/en/sql-reference/account-usage/cortex_ai_functions_usage_history).
