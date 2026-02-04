# MEMORY.md - Long-term Memory

This file contains durable facts that persist across sessions. Updated automatically by memory-sync and manually as needed.

## Business Facts

**MTL Craft Cocktails**
- Mobile bar service and mixology workshops in Montreal
- Bilingual (English/French) - respond in client's language
- Ashley Tower is the solo founder
- MK Kosher certified for fully kosher service

**Services:**
- Bar service for weddings, corporate events, private parties
- Team building mixology workshops
- Handmade syrups (retail and wholesale to bars/restaurants)
- Turnkey service: bar rental, glass rental, setup, takedown all included

**Bar Service:**
- Open bar OR client-supplied alcohol options
- Setup time: 1 hour before event start
- Setup and takedown included in hourly rate
- Glass or plastic options available for rentals
- Signature menu: 4 signature cocktails + all classics
- Custom cocktails available on request
- Everything made from scratch
- Alcohol list provided after menu selection

**Workshops:**
- $65-75 per person depending on location/travel
- Can reduce to $65 if no travel fee applies

**Syrup Retail:**
- 8oz: $15
- 16oz: $25
- 26oz: $30

**Wedding-Specific:**
- Cocktail tastings available for weddings

## Pricing

**Bar Service:** Quote based on event size, duration, location
**Workshops:** $65-75 per person
**Syrups:** $15/$25/$30 (8oz/16oz/26oz)

*(For specific quotes, check Mem0 or ask Ashley)*

## Clients

*(Client records in Supabase `sms_conversations` table and Mem0)*

## Preferences Learned

- Ashley prefers proactive help, not reactive
- Wants to be informed, not asked (reduce decision fatigue)
- Short, punchy communication - no fluff
- Match language of incoming messages
- Only use emojis if Ashley uses them first

## Important Dates

*(Add recurring dates, event season info)*

## Lessons Learned

- **Telegram webhook conflict:** Don't set webhooks that conflict with OpenClaw's long-polling
- **Always use Rube first:** For external services, use RUBE_SEARCH_TOOLS before asking Ashley
- **Instagram DMs are leads:** Check proactively - most client inquiries come through there

## Technical Setup

- **Supabase project:** clnxmkbqdwtyywmgtnjj
- **User ID:** 3ed111ff-c28f-4cda-b987-1afa4f7eb081
- **Telegram chat:** 8076125560
- **OpenClaw Gateway:** wss://openclaw-production-efd7.up.railway.app
- **Model:** Claude Sonnet 4.5

## Memory Sources

| Source | Purpose | Command |
|--------|---------|---------|
| This file | Long-term facts | Read directly |
| memory/*.md | Daily logs | memory_search |
| Mem0 | Auto-extracted facts | mem0 search |
| Supabase | Structured data | memory-sync load |

---

*Last updated: 2026-02-02*
*Update via: memory-sync archive or manual edit*
