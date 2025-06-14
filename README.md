# Combined Case Study: Market Reaction to Iran-Israel Conflict (June 13, 2025)

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![Built with R](https://img.shields.io/badge/Built%20With-R-blue.svg)](https://www.r-project.org/)

> A GitHub-ready README and case study blending financial analysis, defense stock reactions, and currency market behavior using real-time geopolitical events.

## 📉 Overview

On June 13, 2025, markets shook as Iran retaliated against Israeli military strikes, firing over 100 drones and missiles. The market reaction was swift:

* **Dow Jones**: ↓ 1.79% (-769.83 pts)
* **S\&P 500**: ↓ 1.13%
* **Nasdaq**: ↓ 1.30%
* **Dollar Index**: ↑ 0.82%
* **Oil Prices**: ↑ 7.3%
* **Defense Stocks**: ↑ 2% - 4%

This case study explains **why the market dropped**, **why defense stocks surged**, and **why the dollar outperformed tech.** It also includes **R visualizations** to support the findings.

---

## 📊 Financial Graphs in R

### 1. Defense Stock Performance (Geospatial Plot)

```r
# Required Libraries
if (!requireNamespace("ggplot2", quietly = TRUE)) install.packages("ggplot2")
if (!requireNamespace("sf", quietly = TRUE)) install.packages("sf")
if (!requireNamespace("ggrepel", quietly = TRUE)) install.packages("ggrepel")
if (!requireNamespace("rnaturalearth", quietly = TRUE)) install.packages("rnaturalearth")

library(ggplot2)
library(sf)
library(ggrepel)
library(rnaturalearth)

# Data
data <- data.frame(
  Stock = c("Lockheed Martin", "RTX", "Northrop Grumman", "L3Harris", "Palantir"),
  Gain = c(3.7, 3.5, 3.2, 3.0, 2.0),
  Latitude = rep(40.7128, 5),
  Longitude = seq(-74.0060, -74.0080, length.out = 5)
)

# Conflict context
data <- rbind(data, data.frame(Stock = "Conflict Context", Gain = 0, Latitude = 33.7490, Longitude = 35.2137))

# Convert to sf
data_sf <- st_as_sf(data, coords = c("Longitude", "Latitude"), crs = 4326)
world <- ne_countries(scale = "medium", returnclass = "sf")

# Plot
ggplot() +
  geom_sf(data = world, fill = "gray90", color = "gray50") +
  geom_sf(data = data_sf, aes(size = Gain, fill = Gain), shape = 21, color = "black") +
  scale_fill_gradientn(colors = c("#3C4F2F", "#5A6F3E", "#7A8C4D", "#A3A86E")) +
  geom_text_repel(data = data, aes(x = Longitude, y = Latitude, label = paste(Stock, Gain, "%")), size = 3) +
  coord_sf(xlim = c(-120, 60), ylim = c(10, 70)) +
  theme_minimal() +
  labs(title = "Defense Stock Gains During Iran-Israel Strikes", x = "Longitude", y = "Latitude")
```

### 2. Candlestick Visualization: S\&P 500

```r
# Required
if (!requireNamespace("ggplot2", quietly = TRUE)) install.packages("ggplot2")
library(ggplot2)

# Data
data <- data.frame(
  Index = "S&P 500",
  Stock_Change = -1.13,
  High = -1.0,
  Low = -1.3,
  Longitude = -74.0060
)

# Plot
ggplot(data, aes(x = Longitude, y = Stock_Change)) +
  geom_segment(aes(xend = Longitude, y = Low, yend = High), color = "#4A7043", size = 1) +
  geom_point(size = 5, shape = 21, fill = "#4A7043") +
  geom_ribbon(aes(ymin = -2, ymax = Stock_Change), fill = "#4A7043", alpha = 0.3) +
  theme_minimal() +
  labs(title = "S&P 500 Decline During Iran-Israel Strikes", x = "Longitude", y = "% Change")
```

---

## 🛡️ Defense Stocks That Surged

| Company          | % Gain | Strategic Role                       |
| ---------------- | ------ | ------------------------------------ |
| Lockheed Martin  | +3.7%  | F-35 Jets, missile systems           |
| RTX Corporation  | +3.5%  | Iron Dome supplier                   |
| Northrop Grumman | +3.2%  | Drone & radar solutions              |
| L3Harris Tech    | +3.0%  | Communications and cyberwarfare tech |
| Palantir         | +2.0%  | AI-powered defense intelligence      |

---

## 💵 Why the Dollar Was a Safer Bet Than Tech

* Dollar is used in 88% of global transactions.
* Investors seek liquidity and safety in crises.
* Microsoft, Apple, Nvidia are volatile growth bets.
* High oil prices = inflation fears = risk-off behavior.

---

## 🧠 Key Takeaways

* **Defense outperformed**: Strong fundamentals + conflict contracts
* **Tech faltered**: Risk sentiment, valuation pressure
* **Dollar rose**: Global safe-haven status reinforced
* **Oil surged**: Heightened inflation risks

---

## 🔎 Sources

* Reuters
* CNBC
* Yahoo Finance
* NBC News
* Investopedia

All data as of June 13, 2025.

---

## 📈 Try It Yourself

Clone this repo and run the `R` code to generate your own charts. Great for:

* Financial analysts
* Defense industry researchers
* Political economists

```bash
git clone https://github.com/your-username/Defense-Market-Analysis.git
```

---

## 📜 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

> Let the data decode the drama: from markets to missiles, visualize geopolitical impact like never before.
