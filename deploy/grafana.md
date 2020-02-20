## Grafana for Ml workflows

This assumes that you have installed all of the roles needed for the ML workflows workshop and have completed the build. The metrics we plot are generated when you use the model service to score text. (This can be done using kafka like in the keynote demo, or by running notebook 07-services.ipynb). 

1. After logging into the OpenShift console, click on:
`networking-->routes.` 
2. In the list of routes, click on the `location` url corresponding to Grafana. This takes you to a blank dashboard. 
3. Click on `Create your first dashboard`, then click on `graph`. This will populate your dashboard with a timeseries plot. 
4. Click on `Panel Title` and click `edit`. This will give you a `Graph` control panel under the plot. There are a few different tabs in this panel - general, metrics, legend etc. 
5. In the `metrics` tab of the graph control panel change `Data Source` from `default` to the name of your OpenShift project by selecting your project from the drop down menu. 
6. Under the `project` there is a black box. If you start typing it will autocomplete to all the metrics Grafana knows about. We want to plot `pipeline_predictions_total` so type that. 
	- If you have already scored text with the model service, these metrics will now be visible in the graph. (There can be a little delay here.)
	- A legend will also be added underneath your graph. This will likely look messy and may contain many rows - something like `{pipeline_predictions_total{app="pipieline......"}}` multiple times, once for each model service you have running. 
	- To clean up the legend and group the prediction metric counts appropriately change from plotting `pipeline_predictions_total` to plotting `sum(pipeline_predictions_total) by (value)` - this groups over all instances of the service. 
	- We can further neaten the legend lables: In the 'Legend format' box type `{{value}}`. Labels should now be `legitimate` and `spam`. 
7. In order to visualise rates of change of the volume of spam/legitimate messages scored by our model we want the y-axis to be on a log scale. You can do this by clicking into the 'Axes' tab in the graph control panel and changing the `Scale` of the `Left Y` to a log scale.
8. Under the `general` tab you can add a panel title. For example, it can be changed to `Total Predictions.`
9. In the top right of the browser there is a clock and a sign that says `last hour`. You can click here to change the time period. Truncating the graph to smaller time periods makes it easier to see data drift happening live. 
10. You can save your dashboard by clicking on the floppy disk icon. This enables you to set it up, close Grafana, run the rest of the demo then open it back up. 

