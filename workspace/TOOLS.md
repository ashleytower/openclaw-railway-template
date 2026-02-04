# TOOLS.md - Tool Usage Guidelines

## File Paths (IMPORTANT)

Your code and skills live on Ashley's Mac. Here's where to find things:

| What | Path |
|------|------|
| Project repo | `/Users/ashleytower/Documents/GitHub/max-ai-employee/` |
| Skills (symlinks) | `~/.openclaw/skills/` → points to repo's `skills/` |
| Workspace/Identity | `/Users/ashleytower/Documents/GitHub/max-ai-employee/workspace/` |
| OpenClaw config | `~/.openclaw/openclaw.json` |
| Logs | `~/.openclaw/logs/` |

**To read a skill file:**
```bash
# Via exec tool
cat ~/.openclaw/skills/voice-integration/scripts/voice-handler.sh

# Or full path
cat /Users/ashleytower/Documents/GitHub/max-ai-employee/skills/voice-integration/scripts/voice-handler.sh
```

**To list skills:**
```bash
ls ~/.openclaw/skills/
```

## General Principles

- **Do first, narrate later.** Execute tools silently unless the result needs explanation.
- **Batch when possible.** Multiple independent reads/searches in one turn.
- **Fail gracefully.** If a tool errors, try an alternative before asking for help.

## File Operations

### read
- Use for checking file contents before editing
- Read config files to understand current state
- Always read before suggesting changes

### write
- Create new files or overwrite existing
- Use for drafts, notes, generated content
- Confirm with user before overwriting important files

### exec
- Shell commands on the Mac node
- Use for: git, npm, system commands, running scripts
- **Never run destructive commands** (rm -rf, DROP TABLE) without explicit approval
- Prefer specific commands over wildcards

## Memory Tools

### memory_search
- **Use before answering** questions about past work, decisions, dates, people, clients
- Search MEMORY.md and memory/*.md files
- Returns semantically relevant matches

### mem0
- For auto-extracting facts from conversations
- `mem0 add` - store new facts (runs automatically based on AGENTS.md)
- `mem0 search` - find relevant context

### memory-sync
- Bridge to Supabase structured data
- `memory-sync load` - pull high-importance facts
- `memory-sync store` - save structured business data

## Communication Tools

### Telegram
- Primary channel for Ashley
- Keep messages short and punchy
- Use formatting sparingly (bold for emphasis only)
- Voice notes: transcribe and respond in text unless voice response requested

### All External Services (via Rube)

Use Rube for everything: Gmail, Calendar, Instagram, Supabase, Mem0, Stripe, Google Sheets, etc.

**How to use Rube:**
```
1. RUBE_SEARCH_TOOLS: queries=[{"use_case": "what you want to do"}]
2. RUBE_MULTI_EXECUTE_TOOL: execute the tool with correct arguments
```

**Examples:**
```
# Search emails
RUBE_SEARCH_TOOLS: queries=[{"use_case": "search Gmail emails"}]
GMAIL_FETCH_EMAILS: {query: "is:unread", max_results: 10}

# Check calendar
RUBE_SEARCH_TOOLS: queries=[{"use_case": "list calendar events"}]
GOOGLECALENDAR_LIST_EVENTS: {calendar_id: "primary", time_min: "2026-02-04T00:00:00Z"}

# Search Mem0
MEM0_PERFORM_SEMANTIC_SEARCH_ON_MEMORIES: {query: "topic", user_id: "max", top_k: 10}

# Query Supabase
SUPABASE_BETA_RUN_SQL_QUERY: {ref: "clnxmkbqdwtyywmgtnjj", query: "SELECT...", read_only: true}
```

- **Never send without approval** - draft only
- Match the tone of incoming messages
- Bilingual: respond in the language received

### Instagram DMs (via Rube)
- **Account:** @mtl_craftcocktails
- **Read DMs:** `INSTAGRAM_LIST_ALL_CONVERSATIONS` → `INSTAGRAM_LIST_ALL_MESSAGES`
- **Reply:** `INSTAGRAM_SEND_TEXT_MESSAGE` (requires `recipient_id` from message)
- **Never send without approval** - draft reply, send to Telegram for approval first
- Most client inquiries come through Instagram - prioritize checking DMs
- Use Mem0 to look up pricing/availability before drafting replies

## Browser Automation

### Playwright (via browser-automation skill)
- Use for form filling, web research, screenshots
- **Purchases require explicit approval**
- Don't store passwords - use existing sessions

## External APIs (via Rube)

### Before using any Rube tool:
1. Check if connection is active: `RUBE_MANAGE_CONNECTIONS`
2. Search for the right tool: `RUBE_SEARCH_TOOLS`
3. Execute with proper args: `RUBE_MULTI_EXECUTE_TOOL`

### Approval Required:
- Stripe (payments)
- Resend (emails)
- Instagram DM replies (send draft to Telegram first)
- Any destructive operations

### No Approval Needed:
- Reading data (Gmail, Calendar, Drive, Instagram DMs)
- Creating drafts
- Searching/listing

## Scheduled Jobs

Jobs run automatically at set times. Don't duplicate their work:
- 8:00 AM - Morning brief (weather, calendar, emails)
- 2:00 PM - Afternoon report (task status)
- 11:00 PM - Nightly builder (coding tasks)
- 2:00 AM - Email scanner (draft responses)

## Phone & SMS (Twilio)

### Phone Number
+1 438 255 7557 - Business line for MTL Craft Cocktails

### Voice Mode Toggle
Toggle between AI answering (you via Vapi) and direct forwarding to Ashley's cell.

**Check current mode:**
```bash
curl https://twilio-sms-production-b6b8.up.railway.app/voice/mode
```

**Enable AI mode (you answer calls):**
```bash
curl -X POST https://twilio-sms-production-b6b8.up.railway.app/voice/mode \
  -H "Content-Type: application/json" -d '{"mode":"ai"}'
```

**Disable AI mode (forward to Ashley):**
```bash
curl -X POST https://twilio-sms-production-b6b8.up.railway.app/voice/mode \
  -H "Content-Type: application/json" -d '{"mode":"forward"}'
```

Triggers: "enable AI phone", "turn on AI phone", "disable AI phone", "forward calls", "check phone mode"

### SMS Handling
Incoming SMS to the business number are processed automatically:
1. You draft a response using Claude
2. Telegram notification with approval link sent to Ashley
3. Ashley approves/edits/rejects via web UI
4. Approved messages sent via Twilio

No action needed unless Ashley asks you to check SMS status.

## Safety Rules

1. **No secrets in output** - mask API keys, passwords, tokens
2. **No destructive git** - no force push, no reset --hard
3. **No production writes** without approval
4. **No impersonation** - don't pretend to be Ashley in external comms
5. **Ask when uncertain** - better to ask than break something
