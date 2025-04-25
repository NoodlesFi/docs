---
icon: plug-circle-plus
---


# Noodles TV Widget

Easily embed a real-time trading view widget from [Noodles.fi](https://noodles.fi) into your website or application. This widget supports both **single coin** and **coin pair** visualizations with light or dark themes.

---

## Features

- Real-time ohlc chart visualization  
- Supports **single coin** and **trading pairs**  
- Toggle between **light** and **dark** themes  
- Simple integration using `<iframe>`

---

## 1. Single Coin Widget

Displays a real-time chart for a single coin.

**URL Format:**
```
https://noodles.fi/tv-widget?coin=<COIN_ID>&theme=<light|dark>
```

**Parameters:**

| Name    | Required | Description                                  |
|---------|----------|----------------------------------------------|
| `coin`  | True     | Full unique identifier of the coin (ID)      |
| `theme` | False    | `light` (default) or `dark` UI theme         |

**Example:**

[stSUI OHLC](https://noodles.fi/tv-widget?coin=0xd1b72982e40348d069bb1ff701e634c117bb5f741f44dff91e472d3b01461e55::stsui::STSUI&theme=dark)


```html
<iframe
  src="https://noodles.fi/tv-widget?coin=0xd1b72982e40348d069bb1ff701e634c117bb5f741f44dff91e472d3b01461e55::stsui::STSUI&theme=dark"
  width="100%"
  height="500"
  frameborder="0"
  allowfullscreen>
</iframe>
```

---

## 2. Pair coin Widget

Visualizes a trading pair chart between two coins.

**URL Format:**
```
https://noodles.fi/tv-widget?coinA=<COIN_A_ID>&coinB=<COIN_B_ID>&theme=<light|dark>
```

**Parameters:**

| Name     | Required | Description                                  |
|----------|----------|----------------------------------------------|
| `coinA`  | True     | Identifier of the **base** coin              |
| `coinB`  | True     | Identifier of the **quote** coin             |
| `theme`  | False    | `light` (default) or `dark` theme            |


**Example:**

[DEEP/SUI](https://noodles.fi/tv-widget?coinA=0xdeeb7a4662eec9f2f3def03fb937a663dddaa2e215b8078a284d026b7946c270::deep::DEEP&coinB=0x0000000000000000000000000000000000000000000000000000000000000002::sui::SUI&theme=dark)

```html
<iframe
  src="https://noodles.fi/tv-widget?coinA=0xdeeb7a4662eec9f2f3def03fb937a663dddaa2e215b8078a284d026b7946c270::deep::DEEP&coinB=0x0000000000000000000000000000000000000000000000000000000000000002::sui::SUI&theme=dark"
  width="100%"
  height="500"
  frameborder="0"
  allowfullscreen>
</iframe>
```

---

## Contact for help

If you encounter any issues or have feature requests, feel free to reach out [@PurrrPurrr12](https://t.me/PurrrPurrr12) or [@hiephho](https://t.me/hiephho).