---
theme: dashboard
toc: false
---

# Sales

```js
const data = await FileAttachment("./data/video-game-sales-data.json").json();
const categories = data.children.map(d => d.name);
```

```js
const categoriesFilter = view(
  Inputs.select(
  categories,
  {value: categories[0], label: "Platform"}
));
```

```js
const salesFilter = view(Inputs.range(
    [7.39, 82.53],
    {value: 7.39, step: 0.1, label: "Sales (M)"}
));
```

```js
function salesPlot(data, {width} = {}) {
    const height = 600;

    const root = d3.hierarchy(data)
        .sum(d => d.value)
        .sort((a, b) => b.value - a.value);

    d3.treemap()
        .size([width, height])
        .padding(1)
        (root);

    const leaves = root.leaves().filter(d => d.data.category == categoriesFilter && d.data.value >= salesFilter);

    return Plot.plot({
        marks: [
            Plot.rect(leaves, {
                x1: "x0",
                x2: "x1",
                y1: "y0",
                y2: "y1",
                fill: d => d.data.name,
                fillOpacity: 0.6,
                title: d => `${d.data.name}\n${d.data.value}M`,
            }),
            Plot.text(leaves, {
                x: d => (d.x0 + d.x1) / 2,
                y: d => (d.y0 + d.y1) / 2,
                text: d => `${d.data.name}\n${d.data.value}M`,
                textAnchor: "middle",
            })
        ],
        x: { axis: null },
        y: { axis: null },
        width: width,
        height: height,
    });
}
```

<div class="grid grid-cols-1">
  <div class="card">
    ${resize((width) => salesPlot(data, {width}))}
  </div>
</div>
