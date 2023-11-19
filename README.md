# 🏳️‍🌈 LGBT pride

LGBT pride via github languages list

![image](https://github.com/Vendicated/gay/assets/45497981/4f5a0f42-56bf-4cea-8f04-498db315bfb5)


Inspired by https://github.com/spacekookie/gay

Unfortunately, spacekookie's repo broke, because the OCaml language colour was changed.
Thus, i decided to make my own variant and make the colours as close to the original flag as possible.


<details>
<summary>To find the closest coloured languages, i wrote this incredibly shitty script</summary>
  
based on https://gist.github.com/Ademking/560d541e87043bfff0eb8470d3ef4894

```js
const linguistYaml = await fetch("https://raw.githubusercontent.com/github-linguist/linguist/master/lib/linguist/languages.yml").then(r => r.text());
const baseColors = Array.from(
    linguistYaml.matchAll(/(^[^\n:]+):\n  type: programming\n  color: "(#\w{6})"/gm),
    ([, name, hex]) => ({ name, hex }));

function hexToRgb(hex) {
    var shorthandRegex = /^#?([a-f\d])([a-f\d])([a-f\d])$/i;
    hex = hex.replace(shorthandRegex, function (m, r, g, b) {
        return r + r + g + g + b + b;
    });

    var result = /^#?([a-f\d]{2})([a-f\d]{2})([a-f\d]{2})$/i.exec(hex);
    return result ? {
        r: parseInt(result[1], 16),
        g: parseInt(result[2], 16),
        b: parseInt(result[3], 16)
    } : null;
}

// Distance between 2 colors (in RGB)
// https://stackoverflow.com/questions/23990802/find-nearest-color-from-a-colors-list
function distance(a, b) {
    return Math.sqrt(Math.pow(a.r - b.r, 2) + Math.pow(a.g - b.g, 2) + Math.pow(a.b - b.b, 2));
}

// return nearest color from array
function nearestColor(colorHex) {
    var lowest = Number.POSITIVE_INFINITY;
    var tmp;
    let index = 0;
    baseColors.forEach((el, i) => {
        tmp = distance(hexToRgb(colorHex), hexToRgb(el.hex));
        if (tmp < lowest) {
            lowest = tmp;
            index = i;
        };

    });
    return baseColors[index];

}

const LgbtColors = [
    {
        name: "Red",
        hex: "#E40303",
    },
    {
        name: "Orange",
        hex: "#FF8C00"
    },
    {
        name: "Yellow",
        hex: "#FFED00"
    },
    {
        name: "Green",
        hex: "#008026"
    },
    {
        name: "Blue",
        hex: "#24408E",
    },
    {
        name: "Purple",
        hex: "#732982"
    }
];

for (const { name, hex } of LgbtColors) {
    console.log(`${name} -> ${nearestColor(hex).name}`);
}
```

</details>
