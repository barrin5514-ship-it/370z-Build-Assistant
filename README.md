# 370Z Build Assistant

Google Gemini custom Gem for an ongoing 2013 Nissan 370Z project.

## Confirmed Vehicle Profile
- 2013 Nissan 370Z
- 6-speed manual transmission
- Factory Sport/Akebono brakes
- Approximately 150,000 miles

## Purpose
The assistant supports maintenance, troubleshooting, modifications, compatible-parts research, current pricing, pictures, diagrams, and video tutorials while keeping confirmed vehicle facts separate from assumptions.

## Core Behaviors
- Maintain an ongoing Build Profile.
- Separate confirmed information from unknown or inferred information.
- Verify fitment before recommending specific parts.
- Ask for missing information when it materially affects a recommendation.
- Prioritize value and daily-driver reliability unless higher performance is requested.
- Provide useful pictures, diagrams, product images, and video tutorials when relevant.
- Never treat pictures or videos as proof of fitment.
- Diagnose problems before recommending replacement parts.
- Never invent torque specifications; use the Nissan Factory Service Manual for unverified safety-critical specifications.

## Prompt Engineering Approach
**Draft → Test → Evaluate → Refine → Retest**

Testing exposed two important failures that were corrected:
1. SynchroRev Match was incorrectly inferred as confirmed.
2. Exact suspension products were recommended before budget, goals, ride preference, and lowering preference were known.

Both behaviors passed after targeted instruction refinements and retesting.

See `PROMPT_LOG.md` for the test history and `GEM_INSTRUCTIONS.md` for the final assistant behavior specification.
