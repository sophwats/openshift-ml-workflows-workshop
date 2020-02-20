## Grafana for Ml workflows

This assumes that you have installed all of the roles needed for the ML workflows workshop and have completed the build. The data is generated when you run use the model service to score text. (This can be done using kafka like in the keynote demo, or by running notebook 07-services.ipynb). 

1. After logging into the OpenShift console, click on:
`networking-->routes.` 
2. In the list of routes, click on the `location` url corresponding to graphana. This takes you to a blank dashboard. 
3. Click on `Create your first dashboard`, then click on `graph`. This will populate your dashboard with a time series plot. 
4. Click on `Panel Title` and click `edit`. This will give you a `Graph` control panel under the plot. There are a few different tabs - general, metrics, legend etc. 
5. In the `metrics` tab of the graph control panel change Data Source from `default` to the name of your OpenShift project by clicking and selecting your project from the drop down options. 
6. Under the `project` there is a black box. If you start typing it will autocomplete to all the metrics it knows about. We want to plot `pipeline_predictions_total` so type that. 
	- if you have already scored text with the model service data will be added to your graph automatically. (there can be a little delay here)
	- Labels will also be added underneath your graph. These will likely look messy - something like `{pipeline_predictions_total{app="pipieline......"}}` and there will be one of these for each version of your service you have running. 
	- we want to clean this up and group the prediction counts appropriately, so change from plotting `pipeline_predictions_total` to plotting `sum(pipeline_predictions_total) by (value)` - this groups over all instances of the service. 
	- we still want to neaten up the legend lables some more. to do this, in the 'Legend format' box type `{{value}}`. Labels should now be `legitimate` and `spam`. 
7. In order to visualise rates of change of the volume of spam/legitimate messages we want the y-axis to be on a log scale. You can do this by clicking into the 'Axes' tab in the graph control panel and changing the `Scale` of the `Left Y` to a log scale. (We usually roll with `log(base 2)`). 
8. Under the `general` tab you can add a panel title. For example, it can be changed to `Total Predictions.`
9. In the top right there is a clock and a sign that says `last hour`. You can click here to change the time period - this is really useful to show changes live. We usually set it to 5 or 15 minutes. 
10. You can save your dashboard by clicking on the floppy disk icon. This enables you to set it up, close grafana, run the rest of the demo then open it back up. 

