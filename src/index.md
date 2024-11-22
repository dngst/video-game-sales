---
toc: false
---

```js
const data = await FileAttachment("./data/video-game-sales-data.json").json();
const categories = data.children.map(d => d.name);
const videoGamesCount = data.children.reduce((acc, d) => acc + d.children.length, 0);
const totalSales = data.children.reduce((acc, d) => acc + d3.sum(d.children, c => c.value), 0);
```

<div class="hero">
  <h1>Video Game Sales</h1>
  <h2>Explore video game sales by platform</h2>
</div>

<div class="grid grid-cols-2">
  <div class="card">
    <h2>Platforms</h2>
    <span class="big">${categories.length}</span>
  </div>
  <div class="card">
    <h2>Video Games</span></h2>
    <span class="big">${videoGamesCount}</span>
  </div>
</div>

<div class="card">
  <h2>Total Sales (M)</span></h2>
  <span class="big">${Math.round(totalSales)}</span>
</div>

<style>

.hero {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: var(--sans-serif);
  margin: 4rem 0 8rem;
  text-wrap: balance;
  text-align: center;
}

.hero h1 {
  margin: 1rem 0;
  padding: 1rem 0;
  max-width: none;
  font-size: 14vw;
  font-weight: 900;
  line-height: 1;
  background: linear-gradient(30deg, var(--theme-foreground-focus), currentColor);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero h2 {
  margin: 0;
  max-width: 34em;
  font-size: 20px;
  font-style: initial;
  font-weight: 500;
  line-height: 1.5;
  color: var(--theme-foreground-muted);
}

@media (min-width: 640px) {
  .hero h1 {
    font-size: 90px;
  }
}

</style>
