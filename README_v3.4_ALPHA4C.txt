WIRZA v3.4 Alpha 4C

This batch creates the common first-person visual transform bridge used by:
- Item Customizer
- Shields
- 1.7 Visuals

How it works:
Minecraft first-person model matrix -> verified WIRZA adapter -> visual transform -> normal rendering.

The important compatibility rule is strict: WIRZA only installs this hook when the exact Minecraft executable version has a matching verified entry in SignatureProfiles.h. There is no wildcard or guessed signature fallback.

At the moment kVerifiedFirstPersonProfiles is intentionally empty because this environment cannot launch Minecraft for Windows and cannot validate the current executable. As a result, the three modules safely report Partial / Unsupported until a real build is inspected. Their module settings and transform logic are implemented now, so adding the verified per-build profile later does not require redesigning the modules.

1.7 sword block is visual only. It does not add a server-side blocking mechanic to Bedrock and does not modify combat packets.
