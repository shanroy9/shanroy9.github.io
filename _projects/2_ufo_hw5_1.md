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
This visualization displays the relationship between the duration of UFO sightings (in seconds) and the year of occurrence, categorized by the shape of the object. Each point on the scatterplot represents an individual UFO sighting recorded in the dataset. The goal is to identify patterns in sighting durations across different shapes and time periods.

**Design Choices:**
- An Altair scatterplot was chosen to emphasize how individual observations vary along both axes:
- The x-axis encodes the year of the sighting (temporal data type).
- The y-axis encodes the duration (seconds) (quantitative).
- The color encoding differentiates between UFO shapes (nominal type), using a category10 color scheme for clear separation between groups.
- Tooltips were added to display the city, state, shape, and duration when hovering over a point for more detail.

This combination of encodings allows for easy detection of clusters or anomalies (e.g., unusually long durations or specific shapes appearing in particular eras).

**Data Transformations:**
Before plotting, the dataset was cleaned and processed:
- The original datetime field was parsed into a true datetime format using pd.to_datetime().
- Rows with invalid or missing dates were dropped.
- A new column year was extracted using df['datetime'].dt.year.
- Duration data was converted to a numeric type to ensure consistency.

These transformations standardized the input for Altair and enabled temporal plotting and filtering.

## Plot 2 – World Map of UFO Sightings (Interactive)

<vegachart schema-url="{{ site.baseurl }}/assets/json/ufo_chart2.json" style="width:100%"></vegachart>

**Description:**
This interactive map shows the geographic distribution of UFO sightings around the world, with circle sizes indicating the duration of each sighting. A year slider enables filtering the data dynamically, allowing users to explore how UFO sightings evolved over time.

**Design Choices:**
- The visualization uses longitude and latitude encodings to plot each sighting on a world map projection (equalEarth).
- The size of each point is proportional to duration (seconds) — larger circles indicate longer encounters.
- The color encoding represents shape_top (the UFO shape), helping users identify dominant types by region.
- A tooltip displays relevant attributes (city, state, shape, duration, and year) for contextual insight.
- The map projection and consistent scaling make spatial comparison intuitive while avoiding visual distortion.

**Data Transformations:**
- Latitude and longitude fields were cleaned and converted to numeric types.
- Only rows with valid geographic coordinates and years were retained.
- For performance and clarity, durations were capped to filter out extreme outliers.
- A new field year was created for slider-based filtering.

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
{% include elements/button.html link="https://github.com/shanroy9/shanroy9.github.io/blob/main/python_notebooks/UFO_HW5_1.ipynb" text="The Analysis" %}
</div>

---