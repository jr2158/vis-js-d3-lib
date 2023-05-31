<script setup>

import ExampleBarChart from "./components/ExampleBarChart.vue";

</script>

# Getting started

D3 supports a variety of environments.

## Try D3 online

The fastest way to get started (and get help) with D3 is on [Observable](https://observablehq.com)! D3 is available by default in notebooks as part of Observable’s standard library. To create something with D3, return the generated DOM element from a cell. Here is an example bar chart:

<ExampleBarChart />

```js
{
  // Declare the chart dimensions and margins.
  const width = 640;
  const height = 400;
  const marginTop = 30;
  const marginRight = 0;
  const marginBottom = 30;
  const marginLeft = 40;

  // Declare the x (horizontal position) scale.
  const x = d3.scaleBand()
      .domain(alphabet.map((d) => d.letter))
      .range([marginLeft, width - marginRight])
      .padding(0.1);

  // Declare the y (vertical position) scale.
  const y = d3.scaleLinear()
      .domain([0, d3.max(alphabet, (d) => d.frequency)])
      .range([height - marginBottom, marginTop]);

  // Create the SVG container.
  const svg = d3.create("svg")
      .attr("width", width)
      .attr("height", height);

  // Add a rect for each bar.
  svg.append("g")
    .selectAll()
    .data(alphabet)
    .join("rect")
      .attr("x", (d) => x(d.letter))
      .attr("y", (d) => y(d.frequency))
      .attr("height", (d) => y(0) - y(d.frequency))
      .attr("width", x.bandwidth());

  // Add the x-axis.
  svg.append("g")
      .attr("transform", `translate(0,${height - marginBottom})`)
      .call(d3.axisBottom(x).tickSizeOuter(0));

  // Add the y-axis.
  svg.append("g")
      .attr("transform", `translate(${marginLeft},0)`)
      .call(d3.axisLeft(y));

  // Return the SVG element.
  return svg.node();
}
```

As a more complete example, try one of these starter templates:

* [Bar chart](https://observablehq.com/@d3/bar-chart/2?intent=fork)
* [Histogram](https://observablehq.com/@d3/histogram/2?intent=fork)

Observable includes a few D3 snippets when you click **+** to add a cell (type “d3” when the cell menu is open to filter), as well as convenient [sample datasets](https://observablehq.com/@observablehq/sample-datasets) to try out D3 features. Or upload a CSV or JSON file to start playing with your data. You can also fork any of the [hundreds of notebooks](https://observablehq.com/@d3?tab=notebooks) we’ve published for a head start.

Observable is free for public use. Sign up for a [Pro account](https://observablehq.com/pricing) to connect to private databases, collaborate on private notebooks, and more.

## D3 in vanilla HTML

In vanilla HTML, you can load D3 from a CDN such as jsDelivr or you can download it locally. We recommend using the CDN-hosted ES module bundle. But for those who need it, we also provide a UMD bundle that exports the `d3` global when loaded as a plain script.

:::code-group
```html [ESM + CDN]
<!DOCTYPE html>
<div id="container"></div>
<script type="module">

import * as d3 from "https://cdn.jsdelivr.net/npm/d3@7/+esm";

// Declare the chart dimensions and margins.
const width = 640;
const height = 400;
const marginTop = 30;
const marginRight = 0;
const marginBottom = 30;
const marginLeft = 40;

// Load the data.
const alphabet = await d3.csv("alphabet.csv");

// Declare the x (horizontal position) scale.
const x = d3.scaleBand()
    .domain(alphabet.map((d) => d.letter))
    .range([marginLeft, width - marginRight])
    .padding(0.1);

// Declare the y (vertical position) scale.
const y = d3.scaleLinear()
    .domain([0, d3.max(alphabet, (d) => d.frequency)])
    .range([height - marginBottom, marginTop]);

// Create the SVG container.
const svg = d3.create("svg")
    .attr("width", width)
    .attr("height", height);

// Add a rect for each bar.
svg.append("g")
  .selectAll()
  .data(alphabet)
  .join("rect")
    .attr("x", (d) => x(d.letter))
    .attr("y", (d) => y(d.frequency))
    .attr("height", (d) => y(0) - y(d.frequency))
    .attr("width", x.bandwidth());

// Add the x-axis.
svg.append("g")
    .attr("transform", `translate(0,${height - marginBottom})`)
    .call(d3.axisBottom(x).tickSizeOuter(0));

// Add the y-axis.
svg.append("g")
    .attr("transform", `translate(${marginLeft},0)`)
    .call(d3.axisLeft(y));

// Append the SVG element.
container.append(svg.node());

</script>
```

```html [UMD + CDN]
<!DOCTYPE html>
<div id="container"></div>
<script src="https://cdn.jsdelivr.net/npm/d3@7"></script>
<script type="module">

// Declare the chart dimensions and margins.
const width = 640;
const height = 400;
const marginTop = 30;
const marginRight = 0;
const marginBottom = 30;
const marginLeft = 40;

// Load the data.
const alphabet = await d3.csv("alphabet.csv");

// Declare the x (horizontal position) scale.
const x = d3.scaleBand()
    .domain(alphabet.map((d) => d.letter))
    .range([marginLeft, width - marginRight])
    .padding(0.1);

// Declare the y (vertical position) scale.
const y = d3.scaleLinear()
    .domain([0, d3.max(alphabet, (d) => d.frequency)])
    .range([height - marginBottom, marginTop]);

// Create the SVG container.
const svg = d3.create("svg")
    .attr("width", width)
    .attr("height", height);

// Add a rect for each bar.
svg.append("g")
  .selectAll()
  .data(alphabet)
  .join("rect")
    .attr("x", (d) => x(d.letter))
    .attr("y", (d) => y(d.frequency))
    .attr("height", (d) => y(0) - y(d.frequency))
    .attr("width", x.bandwidth());

// Add the x-axis.
svg.append("g")
    .attr("transform", `translate(0,${height - marginBottom})`)
    .call(d3.axisBottom(x).tickSizeOuter(0));

// Add the y-axis.
svg.append("g")
    .attr("transform", `translate(${marginLeft},0)`)
    .call(d3.axisLeft(y));

// Append the SVG element.
container.append(svg.node());

</script>
```

```html [UMD + local]
<!DOCTYPE html>
<div id="container"></div>
<script src="d3.js"></script>
<script type="module">

// Declare the chart dimensions and margins.
const width = 640;
const height = 400;
const marginTop = 30;
const marginRight = 0;
const marginBottom = 30;
const marginLeft = 40;

// Load the data.
const alphabet = await d3.csv("alphabet.csv");

// Declare the x (horizontal position) scale.
const x = d3.scaleBand()
    .domain(alphabet.map((d) => d.letter))
    .range([marginLeft, width - marginRight])
    .padding(0.1);

// Declare the y (vertical position) scale.
const y = d3.scaleLinear()
    .domain([0, d3.max(alphabet, (d) => d.frequency)])
    .range([height - marginBottom, marginTop]);

// Create the SVG container.
const svg = d3.create("svg")
    .attr("width", width)
    .attr("height", height);

// Add a rect for each bar.
svg.append("g")
  .selectAll()
  .data(alphabet)
  .join("rect")
    .attr("x", (d) => x(d.letter))
    .attr("y", (d) => y(d.frequency))
    .attr("height", (d) => y(0) - y(d.frequency))
    .attr("width", x.bandwidth());

// Add the x-axis.
svg.append("g")
    .attr("transform", `translate(0,${height - marginBottom})`)
    .call(d3.axisBottom(x).tickSizeOuter(0));

// Add the y-axis.
svg.append("g")
    .attr("transform", `translate(${marginLeft},0)`)
    .call(d3.axisLeft(y));

// Append the SVG element.
container.append(svg.node());

</script>
```
:::

If you’d prefer to run D3 locally (or entirely offline), you can download the UMD bundle of D3 here:

- <a href="./d3.v7.js" download>d3.v7.js</a>

Then, create an `index.html` file as shown above in the **UMD + local** tab. If you prefer smaller minified files, you can download <a href="./d3.v7.min.js" download>d3.v7.min.js</a> and then update the `src` attribute above accordingly.

## Installing from npm

If you’re developing a web application using Node, you can install D3 via yarn, npm, pnpm, or your preferred package manager.

:::code-group

```bash [yarn]
yarn add d3
```

```bash [npm]
npm install d3
```

```bash [pnpm]
pnpm add d3
```

:::

You can then load D3 into your app as:

```js
import * as d3 from "d3";
```

You can instead import specific symbols if you prefer:

```js
import {select, selectAll} from "d3";
```

Alternatively you can install and import from D3 submodules:

```js
import {mean, median} from "d3-array";
```

TypeScript declarations are available via DefinitelyTyped.

## D3 in React

TODO