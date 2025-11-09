---
name: UFO Sightings – HW5.1
tools: [Python, HTML, vega-lite]
image: assets/pngs/ufo_preview.png
description: Two Altair visualizations of UFO sightings across time and geography — one static and one interactive with year filtering and duration scaling.
custom_js:
  - vega.min
  - vega-lite.min
  - vega-embed.min
  - justcharts
---

# UFO Sightings – HW5.1

Below are two Vega-Lite charts embedded via JSON specs. The **data** and the **analysis notebook** links are at the bottom.

## Plot 1 – Yearly UFO Reports by Shape (Static)

<vegachart schema-url="{{ site.baseurl }}/assets/json/ufo_chart1.json" style="width:100%"></vegachart>

**Description:**
This visualization displays the relationship between the duration of UFO sightings (in seconds) and the year of occurrence, categorized by the shape of the object. Each point on the scatterplot represents an individual UFO sighting recorded in the dataset. The goal is to identify patterns in sighting durations across different shapes and time periods. It visualizes the total number of UFO reports recorded each year from 1950 to 2022, categorized by the reported shape of the object. It helps viewers identify temporal trends (for example, spikes in reports during certain decades) and the relative frequency of different UFO shapes across time.

**Design Choices:**
- An Altair scatterplot was chosen to emphasize how individual observations vary along both axes:
- The x-axis encodes the year of the sighting (temporal data type) as an ordinal variable.
- The y-axis encodes count() of reports as a quantitative measure.
- The color channel encodes the categorical variable shape_top, separating the most frequent shapes while grouping rarer ones as “Other.”
- Tooltips reveal year and count values for interactive inspection.
- A categorical “schemeCategory10” palette was used. Each UFO shape receives a distinct hue, allowing users to differentiate classes easily without relying on legend labels alone. The palette was chosen for perceptual distinctness and color-blind friendliness, ensuring that shapes such as “Circle,” “Triangle,” and “Disk” remain visually separable.

This encoding emphasizes clear year-over-year comparison while maintaining categorical distinction among shapes.

**Data Transformations:**
Before plotting, the dataset was cleaned and processed:
- The column datetime was parsed with pd.to_datetime() and invalid rows were removed.
- Rows with invalid or missing dates were dropped.
- A new column year was extracted using df['datetime'].dt.year.
- Duration data was converted to a numeric type to ensure consistency.
- Shapes were normalized to title case, and the six most common shapes were retained in a new variable shape_top; all others were grouped as “Other.”

These transformations standardized the data for consistent grouping and accurate aggregation before visualization.

## Plot 2 – World Map of UFO Sightings (Interactive)

<vegachart schema-url="{{ site.baseurl }}/assets/json/ufo_chart2.json" style="width:100%"></vegachart>

**Description:**
This interactive map shows the geographic distribution of UFO sightings around the world, with circle sizes indicating how long the event lasted (the duration of each sighting), each point corresponds to an individual sighting whose position is determined by its latitude and longitude, and color indicates the reported shape. The visualization allows exploration of when and where UFO activity occurred over time.

**Design Choices:**
- The visualization uses longitude (X axis) and latitude (Y axis) encodings to plot each sighting on a world map projection spatially.
- The size of each point is proportional to duration (seconds) — larger circles indicate longer encounters.
- The color encoding represents shape_top (the UFO shape), helping users identify dominant types by region and distinguish shape categories.
- A tooltip displays relevant attributes (city, state, shape, duration, and year) for contextual insight.
- The map projection and consistent scaling make spatial comparison intuitive while avoiding visual distortion.
- The same categorical schemeCategory10 palette was reused for consistency with Plot 1. Maintaining identical color-to-shape mappings supports visual continuity between temporal and spatial views, reducing cognitive load when comparing insights across charts.

**Data Transformations:**
- Latitude and longitude fields were cleaned and converted to numeric types.
- Only rows with valid geographic coordinates and years were retained.
- The year field created for Plot 1 was reused here.
- For performance and clarity, duration values were coerced to numeric type and extreme outliers trimmed to stabilize the size scale.
- Only records within 1950–2022 were kept to remove implausible years.

**Interactivity:**
- This chart includes a year slider parameter created with alt.param() and alt.binding_range().
- Users can drag the slider to adjust the maximum year displayed, dynamically updating the map through a transform_filter.
- This interactivity allows viewers to:
    - Observe the geographic expansion of UFO reports over time.
    - Detect temporal patterns (e.g., peaks in reports during specific decades).
    - Explore correlations between sighting durations and time periods interactively.

---

## Search The Data & Methods

Below are links to both the data and the analysis, presented as buttons:

<!-- these are written in a combo of html and liquid --> 

<div class="left">
{% include elements/button.html link="https://github.com/UIUC-iSchool-DataViz/is445_data/raw/main/ufo-scrubbed-geocoded-time-standardized-00.csv" text="The Data" %}
</div>

<div class="right">
{% include elements/button.html link="https://github.com/shanroy9/shanroy9.github.io/blob/main/python_notebooks/Workbook.ipynb" text="The Analysis" %}
</div>

---