# HAL design diagrams

- `hal-class-diagram.mmd`: initial UML class diagram showing Strategy,
  Decorator, Observer, Factory, State, and Command.
- `hal-activity-diagram.mmd`: activity-style Mermaid flowchart showing
  sensor strategy call → event → factory call → state call → command call.
  Mermaid flowchart notation is used rather than formal UML activity notation.

These diagrams describe the initial design, not implemented code. They show
representative classes and commands rather than every device subclass or action.

## Design conventions

A sensor owns its identity and calls an interchangeable reading strategy.
Decorators wrap that strategy to add simulation behaviour. A shared simulation
timer samples sensors; individual decorators do not require their own threads.

Automation observers receive a shared command factory. The factory owns the
current mode State and delegates command creation to it. This is a simple Factory
combined with State, not a claim that it is the GoF Factory Method pattern.
Home and Away create commands appropriate to an event. Observe returns none,
while readings, availability, and event logging continue. Manual commands remain
available in every mode.

Event notifications and automatic commands run sequentially for the prototype.
The activity diagram's outgoing event arrows show subscriber notifications, not
parallel execution. Swing display updates must run on the event dispatch thread.
Automation observers filter event types so their own action results do not cause
unintended feedback loops. Commands report actual results; requesting an action
does not imply success.

Mode changes take place between event-handling cycles. Entering Observe hides
active alerts without changing device states or deleting history. Returning to
Home or Away re-evaluates current readings. These transitions and the manual
control path are omitted from the sensor activity diagram to keep its main flow
clear.

## Viewing and export

Open the `.mmd` files with a Mermaid preview extension or paste their contents
into a Mermaid editor. To export PDFs with Mermaid CLI installed, run from the
repository root:

```bash
mmdc -i report/figures/src/hal-class-diagram.mmd -o report/figures/hal-class-diagram.pdf -b white --pdfFit
mmdc -i report/figures/src/hal-activity-diagram.mmd -o report/figures/hal-activity-diagram.pdf -b white --pdfFit
```

The report currently includes the manually rendered `../uml-rev-1.png` and
`../activity-rev-1.png`. Re-export those files after editing the Mermaid sources,
or update the image paths in `report/main.tex` if using the PDF exports above.

## Inline report layout

Both figures use `[H]` placement at their source positions, without landscape
pages or forced page breaks. If a figure does not fit in the remaining page
space, LaTeX moves the whole figure to the next page in document order.

The activity source now uses a compact left-to-right flow. After installing
Mermaid CLI, replace the existing PNG from the repository root:

```bash
mmdc -i report/figures/src/hal-activity-diagram.mmd -o report/figures/activity-rev-1.png -b white -w 1600 -s 2
```

Then rebuild the report. The activity image has a height cap to keep the old
portrait export within the page until it is replaced; the new wide export
will use the available text width.
