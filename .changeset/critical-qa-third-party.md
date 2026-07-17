---
"mattpocock-skills": patch
---

Extend `/critical-qa`'s action→consequence probe across external boundaries: when an action hands off to a third-party service (payment, auth, e-sign) the critique can't complete for real, drive the provider's sandbox, **simulate the callback** it would send on success, and verify the consequence landed — a checkout that redirects but whose webhook never upgrades the plan or raises the quota is the classic gap. `/manual-qa` and `/e2e` inherit it.
