# Future multiplayer notes

This version is a local single-player game. It has no network transport, database, login, or online matchmaking.

When multiplayer is added, keep the browser client responsible for input and drawing. A trusted game server should own match rules and results.

## Suggested boundaries

- **Input:** Send small, numbered player commands for movement and firing.
- **Match state:** Let the server validate health, ammo, cooldowns, hits, sector progress, and credit rewards.
- **Opponent source:** Support both server-run AI and remote pilots behind the same opponent interface.
- **Identity:** Resolve player IDs on the server. Never trust an ID, score, or coin balance supplied by the browser.
- **Persistence:** Save upgrades and sector progress only after server validation.
- **Matchmaking:** Create matches on the server and issue short-lived connection credentials.
- **Transport:** WebSockets are a practical fit for low-latency match updates. Add snapshots and reconnect handling.

## Migration order

1. Define versioned messages for joining, player input, state snapshots, hits, and match results.
2. Move combat validation and rewards to the server while keeping rendering in the client.
3. Run AI on the server and send state snapshots to the browser.
4. Add identity, matchmaking, persistence, and reconnect support.
5. Check latency, disconnects, duplicate reward claims, and invalid inputs before opening matches publicly.

Keep this note updated once a server protocol is chosen.

