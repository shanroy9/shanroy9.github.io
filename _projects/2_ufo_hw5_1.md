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

**What & why:** This bar chart shows counts of UFO reports per year, split by the most frequent shapes.  
**Encodings:** `x` = Year (O), `y` = Count (Q), `color` = Shape (N).  
**Color scheme:** Categorical palette separates top shape categories (“Other” groups the rest).  
**Transformations:** Parsed `datetime` to get `year`, grouped shapes by top frequency.

## Plot 2 – World Map of UFO Sightings (Interactive)

<vegachart schema-url="{{ site.baseurl }}/assets/json/ufo_chart2.json" style="width:100%"></vegachart>

**What & why:** A geospatial view of individual sightings. Circle **size** encodes report **duration**, and **color** encodes shape.  
**Interactivity:** A **year slider** filters points to “Year ≤ N”, letting viewers see how spatial patterns evolve.  
**Encodings:** `longitude/latitude`, `size = duration (seconds)`, `color = shape`, `tooltip` = city/state/shape/duration/year.  
**Transformations:** Cleaned date/time, numeric duration, valid lon/lat; aggregated nothing (point-level).

---

## Search The Data & Methods

Below are links to both the data and the analysis, presented as buttons:

<!-- these are written in a combo of html and liquid --> 

<div class="left">
{% include elements/button.html link="https://github.com/UIUC-iSchool-DataViz/is445_data/raw/main/ufo-scrubbed-geocoded-time-standardized-00.csv" text="The Data" %}
</div>

<div class="right">
{% include elements/button.html link="https://github.com/shanroy9/shanroy9.github.io/python_notebooks/UFO_HW5_1.ipynb" text="The Analysis" %}
</div>

---