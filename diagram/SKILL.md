---
name: diagram
description: Use when the user asks for a diagram, architecture visualization, flow, or system diagram of any kind.
disable-model-invocation: true
---

# Diagram

## Output Format

Always render as ASCII art. Use standard, free-form ASCII — boxes, lines, arrows in whatever style fits the diagram. No Mermaid, no Excalidraw JSON, no image links.

If the user explicitly asks for a **description** or **spec** (e.g., "describe this for Excalidraw"), switch to Describe Mode below.

## Describe Mode

Only use when the user explicitly asks for a diagram description/spec for a tool like Excalidraw.

Output plain prose only — no markdown, no bullet points, no headers, no tables. The text will be pasted directly into Excalidraw's text-to-diagram AI import field, which converts natural language to a diagram.

Write three paragraphs in this order:

First, describe each component: its name, shape type, color, and explicit position. Use directional anchors — say "place X directly above Y" or "place X to the right of Y on the same row." Keep shape labels concise; if a component has a long name or technology detail, embed it directly in the label using parentheses rather than as a separate annotation element — separate annotations drift and render as floating boxes in the flow. Example: "Browser is a yellow circle in the top-left. LB (Nginx) is a red diamond placed directly below Browser."

Second, describe each connection with a label of 2–3 words maximum. Omit "(Sync)" — synchronous is assumed unless stated otherwise. Describe multi-step flows as a chain, not a fan. For repeated elements (e.g. multiple instances of the same group), name the components of each instance explicitly and say "with the same connections as [first instance]" — never use "identical internal structure" alone, as this causes connections to be dropped. Example: "Browser sends 'HTTP request' to LB. LB sends 'shop lookup' to Routing Table. Routing Table sends 'route request' to Instance A, Instance B, and Instance C. Instance B contains Service and Database with the same connections as Instance A."

Third, describe groupings. Embed any annotation text directly in the frame's label rather than as a separate element inside the frame — separate elements render as floating white boxes. Example: "Group Service and Database inside a gray boundary frame labeled 'Zone A — production only'."

**Shape and color reference** (use these when writing the prose above):

- Circle, yellow (#ffec99) — clients, actors, browsers, external systems
- Rectangle, blue (#6c8cff) — services, microservices
- Rectangle, green (#34d399) — databases, persistent storage
- Rounded rectangle, blue (#6c8cff) — API gateways
- Rectangle with dashed border, green (#34d399) — caches
- Diamond, red (#f87171) — load balancers
- Rounded rectangle, purple (#a78bfa) — queues, message brokers
- Frame, gray (#94a3b8) — boundaries, network zones, groups

**Arrow reference** (use these when describing connections):

- Synchronous request (default) — solid arrow, 2–3 word label
- Async / event — dashed arrow, label with: publishes: event.name
- WebSocket / streaming — bidirectional arrow
- Data flow — dashed arrow with "data flow" label (Mermaid cannot apply labels to undirected dashed lines; always use a dashed arrow here, never a bare dashed line)

**Layout guidance:**

- Clients on the left or top, services in the center, storage at the bottom
- Describe top-to-bottom or left-to-right flow explicitly
- Group by zone or domain before describing individual components inside
