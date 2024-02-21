<script>
  import App from '../components/App.svelte';
</script>

<h1>Estimated Percentage of Countries' Population with Internet Access</h1>

<App />

<body> 
<main> 
  <h2> Writeup</h2>
  <p>
    Regarding our dataset, our team has selected an Internet usage database maintained by the Development Data Section of the Development Data and Outreach Branch within the Statistics Division of the Department of Economic and Social Affairs (UN DESA) of the UN Secretariat. The data in .csv format is available <a href="https://raw.githubusercontent.com/dsc-courses/dsc106-wi24/gh-pages/resources/data/Internet_data.csv">here</a>.
    To visualize this data, our goal was to effectively represent the percentages of internet usage data for each region/country available in our dataset by using a choropleth map. Initially, we explored the possibility of using circle markers with gradient colors to encode the percentages in each respective region. However, we faced challenges when trying to implement the circle markers. Due to time constraints, we decided to use a gradient scale for the entire region instead. This allows us to convey the variation of percentages over the years in a simple yet effective way.
    In addition, we decided to incorporate a slide feature. This feature allows users to easily navigate and compare the changes in internet usage data over the years. The dataset provides information on internet usage for the years 2000, 2005, 2010, 2019, 2020, and 2021. By including this slide feature, users can observe and analyze the trends and patterns in internet usage across different regions and countries over time.
    Another feature we added is the ability to zoom in and out, allowing for a better view of smaller regions on our world map. We also added a hover to display each country’s name as well as its usage.
    During the development process, we split the work into different meeting sessions. Each team member contributed approximately 9-12 hours to develop the project. This includes the time spent on dataset exploration, importing the data, troubleshooting, creating the choropleth map, and working on the write-up.
    The aspect that took the most time during the development process was troubleshooting and resolving issues related to creating the choropleth map using Svelte and D3. We initially started with a different dataset that had a unique geoJSON file, which caused a lot of trouble. Eventually, we switched to using the Internet usage dataset, which required additional adjustments and modifications.
  </p>
    The work was split evenly among all members. Each member contributed approximately 9-12 hours to developing the project. This includes the time spent on dataset exploration, importing the data, troubleshooting, creating the choropleth map, and working on the write-up. The aspect that took the most time during the development process was troubleshooting and resolving issues related to creating the choropleth map using Svelte and D3. We initially started with a different dataset that had a unique geoJSON file, which caused a lot of trouble. Eventually, we switched to using the Internet usage dataset, which required additional adjustments and modifications.
  <p>
    

  </p>
</main>
</body>


<style>
  body {
    background-color: #f0f0f0; /* Set your desired background color */
  }

  h1 {
      text-align: center;
      font-family: 'Roboto', sans-serif; /* Using Roboto font */
      font-size: 28px; /* Increase font size for better visibility */
      margin-bottom: 20px; /* Add some bottom margin for separation */
      color: black; /* Darken the color for better readability */
  }

  main { 
    max-width: 800px; /* Limit width to improve readability */
    margin: 0 auto; /* Center the content horizontally */
    text-align: justify; /* Justify text for better alignment */
    line-height: 1.6; /* Increase line height for better readability */
    font-size: 18px; /* Set a comfortable font size for paragraphs */
    color: #666; /* Adjust text color for better contrast */
  }

  main p {
    margin-bottom: 20px; /* Add some bottom margin between paragraphs */
  }

  main a {
    color: #007bff; /* Change link color */
    text-decoration: none; /* Remove underline */
    font-weight: bold; /* Make links stand out */
  }

  main a:hover {
    text-decoration: underline; /* Add underline on hover */
  }
</style>
