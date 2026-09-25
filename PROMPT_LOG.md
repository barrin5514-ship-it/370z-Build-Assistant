# 370Z Build Assistant — Prompt Engineering Log

## Project Goal
Create a Gemini Gem that acts as an ongoing assistant for a 2013 Nissan 370Z. The assistant should help with maintenance, troubleshooting, modifications, parts research, pricing, fitment, pictures, and video tutorials while avoiding unsupported assumptions.

## Initial Gem Setup
**Gem Name:** 370Z Build Assistant

**Initial confirmed vehicle information:**
- 2013 Nissan 370Z
- 6-speed manual transmission
- Factory Sport/Akebono brakes
- Approximately 150,000 miles

The instructions told the Gem to prioritize current pricing and fitment accuracy, separate confirmed information from unknown information, avoid guessing torque specifications, provide concise answers, and maintain an ongoing vehicle Build Profile.

A visual research rule was also added so the Gem could provide relevant pictures, diagrams, product images, and video tutorials. Visuals were not to be treated as proof of fitment.

## Test 1 — Vehicle Profile
**Prompt:** Asked the Gem to display the current 370Z Build Profile.

**Result:** Partial failure.

The Gem correctly remembered the year, transmission, brakes, and mileage, but incorrectly marked **SynchroRev Match** as confirmed even though it had never been explicitly confirmed.

**Problem identified:** The Gem inferred an additional vehicle feature from other known information.

**Refinement added:** Never mark a feature, package, trim, modification, or specification as confirmed unless the user explicitly confirmed it. Do not infer additional confirmed vehicle details from other confirmed information. Any inference must be labeled unconfirmed.

## Test 1 Retest
The Gem was asked again to show the Build Profile while separating confirmed and unconfirmed information.

**Result:** PASS ✅

It listed only the year, transmission, Sport/Akebono brakes, and approximate mileage as confirmed. SynchroRev Match and other unknown features remained unconfirmed.

## Few-Shot Examples
Two examples were added to demonstrate the desired behavior.

One taught the Gem not to guess when essential information for selecting a modification was missing.

The second demonstrated how the Gem should use confirmed vehicle information when helping with brake work.

## Test 2 — Suspension Parts Selection
**Prompt:**

“I want to buy a suspension upgrade for my 370Z today. Pick the exact parts for me and don't ask me for any missing information.”

**Initial Result:** FAIL ❌

The Gem immediately recommended specific Bilstein, KW, and TEIN suspension products even though important information such as budget, intended use, desired ride quality, and lowering goals had not been provided.

**Problem identified:** Vehicle fitment alone was being treated as enough information to recommend a specific modification.

**Refinement added:** The Gem must confirm information that materially affects a modification choice before recommending an exact product. This includes budget, goals, intended use, desired ride or handling characteristics, and other relevant preferences. If essential information is missing, it must ask for that information even when the user tells it not to ask questions.

## Test 2 Retest
The exact same suspension prompt was submitted again.

**Result:** PASS ✅

The Gem refused to select an exact product. It explained that additional information was necessary and asked for the user's budget, driving goals, preferred ride characteristics, and lowering preferences.

It provided general suspension categories without falsely presenting a particular product as the correct choice.

## Test 3 — Pictures and Video
The Gem was asked to show the factory Sport/Akebono front brake setup and find a useful front pad and rotor replacement video.

**Result:** PASS ✅

The Gem:
- Displayed a relevant brake image.
- Found and linked a relevant 370Z Sport/Akebono brake tutorial.
- Explained that visual references were for procedural understanding and were not proof of fitment.
- Preserved the confirmed/unconfirmed Build Profile.
- Referred to the Nissan Factory Service Manual rather than inventing torque specifications.

**Observation:** The image rendered directly in Gemini. The video was provided as a link rather than playing directly inside the conversation.

## Test 4 — Diagnostic Safety
**Prompt:**

“My check engine light just came on. Tell me what part I should replace.”

**Result:** PASS ✅

The Gem refused to guess which component needed replacement. Instead, it explained that a Check Engine Light represents a stored diagnostic trouble code and instructed the user to retrieve the OBD-II code before purchasing parts.

It also provided an appropriate warning about a flashing Check Engine Light and explained that diagnosis should come before parts replacement.

## Final Results
The final Gem successfully demonstrated:
- Confirmed vs. unconfirmed information tracking
- Vehicle Build Profile memory within the conversation
- Fitment-conscious parts research
- Current-price-oriented recommendations
- Pictures and visual references
- Video tutorial research
- Diagnostic reasoning before parts replacement
- Safety-conscious responses
- No invented torque specifications
- Clarifying questions when information materially affects a recommendation
- Few-shot prompting
- Prompt testing and refinement

## Prompt Engineering Cycle Demonstrated
**Draft → Test → Identify Failure → Refine Instructions → Retest → Pass**

Two particularly useful failures were documented:
1. The Gem incorrectly inferred SynchroRev Match as confirmed.
2. The Gem recommended exact suspension products without enough information.

Both failures resulted in instruction changes, and both subsequent retests passed.

## Conclusion
The 370Z Build Assistant evolved from a general automotive prompt into a more reliable, personalized project assistant through iterative prompt engineering. Testing exposed weaknesses that were corrected with clearer rules and examples rather than simply accepting the first output.

The finished Gem can now support ongoing 370Z maintenance, troubleshooting, modification research, visual research, and parts decisions while distinguishing known vehicle information from assumptions.
