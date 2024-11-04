
## Overview
In this project, an interactive dashboard was completed to visualize bacterial data from volunteers, specifically focusing on identifying the top 10 bacterial species found in belly buttons. Four technical deliverables were created using JavaScript, Plotly, and D3.js: a horizontal bar chart to display the top species, a bubble chart to visualize sample values, and a gauge chart for weekly washing frequency. The final deliverable involved customizing the dashboard for improved aesthetics and usability. Each chart updates based on user-selected IDs from a dropdown menu, providing valuable insights into the bacterial composition relevant to synthetic beef production.

link to Interactive dashboard: https://dianahandler.github.io/Bacterial-Species-Interactive-Dashboard/


## Outline Steps and Code


The init function initializes the dashboard by populating a dropdown menu with sample names from a JSON file (samples.json). Here’s a breakdown of the steps:  

Select Element Reference: It grabs a reference to the dropdown select element in the HTML using D3.js.  
Fetch Data: It uses D3's json method to asynchronously retrieve data from samples.json.  
Populate Dropdown:  
It extracts the list of sample names from the retrieved data.  
For each sample name, it appends an <option> element to the dropdown menu, setting the display text and value to the sample name.  
Build Initial Plots: After populating the dropdown, it selects the first sample from the list and calls the buildCharts and buildMetadata functions with this sample to generate the initial visualizations and metadata display.  

This function sets up the interactive elements of the dashboard, ensuring that users can select a sample to view corresponding data visualizations.  
  
![Screenshot 2024-11-03 at 11 09 44 PM](https://github.com/user-attachments/assets/a74b33de-36d8-4e18-9fa1-5cf266d85fe9)


Next, we set up the dashboard functionality, focusing on handling user interactions and updating the displayed metadata based on the selected sample.  

Dashboard Initialization:  

The init() function is called to set up the initial state of the dashboard when the page loads.  
Sample Change Handling:  

The optionChanged(newSample) function is defined to be triggered whenever a new sample is selected from the dropdown menu. This function calls:  
buildMetadata(newSample): Updates the demographic information for the selected sample.  
buildCharts(newSample): Updates the visualizations based on the new sample.  
Building the Demographics Panel:  

The buildMetadata(sample) function retrieves the metadata from the samples.json file using D3.js.  
It filters the metadata to find the object corresponding to the selected sample (matching the sample ID).  
The function selects the HTML panel with the ID #sample-metadata and clears any existing content.  
It uses Object.entries() to loop through the key-value pairs of the selected sample's metadata and appends each pair to the panel as a new heading element (<h6>).  
Overall, this code manages user interactions, allowing the dashboard to dynamically update both the demographic information and the visualizations based on the selected sample.  

  
![Screenshot 2024-11-03 at 11 13 18 PM](https://github.com/user-attachments/assets/f520f602-6be1-4a7e-b5e1-6ca27e3f5f73)


## Creating Our Bar Chart

This code defines the buildCharts function, which is responsible for preparing data for visualizations based on a selected sample. Function Definition: The buildCharts(sample) function is created to take a sample ID as an argument.  
  
Data Retrieval: It uses d3.json to load the samples.json file asynchronously.  

Samples Array: It creates a variable, samples, that holds the array of sample data from the JSON file.  

Filtering Samples: It filters the samples array to find the object that matches the provided sample ID and stores it in filteredSamples.  

Sample Results: The first object from the filteredSamples array is stored in sampleResults, representing the selected sample's data.  

Data Extraction: It extracts the otu_ids, otu_labels, and sample_values from sampleResults into separate variables for further processing.  

Overall, this function sets up the data needed to create visualizations by retrieving and filtering sample data from the JSON file.  

![Screenshot 2024-11-03 at 11 17 48 PM](https://github.com/user-attachments/assets/61ea76c9-faf4-4068-a8b3-3104593d5025)


## Setting Up the Layout of Our Chart

![Screenshot 2024-11-03 at 11 21 13 PM](https://github.com/user-attachments/assets/f6a6e795-90d4-404a-8c5e-5f90f3406a18)


This code snippet prepares and renders a horizontal bar chart using Plotly, displaying the top 10 bacterial cultures found in a sample.

Y-Ticks Creation:  
It maps the sampleID array to create yticks, labeling each OTU as "OTU X" and selects the top 10, reversing the order for proper display.  
  
X-Values and Hover Text: 
It slices the sampleValues and sampleLabels arrays to get the top 10 values and corresponding labels, also reversing their order to match the y-ticks.  
  
Bar Data Trace:  
It constructs the barData array with a single trace object for the bar chart, specifying the x and y values, setting the type to "bar", and defining the orientation as horizontal.  
  
Bar Layout:  
It defines barLayout for the chart, including the title "Top 10 Bacteria Cultures Found".  
  
Plotting the Chart:  
Finally, it uses Plotly.newPlot to render the bar chart in the HTML element with the ID 'bar', using the prepared data and layout.  

## Creating Our Bubble Chart

Bubble Data Trace:

This code creates the bubbleData array with a single trace object for the bubble chart. The trace includes:  
- x: The OTU IDs from sampleID.
- y: The corresponding sample values from sampleValues.
- text: The labels from sampleLabels for hover information.
- mode: Set to 'markers' to represent data points as bubbles.
- marker: Configured with:
-  size: Bubble sizes based on sampleValues.
-  color: The bubble colors based on sampleID.
-  colorscale: Uses the 'Earth' colorscale for visual appeal.
  
Bubble Layout:  

It defines bubbleLayout for the chart, including:  
- A title "Bacteria Cultures Per Sample".
- X-axis labeled "OTU ID".
- Margins to adjust the layout.
- hovermode set to 'closest' for better interaction.
  
Plotting the Chart:  
Finally, it uses Plotly.newPlot to render the bubble chart in the HTML element with the ID 'bubble', utilizing the prepared data and layout.  

![Screenshot 2024-11-03 at 11 24 58 PM](https://github.com/user-attachments/assets/f50aa32d-a2dc-4dc8-8a7c-1acaaf54a70f)



## Creating our Gauge Chart

The following code prepares and renders a gauge chart using Plotly to display the belly button washing frequency for a selected sample.  
Filtering Metadata:  
- It filters the metadata array to find the object corresponding to the selected sample ID (sample) and stores the result in metadataResult.
Sample Metadata:  
- It retrieves the first object from the filtered metadata array, storing it in sampleMetadata, which contains the relevant information for the selected sample.
Washing Frequency:  
- It extracts and converts the washing frequency (wfreq) from sampleMetadata into a floating-point number and stores it in wFreq.
Gauge Chart Trace:  
- It creates the gaugeData array with a single trace for the gauge chart, including:  
-  value: Set to wFreq.
-  type: Defined as "indicator" for a gauge chart.
-  mode: Set to "gauge+number" to display both the gauge and the numerical value.
-  title: A formatted title indicating the measurement (scrubs per week).
-  gauge: Configuration details for the gauge, including:
-   Axis range from 0 to 10.
-   A black color for the gauge bar.
-   Steps defining color ranges for different washing frequency intervals.

  
Gauge Layout:  
- It defines gaugeLayout to set the size and margins of the gauge chart.  
Plotting the Chart:  
- Finally, it uses Plotly.newPlot to render the gauge chart in the HTML element with the ID 'gauge', using the prepared data and layout.

![Screenshot 2024-11-03 at 11 32 26 PM](https://github.com/user-attachments/assets/b8008527-1d2d-48ee-aa90-1a11e1bd5f36)


link to Interactive dashboard: https://dianahandler.github.io/Bacterial-Species-Interactive-Dashboard/



