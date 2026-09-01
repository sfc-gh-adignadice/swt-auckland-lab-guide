# Bonus Exercises

## User Skills (Automation)

You do this kind of Monday morning analysis every week. Instead of repeating the same questions, capture the workflow as a **User Skill** — a personal, reusable multi-step command.

!!! action "Create a reusable User Skill"

    ```text
    Create a skill called "Monday Category Review" that does the following:
    1. Pull this week's revenue for Home & Kitchen by subcategory
    2. Compare to last week and flag any subcategory that declined more than 10%
    3. For any flagged subcategory, identify the top 3 products driving the decline
    4. Summarize findings in bullet points ready for my team standup
    ```

Next Monday, you simply say: `Run my Monday Category Review skill`

**New feature — User Skills:** Personal, reusable workflows saved to your workspace. They run with your data access and can be triggered by name. See [User Skills documentation](https://docs.snowflake.com/en/user-guide/snowflake-cowork/using-cowork#user-skills).

---

## Governance Demo

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

## Cost and Monitoring

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
