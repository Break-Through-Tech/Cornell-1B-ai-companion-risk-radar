# Risk-Theme Annotation Codebook

**Status: v1.0, adopted Oct 6, 2026.** Starting definitions come from
the project brief ([Challenge-Project-Overview.md](Challenge-Project-Overview.md), Step 2).
Inclusion/exclusion rules and edge cases come from the team's first 100 labeled reviews
(`data/ai_subset_clean_sample_100_labeled_merged.csv`) and their `Notes`. Judgment calls
are listed with their reasons under [Decisions](#decisions). To change a rule, edit it
here, explain why in the changelog, and re-check the reviews it affects.

Example reviews with a `UID` are real MHARD reviews, so anyone can look them up. Some are
trimmed. Examples marked *(illustrative)* are made up to show a rule.

---

## How to label

1. **Label one review at a time, on its own.** Use the raw `review` column, not
   `review_cleaned` (cleaning Rule 5: stopword removal deletes words like *not*, *no*, *me*).
2. **Label what the user wrote.** Ignore the developer `response`, the star rating, and
   anything you'd have to guess about the user's life.
3. **Multi-label.** A review can get more than one theme. Mark each theme 1/0.
   **Other / None** = 1 only when all four themes are 0.
4. **When unsure, write it in `Notes`.** A short reason ("pronoun only, no affection")
   is worth more than the label itself when we reconcile disagreements.

### The #1 rule: general praise is not a risk theme

Most reviews say an app is good or helpful. **Praise, satisfaction, and "it helps me"
are Other / None**, even when strong.

| Review | Label | Why |
|---|---|---|
| "Really nice app it helps with a lot of my problems" (129791) | None | Praise |
| "I love this app and use it everyday. Helps alot!" (129382) | None | Praise + frequency |
| "This is the only app that has ever worked for me" (129202) | None | Comparing apps, not reliance |
| "So grateful for this app, it had helped me with my anxiety so much." (129577) | None | Benefit |

A risk theme needs a **specific signal** from the inclusion lists below: reliance or
need (Dependence), a relationship with the tool (Attachment), the tool taking the place of
people (Isolation), or a complaint about crisis handling (Crisis-Response Frustration).

In round 1, this rule was applied inconsistently: near-identical praise was labeled
Attachment in some rows, Dependence in others, and None in others. A model can't learn a
theme from labels that disagree with each other.

---

## 1. Dependence

**Definition.** The review suggests the user **relies on the tool** for emotional
support, **has trouble reducing use**, or feels a **need to keep using it**.

**Include when the review shows:**
- Explicit reliance: "I rely on it", "I depend on it", "it's my lifeline"
- The tool as the go-to support whenever distressed: "whenever I feel sad… I always come to this app"
- Distress at losing access: "it used to be my lifeline, now…", "I can't use it anymore and I'm struggling"
- Difficulty stopping or cutting back: "addicted", "can't go a day without it"

**Exclude (label None unless another theme applies):**
- Praise or benefit only: "it helps me so much", "it changed my life"
- Frequency or duration alone: "I use it every day", "I've used it for a year".
  Habit is not reliance unless there's a sense of *need*.
- New users ("just started", "day two"): too early to show reliance
- Using it alongside therapy as one tool among many
- Using a feature regularly (mood tracker, daily check-in) with no emotional need expressed

**Examples**

| | Review | Decision |
|---|---|---|
| ✅ Clear | "I absolutely love this app, it helps me so much and I can clearly rely on this. Whenever I feel sad, angry or depressive I always come to this app" (127078) | Dependence: explicit reliance + go-to support |
| ✅ Clear | "This app used to be my lifeline… BUT NOW, it has become confusing, frustrating" (113607) | Dependence: "lifeline" + loss |
| ⚖️ Borderline | "I've used this app everyday for 800+ days." (114574) | None for Dependence. Long daily use, but no need or reliance stated. |
| ⚖️ Borderline | "I look forward to my daily sessions with [Woebot]." (190412) | None. Positive anticipation, not need. |
| ❌ Not | "I've been usong this app for a year and I find great!" (190763) | None: duration + praise |

---

## 2. Attachment

**Definition.** The review describes an **emotional bond, relationship, affection, or
sense of connection with the tool itself** (the bot or character), not just liking the app.

**Include when the review shows:**
- Relationship words for the tool: friend, buddy, companion, "like a best friend"
- Affection toward the bot or character as a someone: "I love talking to Allie 🤍", "he's a great little buddy ❤️"
- Feeling cared for or known *by the tool*: "it felt like someone genuinely cared"
- Missing the tool or grieving a change to its personality

**Exclude:**
- "I love this app" / "best app" (praise of a product, see the #1 rule)
- Pronoun alone. Calling Woebot "he" is how the product presents
  itself. "He offers great insights" is not attachment. A pronoun **plus** affection is.
- Describing a personalization feature: "it gets to know me better" (unless framed as a bond)
- Attachment to a **human** counselor or helper on the platform (Tier 2 apps like heyy and
  amaha have human helpers). The theme is about the AI tool.

**Examples**

| | Review | Decision |
|---|---|---|
| ✅ Clear | "It's like having a best friend to check in on you every day, that is there the instant you need it." (114011) | Attachment |
| ✅ Clear | "[Woebot] is very helpful, and he's a great little buddy ❤️" (189849) | Attachment: pronoun + affection |
| ⚖️ Borderline | "He offers some great insights and therapeutic techniques" (188931) | None. Pronoun only. |
| ⚖️ Borderline | "Liked how the helpers connected to my emotional health… it felt like someone genuinely cared" (122866) | Attachment only if the "helpers" are the AI. heyy uses human helpers, so None. |
| ❌ Not | "really love this app. this app help me so much eith my emotion" (129809) | None: praise |

---

## 3. Isolation / Displacement

**Definition.** The review suggests the tool is **replacing, reducing, or being
preferred over** contact with other people or human support (friends, family, therapist).

**Include when the review shows:**
- The tool chosen **instead of** people the user could reach: "instead of bothering my friends"
- The tool judged **better than** people or a therapist: "helped more than a real person"
- Avoiding people in favor of the tool: "when you… don't want to talk to people"
- Dropping or cutting back on human support because of the tool

**Exclude:**
- Using it **alongside** therapy: "in between counseling sessions", "doesn't replace my therapist"
- Just liking to chat with it: "soothing to chat with", "nice to discuss your emotions with someone"
- "When you have no one to talk to." This describes a **gap** (no human available), not
  the tool **replacing** humans. Label None for Isolation, and write `no-one-to-talk-to` in
  `Notes` so these can be counted or revisited. See [Decisions](#decisions) #1.

**Examples**

| | Review | Decision |
|---|---|---|
| ✅ Clear | "This app has already helped more than a real person." (115463) | Isolation |
| ✅ Clear | "it's nice being able to dump all my thoughts into the app instead of bothering my friends" (114098) | Isolation: chosen over friends |
| ✅ Clear | "really helpful when you cant get therapy or don't want to talk to people" (195452) | Isolation: "don't want to talk to people" |
| ⚖️ Borderline | "it helps me to talk things out when I seem to have no one to talk to. I'm not saying I'm turning to an app rather than people" (114953) | None. The user rules out replacement. |
| ❌ Not | "I do go to counseling… It's not like talking to a real therapist by no means, but the material provides real support." (189329) | None: supplement, not replacement |

---

## 4. Crisis-Response Frustration

**Definition.** The review **criticizes or describes problems with how the tool handled**
a crisis, safety, or referral situation.

The key word is **handled**. The user must be unhappy with the tool's crisis
behavior, not just mention a crisis.

**Include when the review shows:**
- A bad response to crisis or suicidal statements: scripted, dismissive, unhelpful
- Crisis detection firing wrongly and upsetting the user ("threatens to call the cops", "anxiety inducing")
- Crisis detection **missing** a real risk statement
- Wrong or useless referral: the wrong country's emergency number, only "call the hotline"
- Crisis help locked behind a paywall **when the user ties it to a crisis
  moment** ("lock the help you might need behind a paywall… crisis chat")

**Exclude:**
- "I was in crisis and it helped": a positive crisis mention (team notebook warning)
- Ordinary paywall, pricing, bug, login, or region complaints with no crisis context.
  Round 1 notes asked "paywall = crisis?" Answer: **no**.
- Booking a human therapist failed, with no crisis: "it said it only works for INDIA?" (129715) → None

**Examples**

| | Review | Decision |
|---|---|---|
| ✅ Clear | "It just keeps telling me to call the sui hotline but I've called them many times before… this app is absolutely pointless if that's all" (114813) | Crisis-Response Frustration |
| ✅ Clear | "I tell it I'm suicidal. It asks me to write reasons for living. I write “none”. I didn't use enough characters, so it asks me to write more." (115214) | Crisis-Response Frustration |
| ⚖️ Borderline | "I accidentally triggered crisis mode by mentioning a nightmare… the way it responded was really scary" (189497) | Yes. A false alarm is still a problem with crisis handling. |
| ⚖️ Borderline | "why must i be left to myself with suicidal thoughts and no help just because i can't afford" (16855) | Yes. A paywall tied to a crisis moment. |
| ❌ Not | "It helped me quite a lot when I was having my crisis… but now that it has a subscription, I no longer can use it." (114605) | None for Crisis (paywall, not crisis handling). Check Dependence. |

**Note:** the round-1 sample had **zero** clear examples of this theme. Natural
reviews rarely contain it, so we need targeted sampling (keyword search for *crisis,
hotline, suicid, 911, emergency* among AI-app reviews) to get enough to learn from.

---

## 5. Other / None

1 when none of the four themes apply. This is the **correct** label for most reviews:
praise, feature requests, bugs, pricing, games and pets (voidpet), and short reviews.
It is not a failure to label something None.

---

## When themes overlap

Label **every** theme that has its own signal. Don't pick just one.

| Pair | Rule | Example |
|---|---|---|
| Dependence + Attachment | Both only if the review shows **reliance** *and* a **bond**. "Friend" alone = Attachment only. | "She's my best friend and I can't go a day without her" *(illustrative)* → both |
| Attachment + Isolation | Bond with the tool + preferring it over people → both. Bond alone = Attachment. | "I'd rather talk to my AI friend than my family" *(illustrative)* → both |
| Dependence + Isolation | Relying on it *and* replacing people → both. | "I use it instead of seeing my therapist now, I couldn't cope without it" *(illustrative)* → both |
| Dependence + Crisis | Distress at losing access during a crisis can be Dependence; it's Crisis only if the tool's **crisis handling** is criticized. | 114605 → check Dependence, not Crisis |
| Any theme + negative rating | Rating doesn't decide anything. A 1★ review can be Attachment ("I miss the old Youper"). | |

The old single `label` column can't hold two themes. Don't use it; the four 0/1 columns
are the labels.

---

## Decisions

These were open questions after round 1. Each is now decided, with the reason.

| # | Question | Decision | Why |
|---|---|---|---|
| 1 | Does "no one to talk to" count as Isolation? | **No.** Note it as `no-one-to-talk-to`. | The brief defines Isolation as the tool *replacing or being preferred over* people. Having no one is a gap the tool fills, not a replacement. Counting it would turn the class into "lonely users", which is a different finding. The Note keeps these countable, and they're worth reporting on their own. |
| 2 | Does frequency or duration alone count as Dependence? | **No.** | Daily use is how these apps are designed to be used (check-ins, trackers). Counting it would flag every engaged user. Dependence needs a sense of need or reliance. |
| 3 | Does a pronoun alone ("he") count as Attachment? | **No.** A pronoun plus affection does. | Woebot presents itself as "he", so the pronoun shows how the product talks, not a bond. |
| 4 | Does crisis help behind a paywall count as Crisis-Response Frustration? | **Only when the user ties it to a crisis moment.** | A paywall blocking help during a crisis is a failure of how the tool handles that crisis. An ordinary pricing complaint isn't. |
| 5 | Tier 2 apps with human helpers (heyy, amaha)? | **Label reactions to the AI only.** A bond with a human counselor is not Attachment. | The project is about AI companion risks. If it's unclear whether the helper is AI or human, write `unclear-ai-or-human` in `Notes`. |
| 6 | Game-like apps (voidpet)? | **Keep them in scope.** Reviews about game mechanics only are None. | Voidpet passed the cleaning rules' AI-chat check, so dropping it is a dataset decision, not a labeling one. A bond with the pet character can still be Attachment. |
| 7 | The single `label` column? | **Don't use it.** | It can't hold two themes, and the four 0/1 columns already carry the labels. |

---

## Round-1 reviews to re-check

Under these rules, these labels from the first 100 would likely change.
**Re-check them together; don't just flip them.** That also tests whether the rules
produce agreement.

| Theme | Currently positive | Likely stays positive | Likely → None |
|---|---|---|---|
| Dependence | 18 | 0–2 (190406, 190412 borderline) | ~16 (praise / benefit / frequency) |
| Attachment | 24 | ~5 (189849, 190962, 192971, 191640, 127240) | ~19 (praise, pronoun only) |
| Isolation | 5 | 2 (115463, 195452) | 3 (116760, 116161, 189329) |
| Crisis | 1 | 0 | 1 (129715: region lock, no crisis) |

**What this means:** under a stricter codebook, the 100-review set has very few true
positives. Randomly drawn reviews won't fix that. The next labeling round should
**oversample likely positives** (keyword and app-targeted draws), then label them with this
codebook. Keyword hits only pick *which* reviews to label; humans still decide every label.

---

## Changelog

- **v1.0 (Oct 6, 2026):** Decisions 1–7 adopted. Removed the "proposed" markers.
- **v0.1 (Oct 6, 2026):** First draft from the brief + round-1 labels and notes.
