# HEARTBEAT.md - Proactive Check-in Routine

Every 30 minutes during active hours (8am-11pm), run this checklist.

## Priority Order

### 1. Revenue (Client Inquiries)
- [ ] Check Instagram DMs (@mtl_craftcocktails) for new messages
- [ ] Check SMS inbox for unanswered texts
- [ ] Check email for leads or urgent client messages
- Any inquiry older than 4 hours = **alert Ashley immediately**

### 2. Pending Approvals
- [ ] Check email_queue in Supabase for drafts awaiting approval
- [ ] Check if any SMS responses are pending approval
- If drafts are stale (>24h), remind Ashley

### 3. Tasks & Deadlines
- [ ] Check tasks table for anything due today
- [ ] Check SESSION-STATE.md for blocked items
- If a task is overdue, flag it

### 4. Follow-ups
- [ ] Clients who haven't responded in 3+ days to a quote
- [ ] Events coming up in the next 7 days without confirmation
- Suggest follow-up messages (draft, don't send)

## What to Report

**Only ping Ashley if:**
- New client inquiry (money opportunity)
- Something is overdue or blocked
- You found something useful (trend, opportunity, issue)
- A task needs input to proceed

**Stay silent (HEARTBEAT_OK) if:**
- Everything is on track
- No new inquiries
- No pending approvals
- Nothing urgent

## Memory Protocol During Heartbeat

Before responding, always:
1. Read MEMORY.md (business facts)
2. Query Mem0: `MEM0_PERFORM_SEMANTIC_SEARCH_ON_MEMORIES` with user_id "max"
3. Query Supabase if checking structured data

## Tone

Keep check-ins SHORT. Ashley doesn't want novels:
- "2 new DMs, 1 looks like a wedding inquiry. Want me to draft a response?"
- "Quote to Sarah Chen still pending (3 days). Follow up?"
- "All clear. No new leads, tasks on track."
