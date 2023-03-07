# Kusto
- This custom query is intended to be used in an Azure workbook
- To customize the appearance or formatting of values select Column Settings in your workbook.
- here you should be able to select colors, values, and to hide columns ,each time you add another codeblock like the following ```| join (
    InsightsMetrics
    | where Name == "TransferPerSecond"
    | project-rename TransferPerSecond = Val
    | project-away TenantId, TimeGenerated, SourceSystem, Origin, Namespace, Tags, AgentId, _ResourceId, Type
    | summarize take_any(*)
) on Computer```

- It will add a repetitive column named Computer1, Computer2, Computer3, and so forth. In the column settings you can hide those repeat columns as well. 
- If there is another VM metric you'd like to add copy your query into a Log Analytics Workspace and run `InsightsMetrics`. the resulting output should have a column named "name" from this column you will see different rows, these are the various metrics available to you. Once you've decided which metrics you want simply repeat the | join code block and change it to look like the following

```| join (
    InsightsMetrics
    | where Name == "YourNewMetric"
    | project-rename "YourNewMetric" = Val
    | project-away TenantId, TimeGenerated, SourceSystem, Origin, Namespace, Tags, AgentId, _ResourceId, Type
    | summarize take_any(*)
) on Computer```
