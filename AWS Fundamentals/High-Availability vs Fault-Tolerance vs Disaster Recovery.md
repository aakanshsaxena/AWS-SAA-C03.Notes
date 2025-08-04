HA - aims to **ensure** an agreed level of operational **performance** usually **uptime**, for a **higher than normal period**
- Not aiming to stop failure -> designed to be online and providing services as often as possible
- When it fails -> its components can be replaced or fixed ASAP
- Not about the user experience, about maximizing a system's online time
- Measured in % of available time
- Keep a system operational - fast or automatic recovery of issues
Fault Tolerance - the property that enables a system to **continue operating properly** in the event of the **failure of some** (one or more faults within) of its **components**
- Continue operating through a failure without impacting costumers
- Can be expensive - much more complex than high availability
Disaster Recovery - a set of policies, tools and procedures to **enable the recovery** or **continuation** of **vital** technology infrastructure and systems **following a natural or human-induced disaster**
- What if HA and FT don't work?
- What happens before (pre-planning) and what happens after (DR process)
- Keep your crucial and non-replaceable parts of your system safe
HA - minimize any outages
FT - operate through faults
DR - used when these don't work