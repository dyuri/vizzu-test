# Testing Vizzu

## Notes / wishes

- npm installable
- CSV input
- [/] consturctor should accept not only `id` (string) but actual HTML element as well
- [*] `vizzu-chart` web component
- [/] why do you need the init callback? using a promise here (or an option at least) will be much nicer
  - especially the `chart` in the callback, it's not explicitly passed to the callback, but visible only due to JS scope
- CSS variable support for styling (via JS API) (easy dark/light mode switch, or themes)

```javascript
const el = document.getElementById("myVizzu"); // no idea how to get it from the `chart` object, would be nice
const styles = window.getComputedStyle(el);

styles.getPropertyValue("--plot-marker-label-position"); // style: { plot: { marker: { label: { position: "whatever"}}}}
```

- [/] `chart.animate` returns a promise (which is fine) that resolves to `undefined`, it should resolves to the `chart` object itself, to make it easily chainable without relying on the global scope/namespace
- for me `data` is kind of turned inside out, in my head I have data points with properties, and not list of properties with a list of values that are related to eachother (this is also the case for simple CSV => JSON mapping)

```javascript
// Vizzu:
{
  series: [ // why do even need this? there's always only one series property, is there anything else?
    { name: 'A', type: 'categories', values: ["2018", "2019", "2020"] },
    { name: 'B', type: 'values': values: [1, 2, 3] }
    { name: 'C', type: 'values': values: [3, 2, 1] }
  ]
}

// me:
{
  types: {
    categories: ["A"],
    values: ["B", "C"]
  }
  series: [
    { A: "2018", B: 1, C: 3 },
    { A: "2019", B: 2, C: 2 },
    { A: "2020", B: 3, C: 1 }
  ]
}
```
