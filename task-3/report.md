# Project Report: AI-Powered Learning Assistant

## 🛠️ Tools & Technologies Used
- **Automation Engine:** n8n (Cloud)
- **Database:** Supabase (PostgreSQL)
- **AI Provider:** Google Gemini API (Model: `gemini-2.5-flash-lite`) — migrated from OpenAI.
- **Interface:** Telegram Bot API

---

## ❌ Challenges & What Didn't Work

1. **AI Pattern Bias (The "Always A" Trap):** During early testing, the Examiner agent failed to understand the concept of key randomization. It kept defaulting to option "A" as the correct answer for nearly all generated questions, creating a predictable and broken quiz experience.
   
2. **Cascading Workflow Breakages:** Building a complex loopy architecture in n8n proved highly interdependent. Constantly adding new features (like global stats or fallback logic) repeatedly broke previously working nodes. For example, introducing multi-branch topics (Latest vs. Random) caused database insert nodes to throw errors because they kept expecting data from unexecuted paths.

3. **API Quota Limitations:** The workflow initially relied on OpenAI, but tests were abruptly halted due to "Insufficient Quota" errors caused by OpenAI's strict prepaid billing policies and expired trial credits.

4. **Silent Node Freezes (The Empty Database Trap):** By default, n8n completely stops a workflow branch if a database query returns 0 rows. This caused the bot to go completely silent when looking up stats for new users, as no data existed yet.

---

## 🎯 Notable Decisions & Solutions

- **Strict Prompt Engineering:** Adjusted the Examiner's prompt instructions to explicitly force the randomization of the correct option across A, B, and C keys, eliminating the bias.
- **Dynamic Expression Routing:** Solved branching reference errors by replacing direct node paths with conditional logic using `.isExecuted` ternary expressions:
  `{{ $('Limit').isExecuted ? $('Limit').item.json.id : $('Limit1').item.json.id }}`
- **Migration to Gemini Lite:** Switched the AI backbone to Google Gemini 2.5 Flash Lite via Google AI Studio. This provided an incredibly fast, highly reliable, and generous Free Tier without strict quota walls.
- **Pre-Filtering Input Engine:** Integrated an upstream `If` node immediately after the Telegram trigger to cleanly separate button clicks (`callback_query`) from plain text messages. This prevented the fallback system from crashing when users clicked inline elements.
- **Always Output Data Configuration:** Enabled the "Always Output Data" setting in Supabase nodes to ensure empty query results seamlessly pass default `|| 0` values rather than killing the execution flow.

---

## 📈 Conclusion
The architecture is now fully production-ready, highly resilient, and completely modular. The assistant strictly satisfies all behavioral and structured requirements stated in the technical task.
