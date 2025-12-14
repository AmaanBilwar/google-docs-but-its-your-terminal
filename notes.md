# Notes for amaan by amaan

## how does ratatui layout constraints work?

`Constraint::Length(n)` reserves exactly *n* rows (or columns) for that area, regardless of how much space is left.  
`Constraint::Min(n)` guarantees at least *n* rows but lets the widget expand to fill any remaining space after the fixed‑size sections are allocated.  

In our UI:

* `Constraint::Length(1)` gives the help bar a single line.  
* `Constraint::Min(3)` forces the messages pane to occupy at least three lines, but it grows to use all extra space below the help bar.  
* `Constraint::Length(3)` fixes the input box to three lines so it never gets trimmed.  

Together they create a stable three‑section layout where the input stays visible, the messages can scroll, and the help line is always present — exactly what the ratatui docs describe for `Layout` and `Constraint` [[ratatui layout docs]](https://docs.rs/ratatui/latest/ratatui/layout/struct.Constraint.html).
