# StringSpec for Claude and other MCP clients

![StringSpec](assets/icon.svg)

Ask an AI assistant about tennis strings and get answers from lab measurements instead of marketing copy: how stiff a string is, how fast it loses tension, how much energy it returns, how much spin it allows, and which strings suit a player's needs and racquet.

This repository holds:

- the connection details for the **StringSpec remote MCP server** at `https://stringspec.com/mcp`,
- a **Claude plugin** that adds that server plus a `string-research` skill, which teaches Claude how to read the numbers.

The server is run by [StringSpec](https://stringspec.com), a database of nearly 800 tennis strings measured on the same machine under the same protocol, so one string's numbers compare fairly with another's. How the numbers are made: [methodology](https://stringspec.com/methodology/).

## What you can ask

- "Which polyester strings are the softest, and what do they cost?"
- "How fast does Solinco Hyper-G 16 lose tension, and how long will it stay playable?"
- "Compare RPM Blast 17 with Luxilon ALU Power 16L."
- "I have tennis elbow and a stiff racquet. What should I string, without natural gut?"
- "What should I string for more spin on an 18x20 racquet?"

## Tools

All tools are read-only (`readOnlyHint: true`) and need no account.

| Tool | What it answers |
|---|---|
| `search_strings` | Filter by name, brand, material, gauge and price; sort by popularity, softest, stiffest, most spin, best tension hold, most power or cheapest. At most 10 strings per call. |
| `get_string` | Everything on one string, found by name: every measurement with its percentile in the database, elongation at 40, 51 and 62 lb, an estimated playable life, a tension adjustment, how it ranks for spin, comfort, control, power, tension hold, durability and feel, the closest alternatives, and the retail price. |
| `compare_strings` | Two or three strings side by side, with the comparison page on stringspec.com. |
| `recommend_strings` | StringSpec's string finder: a main need and an optional second one, adjusted for the racquet (string pattern, head size, frame stiffness), with a material ruled out if asked. Returns a ranked shortlist with a 0 to 100 fit and the reason each string fits. |

Every answer separates measurements from estimates (playable life, tension advice and fit are derived from the measurements) and dates each price.

## Setup

### Claude (claude.ai, Desktop, mobile)

Settings → Connectors → Add custom connector, then paste `https://stringspec.com/mcp`. No sign-in is needed.

### Claude Code

Install the plugin, which adds the server and the `string-research` skill:

```
/plugin marketplace add BigBalli/stringspec-mcp
/plugin install stringspec@stringspec
```

Or add only the server:

```
claude mcp add --transport http stringspec https://stringspec.com/mcp
```

### Other MCP clients

Any client that supports remote MCP servers over Streamable HTTP can use `https://stringspec.com/mcp` with no credentials. The server speaks protocol versions 2026-07-28, 2025-11-25, 2025-06-18 and 2025-03-26 and answers with JSON (no SSE, no sessions).

## Privacy

The server receives the tool name and its arguments (for example a string name or "comfort"), uses them to answer, and does not store them. It never sees your conversation or your account. Full policy: [stringspec.com/privacy](https://stringspec.com/privacy/).

## Support

Email g@bigballi.com, or see [stringspec.com/connect](https://stringspec.com/connect/).

## License

The contents of this repository are released under the MIT License. The data served by the StringSpec MCP server is not part of this repository and is not covered by that license.
