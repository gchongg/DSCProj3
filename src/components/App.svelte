<script>
  import { onMount } from 'svelte';
  import * as d3 from 'd3';

  let svg;
  let data = new Map();
  let colorScale;

  let internet_usage = []
  let countryISO_map = new Map();
  let selectedYear = 2010; // Default year

  colorScale = d3.scaleThreshold()
      .domain(d3.range(0, 110, 10))
      .range(["rgb(247,251,255)",
              "rgb(222,235,247)",
              "rgb(198,219,239)",
              "rgb(158,202,225)",
              "rgb(107,174,214)",
              "rgb(66,146,198)",
              "rgb(33,113,181)",
              "rgb(8,81,156)",
              "rgb(8,48,107)",
              "rgb(0,0,80)",
              "rgb(3,19,43)"]);

  onMount(async () => {
    // Fetch data
    const [geoJSON] = await Promise.all([
      d3.json("https://raw.githubusercontent.com/holtzy/D3-graph-gallery/master/DATA/world.geojson"),
    ]);

    const res = await fetch("internet_usage.csv");
    const csv = await res.text();
    internet_usage = d3.csvParse(csv, d3.autoType)

    // Map country names to ISO codes
    geoJSON.features.forEach((element) => countryISO_map.set(element.properties.name, element.id));

    // Process CSV data and store it in the Map
    internet_usage.forEach(d => {
      if (countryISO_map.has(d.name)) { 
        if(!data.has(d.year)){
          data.set(d.year, new Map());
        }
        data.get(d.year).set(countryISO_map.get(d.name), d.value);
      }
    });

    // Setup SVG
    svg = d3.select("svg");
    var width = +svg.attr("width"), 
        height = +svg.attr("height");
    // Map and projection
    const path = d3.geoPath();
    const projection = d3.geoEquirectangular()
      .scale(150)
      .center([0,0])
      .translate([width/2 , height/2]);

    // Color scale


    // Draw the map
    svg.append("g")
      .selectAll("path")
      .data(geoJSON.features)
      .enter()
      .append("path")
      // draw each country
      .attr("d", d3.geoPath().projection(projection))
      // set the color of each country
      .attr("fill", d => {
        const total = data.get(selectedYear).get(d.id) || 0;
        return colorScale(total);
      })
      .style("stroke", "transparent")
      .attr("class", "Country")
      .style("opacity", 0.8)
      .on("mouseover", function() {
        d3.select(this)
          .transition()
          .duration(200)
          .style("opacity", 1)
          .style("stroke", "black");
      })
      .on("mouseleave", function() {
        d3.select(this)
          .transition()
          .duration(200)
          .style("opacity", 0.8)
          .style("stroke", "transparent");
      })
      .append("title").text(function(d) { 
        return `${ d.properties.name } \n Estimated Percentage of Indviduals using the Internet: ${data.get(selectedYear).get(d.id)} `
      });
      const zoom = true;
      if (zoom) {
        var zoomFunction = d3.zoom()
            .scaleExtent([1, 8])
            .on('zoom', function(event) {
              svg.selectAll('path')
              .attr('transform', event.transform);
            });
          svg.call(zoomFunction);
      };

//Legend
    const legend = svg.append("g")
                  .attr("transform", "translate(20, 20)");
    const legendScale = d3.scaleLinear()
                        .domain([0, 100])
                        .range([0, 200]);
    const legendAxis = d3.axisBottom(legendScale)
                        .tickValues(colorScale.domain())
                        .tickFormat(d3.format(".0f"));

    legend.append("g")
      .call(legendAxis)
      .select(".domain")
      .remove();

    legend.selectAll("rect")
      .data(colorScale.range().map(color => {
        const d = colorScale.invertExtent(color);
        if (d[0] == null) d[0] = legendScale.domain()[0];
        if (d[1] == null) d[1] = legendScale.domain()[1];
        return d;
      }))
      .enter()
      .append("rect")
      .attr("height", 6)
      .attr("x", d => legendScale(d[0]))
      .attr("width", d => legendScale(d[1]) - legendScale(d[0]))
      .attr("fill", d => colorScale(d[0]));
    });


  // Reactive statement moved to top-level
  $: {
    if (data.has(selectedYear)) {
      updateMap();
    }
  }

  // Function to update the map
  function updateMap() {
  svg.selectAll("path")
    .attr("fill", d => {
      const total = data.get(selectedYear).get(d.id) || 0;
      return colorScale(total);
    })
    .select("title") // Select existing title element
    .text(function(d) { 
      return `${ d.properties.name } \n Estimated Percentage of Individuals using the Internet: ${data.get(selectedYear).get(d.id)} `
    });
  }
</script>


<style>
    @import url('https://fonts.googleapis.com/css2?family=Nunito:wght@300;400;700&display=swap');

  h1 {font-family: 'Nunito', sans-serif;
    font-weight: 400;
    line-height: 2;
    font-size: 24px;
    color: var(--color-text);
    justify-content: center;
  }
  main {
    text-align: center;
    font-family: 'Nunito';
    font-weight: 400;
    line-height: 0;
    font-size: 16px;
    color: var(black);
    justify-content: right;
  }
</style>

<main>
  <svg width="1000" height="500"></svg>
  <div class="overlay">
    <label>{selectedYear}</label>
    <input
      id="slider"
      type="range"
      min="2000"
      max="2021"
      bind:value ={selectedYear}
    />
  </div>
</main>
