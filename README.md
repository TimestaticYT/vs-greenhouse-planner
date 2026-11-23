# Vintage Story Greenhouse Planner

A planting calendar for greenhouses in [Vintage Story](https://www.vintagestory.at/), built for game version 1.22.

**Open it:** https://timestaticyt.github.io/vs-greenhouse-planner/

## What it does

- Shows, for every planting day of the year, whether a crop gets a full harvest, takes cold or heat damage, or dies.
- Lets you switch the greenhouse bonus (+5 °C) on or off per month, for when you open the roof in summer.
- Plans a four-greenhouse rotation (N → P → K → rest) where all houses are harvested together once the slowest crop is ripe.
- Lists what you can plant on a given in-game day, and plans a single shelf for a year.
- Switches between English and German (EN/DE, top right). German crop names match the game's German language file.

## Using it with your world

Stand where your crops are and run:

```
/wgen pos climate
/wgen pos latitude
```

Enter the **Year avg** temperature, **Avg. Rainfall** and the latitude. Everything updates right away. Your settings are saved in your browser and are still there when you come back. If you farm in more than one place, add a location with **New** and switch between them with the **Location** menu; each location keeps its own settings.

## How it works

The temperature model is the game's own formula from `Systems/Temperature.cs` in vssurvivalmod: a seasonal swing of latitude/90 × 65 °C, coldest in mid-January in the north, and a day/night swing of 18 − 13 × rainfall °C, coldest at 4:00. The game's random weather noise is not simulated; the safety margin setting stands in for it.

Crop limits, growth times, nutrient use and yields come from the 1.22 game assets. Damage and growth follow the farmland code. Each check below the cold limit or above the heat limit cuts the harvest to 50 % (75 % for carrot, parsnip, rye and fennel), 48 hours of damage kills the crop, and growth slows by 10 % per degree below 10 °C.

Soil fertility (very low to high) is a setting: it changes how fast crops grow, and the rotation and shelf plan track each soil's nutrient levels from one crop to the next.

Not modelled: fertilizer, light and watering.

It's a single static `index.html` with no build step.
