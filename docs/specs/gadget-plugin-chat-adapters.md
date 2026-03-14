# gadget-plugin-chat-adapters Specification

## Purpose
Provide bot-agnostic command and event adapter interfaces so Gadget plugins can integrate with arbitrary chat bots and platforms.

## Standalone and Optional Integrations
- Operates standalone as adapter contracts and runtime routing.
- Consumer plugins can integrate through this adapter layer, but must not require it.

## v1 Functional Requirements
1. Define normalized message/command envelope for plugins:
   - `workspace_id`, `channel_id`, `thread_ts`, `user_id`, `is_bot`, `is_edit`, `is_dm`, `text`, `event_id`
2. Support command namespace strategy to reduce Slack click-ops:
   - top-level command mode
   - subcommand mode under a pre-registered command prefix
3. Expose capability discovery to indicate adapter availability and supported contexts.
4. Route both top-level and threaded message contexts.
5. Preserve enough context for engagement rules to exclude DMs, edits, and bot messages.
6. Ensure replay-safe delivery metadata for idempotent consumers.

## Integration Expectations
- Engagement ledger can parse `@user++` from adapter-delivered messages.
- Engagement ledger can consume slash command payloads from adapter routing.
- Adapter presence is optional; plugins may use direct API/other paths when absent.

## Non-Goals in v1
- Platform-specific deep feature parity across every provider.
- Owning business logic for points, spam, or leaderboard calculations.

## v2 Targets
- Richer platform-specific event subscription options.
- Enhanced command UX helpers and localization.

## Extractable Issues
1. **Define normalized chat event and command envelope contracts**  
   Milestone: `v1-optional-integrations`  
   Labels: `type:api`, `area:adapter`, `priority:p0`, `standalone`
2. **Implement command namespace modes (`top_level`, `subcommand`) with configurable prefix**  
   Milestone: `v1-optional-integrations`  
   Labels: `type:feature`, `area:adapter`, `priority:p0`
3. **Implement capability discovery for optional plugin integration**  
   Milestone: `v1-optional-integrations`  
   Labels: `type:api`, `area:adapter`, `integration:optional`, `priority:p0`
4. **Support threaded and top-level message routing in adapter payloads**  
   Milestone: `v1-optional-integrations`  
   Labels: `type:feature`, `area:adapter`, `priority:p1`
5. **Add replay-safe delivery metadata for idempotent consumers**  
   Milestone: `v1-optional-integrations`  
   Labels: `type:infra`, `area:adapter`, `priority:p1`
