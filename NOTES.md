# Calendar Time: decisions and next steps

Live page: https://claude.ai/artifact/RBFSvFPhzKhjNqMdxM6wiW (source: `index.html`)

## Already built
- Reads all Google calendars (connector "Google Calendar": `list_calendars`, `list_events`), today + next 2 days, 9am–10pm.
- 10 min buffer around events, 30 min minimum open block.
- "Projects & Exams" calendar = HW deadlines (marker on the bar + label), never blocks time.
- Activities list lives in the page's db, collection `activities` (name, minutes, repeat once/daily/anytime, group "exercise", order).
- Activities with group "exercise" are suggested at most once per day in total (gym OR pool OR a class).

## Next: 24 Hour Fitness classes + travel
- Clubs (club number, address):
  - Balboa 00892, 7715 Balboa Ave, San Diego 92111
  - UTC 00888, 4425 La Jolla Village Dr, San Diego 92122
  - Miramar 00094, 9550 Miramar Rd, San Diego 92126
  - Pacific Beach 00065, 909 Garnet Ave, San Diego 92109 (no group classes listed as of Nov 2026)
- Schedule feed used by 24hourfitness.com's own class schedule page (unofficial, may change):
  `https://mobile.24hourfitness.com/api/class-schedule?clubNumber=<n>&startDate=YYYY-MM-DD&endDate=YYYY-MM-DD&trainingType=gx24`
  Club list: `https://api.24hourfitness.com/clubs`
- Include only `trainingType` GX24 (basic membership). Exclude:
  - Premium (Reformer24 LIVE) and all "Group Training" / Modus classes (cost extra)
  - Category "Active Aging" (SilverSneakers) and mobility classes
  - Aqua and Zumba (user's choice)
- 24 Hour Fitness classes count as exercise (one exercise per day).
- Page can't fetch external sites, so Claude fetches schedules and saves them into the page's db; refresh weekly.
- Trip math for a class: Uber pickup wait + ride there (traffic at that time) → class → shower → Uber pickup wait + ride back.
  - Start/return point: 9165 Pharmacy Dr, La Jolla.
  - Travel by Uber both ways.
  - Shower: needed after class; length and where (gym or home) not decided yet.
- Travel time connectors: Uber (price/time estimates, probably "now" only) and TomTom Maps or Mapbox (traffic-aware routing for later departure times). Add them to the page's `mcp` capability once connected.

## Later
- ClassPass cycling classes within 10 miles of 9450 Gilman Dr. ClassPass blocks automated access, so this needs the user's own browser (Claude in Chrome or the Claude desktop app) or pasted results.
