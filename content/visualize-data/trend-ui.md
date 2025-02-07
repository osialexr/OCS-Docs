---
uid: TrendUserInterface
---

# Trend page

Use the `Trend` page to show data from assets and streams in a graphical format that traces the data over a specified period of time. Use trace data in a trend to monitor assets, anticipate problems, and proactively perform preventative maintenance. Display traces in a trend to better understand the data and gather useful information from it.

The following image shows the important elements of the `Trend` page, and the table below describes how to use these elements. For more information on how to use the `Trend` page to analyze traces, see [View trend data](xref:CreateTrendSession).

![Trend page](images/Trend_full_page.png)

| Callout | Description |
|--|--|
| 1 | Trend pane &ndash; Displays the selected traces. Line traces are displayed for numeric data and heat maps are displayed for string or enumerated data. |
| 1A | Trend mode &ndash; Select to toggle between the stacked, single-scale, and multi-scale view modes. |
| 1B | Cursor &ndash; Place cursors to get minimum, maximum, average, and delta values between two points in time. |
| 1C | Time range picker &ndash; Specify the time range by selecting a time range, specifying a custom range, or using the step forward and step backward arrows. |
| 2A | Namespace &ndash; Select the triangle and select the namespace from the list. |
| 2B | Reset &ndash; Clears the workspace. |
| 2C | Share ![Share](../_icons/default/share.svg) &ndash; Copies the workspace URL. Use this to share your workspace with others. |
| 3 | Add Traces pane &ndash; Lists the assets and streams available to add as traces to the `Trend` pane. |
| 3A | Information ![Information](../_icons/branded/information.svg) &ndash; Mouse over to display a tooltip of stream information, including name and identifier. For streams shared from a community, tenant name and namespace identifier are listed as well. |
| 3B | Plus ![Plus](../_icons/branded/plus.svg) &ndash; Select to add a trace to the `Trend` pane. |
| 4 | Legend table &ndash; Displays information about the traces in the `Trend` pane. Toggle between the Trend and Cursor views. |
| 4A | Trend view &ndash; Select the **Trend** ![Trend](../_icons/default/chart-line.svg) icon to display statistics about each trace in the Legend table. The screen capture shows the trend view. |
| 4B | Cursor view &ndash; Select the **Cursor** ![Cursor](../_icons/default/map-marker.svg) icon to display cursor statistics in the Legend table. The cursor must be locked to display the statistics (select **Plus** ![Plus](../_icons/default/plus.svg) above the cursor). With two or more locked cursors, summary statistics are displayed for contiguous cursors. |

## Extrapolated values

When viewing a trend session, extrapolated values are depicted as dashed lines and dashed heatmaps. Extrapolated values are based on historic values.

- **Dashed lines**

    For numeric data types, extrapolated values are depicted as dashed lines.

    ![numeric data type extrapolated values](images/extrapolated-values-line.png)

- **Dashed heatmaps**

    For enumerations, extrapolated values are depicted as as dashed heatmaps.

    ![enumeration extrapolated values](images/extrapolated-values-heatmap.png)