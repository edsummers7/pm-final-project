# Feature Roadmap, Module 4 · StreamLine Spotlight

**Team:** 2 engineers + 1 designer

## Strategic anchors
- **Persona:** The Wanderer
- **Primary metric:** Month 1 retention of Spotlight-exposed Wanderers, compared with a non-exposed holdout. Proposed target: +10 points. The Full Library Nov cohort is at 63%, and the Spotlight cohorts reached 74 to 79%.
- **Moment of misery:** Someone who can't find what they want in a cluttered library goes to Google or a competitor to find it and never comes back. The loss happens in the first weeks, before they've built a habit.
- **Guardrail:** Power User sessions per week (currently 4.8) and their low churn. The 22% of users with the highest LTV must not be pushed into a curated experience that makes their library harder to use. As a second guardrail, average session length must not fall below 24 minutes.

## Scoring
| Feature | Value | Effort | Quadrant | Decision | Rationale |
|---|---|---|---|---|---|
| A1 Spotlight Curated Rail | 5 | 2 | Quick Win | Now | It attacks the moment of misery head-on: the Wanderer sees something good before leaving for Google. It's the mechanism behind the 74-79% Spotlight cohorts and needs no model. |
| A2 'Why You'll Love This' Label | 4 | 3 | Major Project | Later | Hover doesn't exist on mobile or TV, and it needs taste data the Wanderer doesn't have yet. LLM copy also needs quality control and caching. |
| A3 Hidden Gem Badge | 4 | 2 | Quick Win | Now | It can be rule-based on existing quality and viewcount data. It gives the Wanderer a reason to trust an unfamiliar title and surfaces unused niche content. |
| A4 Mood-Based Entry Point | 2 | 3 | Time Sinker | Cut | It adds a gate at login for someone who doesn't know what they want. It also filters the rail, which risks Power User sessions and the 24-minute session guardrail. Cut it. |
| A5 Personalized Spotlight Queue | 4 | 5 | Major Project | Next | It's high value, but a new Wanderer has thin taste data in the first weeks, which is exactly when the loss happens. It also needs a model and cold-start handling, so it won't fit this sprint. |
| A6 Spotlight Digest Email | 3 | 3 | Time Sinker | Later | It can win back lapsed Wanderers, but the misery happens in-product, and good personalization depends on A5. A later version could reuse A1's picks. |
| A7 Curator Profiles | 2 | 4 | Time Sinker | Cut | The Wanderer doesn't know whom to follow. It needs editorial staffing, a follow graph and profile design before it pays off. |
| A8 Watch Party (Spotlight) | 1 | 5 | Time Sinker | Cut | It's a social feature that does nothing for library clutter, and it needs sync and chat infrastructure. A Sales-style wish-list item. |
| A9 Advanced Filter Engine | 2 | 4 | Time Sinker | Cut | Filters serve people who already know what they're looking for, which is the Power User. The Wanderer browses. It also depends on clean decade, language and runtime metadata |
| A10 Offline Download (Spotlight) | 1 | 5 | Time Sinker | Cut | It has nothing to do with discovery, and it brings DRM, storage and licensing work. |

## Roadmap
### NOW, 3-week sprint
- **A1 Spotlight Curated Rail**, It attacks the moment of misery head-on: the Wanderer sees something good before leaving for Google. It's the mechanism behind the 74-79% Spotlight cohorts and needs no model.
- **A3 Hidden Gem Badge**, It can be rule-based on existing quality and viewcount data. It gives the Wanderer a reason to trust an unfamiliar title and surfaces unused niche content.

### NEXT, following 1-2 sprints
- **A5 Personalized Spotlight Queue**, It's high value, but a new Wanderer has thin taste data in the first weeks, which is exactly when the loss happens. It also needs a model and cold-start handling, so it won't fit this sprint.

### LATER, backlog
- **A2 'Why You'll Love This' Label**, Hover doesn't exist on mobile or TV, and it needs taste data the Wanderer doesn't have yet. LLM copy also needs quality control and caching.
- **A6 Spotlight Digest Email**, It can win back lapsed Wanderers, but the misery happens in-product, and good personalization depends on A5. A later version could reuse A1's picks.

### ✂ Cut List
- **A4 Mood-Based Entry Point**, It adds a gate at login for someone who doesn't know what they want. It also filters the rail, which risks Power User sessions and the 24-minute session guardrail. Cut it.
- **A7 Curator Profiles**, The Wanderer doesn't know whom to follow. It needs editorial staffing, a follow graph and profile design before it pays off.
- **A8 Watch Party (Spotlight)**, It's a social feature that does nothing for library clutter, and it needs sync and chat infrastructure. A Sales-style wish-list item.
- **A9 Advanced Filter Engine**, Filters serve people who already know what they're looking for, which is the Power User. The Wanderer browses. It also depends on clean decade, language and runtime metadata
- **A10 Offline Download (Spotlight)**, It has nothing to do with discovery, and it brings DRM, storage and licensing work.
