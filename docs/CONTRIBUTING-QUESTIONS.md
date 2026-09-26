# Questions for the project owner

Prepared by a prospective contributor after cloning and running the scaffold locally (2026-09-26). The repo currently contains the Replit workspace template with no product code, schema, or README, so these questions are needed before any feature work can start.

Answer inline. Short answers are fine. "Don't know yet" is a valid answer.

## A. Vision

1. In one sentence: what does a user do with this app, and what do they get out of it?
2. Who is the first user? Individual, community group, business, municipality, NGO?
3. What already exists outside this repo (Replit prototype, Figma, Notion, pitch deck, prior repo)? Links welcome.
4. Is "earth token / accounting / gamification" three features or one product? Which comes first?

## B. Earth token

5. What is one earth token a unit of? Action, impact, currency, reputation?
6. How is a token created? Earned by users, issued by admins, minted on-chain, purchased?
7. Can tokens be spent, transferred, redeemed, or burned? For what?
8. Is there any blockchain or crypto intent, now or later? If yes, which chain and custodial or not. If no, please say so explicitly so we don't design for it.
9. Does a token have a fiat or carbon equivalence (1 token = X kg CO2e or $Y)? Who sets the rate?

## C. Accounting

10. Does "accounting" mean a double-entry ledger of token movements, carbon/impact accounting, or financial bookkeeping for organizations?
11. Do balances need an immutable audit trail (append-only journal), or is a mutable balance column acceptable for v1?
12. Are organizations first-class? Do orgs own accounts, or only individuals? Can one user belong to many orgs?
13. Reporting needs: statements, CSV/PDF export, monthly or yearly periods?

## D. Gamification

14. What actions earn tokens? Five to ten concrete examples.
15. Who verifies an action happened? Self-report, peer, admin, sensor/API, photo evidence?
16. Which mechanics do you want, ranked: points, levels, badges, streaks, leaderboards, challenges, teams?
17. Anti-abuse: daily caps, cooldowns, fraud review?
18. Is competition local (neighborhood or city leaderboards) or global?

## E. Acting locally

19. Is location a first-class concept? At what granularity: GPS point, postal code, city, region?
20. Are there local hubs, chapters, or organizers? Who creates them?
21. Location privacy expectation: exact, fuzzed, opt-in?

## F. Reword search and vetted information

22. What is "reword search"? Query rewriting, synonym expansion, LLM-assisted search, plain-language to technical?
23. What is being searched: actions, articles, datasets, local resources, other users?
24. Where does "vetted earth information" come from? Curated by admins, imported from named sources, user-submitted then reviewed?
25. What does "evidence based" mean in practice: citations required per item, source rating, peer-review workflow?
26. Is an LLM in scope for search or summaries? If yes, which provider, and is there a budget?

## G. Realtime

27. What must be realtime? Leaderboard updates, notifications, live challenges, chat, map presence?
28. Acceptable latency: seconds via polling, or true push (WebSocket/SSE)?

## H. Users, auth, roles

29. Auth method: email/password, magic link, OAuth (Google/Apple), Replit Auth, wallet?
30. Roles: user, organizer, verifier, admin? Others?
31. Any minors (schools, youth programs)? This changes data handling.

## I. Clients and platforms

32. React is pinned to 19.1.0 "because expo requires it." Is a mobile app (Expo) planned? Timeline?
33. Web first, mobile first, or both from day one?
34. Is `artifacts/mockup-sandbox` a throwaway preview server or the seed of the web client?

## J. Infrastructure

35. Staying on Replit autoscale deploy, or moving (Vercel, Fly, Cloudflare, Railway)?
36. Database hosting: Replit-hosted Postgres, Neon, Supabase, other? Shared dev DB or each developer local?
37. Where are secrets and env managed? Can you share a `.env.example`?
38. The darwin binary overrides in `pnpm-workspace.yaml` break `mockup-sandbox` on macOS. Are they intentional beyond Replit? OK to PR a fix?

## K. Data, compliance, accessibility

39. Any PII beyond email and location? Data retention rules?
40. Jurisdictions in scope (GDPR, CCPA, other)?
41. OK to hold UI to WCAG 2.1 AA?
42. Any content moderation needs for user-submitted evidence or text?

## L. Contribution process

43. Branch model: PRs to `main`? Is it protected? Who reviews and merges?
44. OK to use Conventional Commits?
45. Issue tracker: GitHub Issues, Linear, Notion, other? Can contributors open issues?
46. Would you accept these as first PRs: README, CI typecheck workflow, CONTRIBUTING.md, `.env` in `.gitignore`, Mac install fix?
47. Test expectations: none yet, unit only, e2e? Preferred runner (Vitest likely)?
48. Are you actively developing in Replit Agent in parallel? If so, how should we avoid collisions?

## M. Roadmap

49. What is the single first vertical slice you want shipped (for example: one action → earn token → see balance)?
50. Any deadline, demo, grant, or pitch date driving scope?
51. What must NOT be built yet?
