# Markdown List Baseline

Rich Markdown list rows combine a SwiftUI marker with a UIKit-backed body.
`InlineMarkdown` publishes the body text view's first glyph baseline so bullet,
number, and task markers align with the first rendered line at every chat text
size, including wrapped items.

The focused hosted regression
`MarkdownRichContentHostedTests/testRichListMarkersShareTheirBodiesFirstLineBaseline()`
checks the UIKit glyph baseline numerically at the default and largest chat text
sizes. It also retains the `rich-list-marker-alignment` screenshot attachment
for visual inspection. The fixture removes its hosting view and drains teardown
to an observed, bounded completion signal to avoid leaking appearance work into
later tests.
