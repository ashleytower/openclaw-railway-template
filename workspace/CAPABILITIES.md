# Max Capabilities & Overnight Agent Work

## Current Architecture

```
Telegram → Railway Gateway → Mac Node (WebSocket)
                ↓
         Sub-agents (up to 8 concurrent)
                ↓
         Rube (500+ integrations via mcporter)
```

## What Max Can Do Now

### Via Rube (mcporter)
- **Memory**: Search/store facts in Mem0
- **Database**: Query Supabase (recipes, tasks, SMS history)
- **Communications**: Instagram DMs, Gmail, Calendar
- **Payments**: Stripe (with approval)
- **170+ more apps**: Search with `mcporter list rube`

### Via Mac Node
The Mac connects to Railway via WebSocket. Max can:
- Take screenshots
- Send notifications
- Access Mac-specific capabilities exposed by the node

### Via Sub-agents
Max can spawn up to 8 parallel workers using `sessions_spawn`:
```
sessions_spawn task="Research competitor pricing" label="research-1"
```
- Each runs in isolated session
- Results announce back to Telegram
- Cannot spawn nested sub-agents

## Overnight Coding Work: Options

### Option 1: Sub-agents on Railway (Works Now)
Max spawns coding sub-agents that run on Railway container:
- Read/Write/Edit/Bash tools available
- Limited to Railway's /data/workspace
- Good for: API work, data processing, documentation

### Option 2: Claude Code via Mac Node (Needs Setup)
For Max to run Claude Code on your Mac overnight:

1. **Create a skill** that wraps Claude Code CLI:
```bash
# ~/.openclaw/skills/claude-code/run.sh
claude --dangerously-skip-permissions "$@"
```

2. **Expose via Mac node** capabilities

3. **Max calls it**:
```bash
sessions_spawn task="Run claude-code skill: implement feature X in repo Y"
```

### Option 3: Ralph Loops via Cron (Best for Overnight)
Set up a cron job that triggers Claude Code with Ralph:

```json
// In openclaw.json cron section
{
  "schedule": "0 2 * * *",  // 2 AM daily
  "task": "Run overnight coding: ralph-loop on max-ai-employee repo"
}
```

This would:
1. Fire at 2 AM
2. Max spawns sub-agent with coding task
3. Sub-agent uses Claude Code skill on Mac
4. Results ready by morning

## What's Missing for Overnight Coding

1. **Claude Code skill**: Need to create skill that wraps `claude` CLI
2. **Mac node tool exposure**: Need to expose the skill to Max
3. **Task queue**: Way for Max to queue overnight work
4. **Results notification**: Morning summary of what was done

## Recommended Next Steps

1. Test Max with mcporter (verify memory lookups work)
2. Create `claude-code` skill on Mac
3. Test sub-agent spawning: `sessions_spawn task="test task"`
4. Set up overnight cron if sub-agents work

## Commands to Test

```bash
# Check Max's current skills
# (via Telegram): "What skills do you have?"

# Test memory lookup
# (via Telegram): "What's Emma's Garden recipe?"

# Test sub-agent spawn
# (via Telegram): "Spawn a sub-agent to check today's calendar"
```
