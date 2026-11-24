# Vintage Story Greenhouse Planner

A planting calendar for greenhouses in [Vintage Story](https://www.vintagestory.at/), built for game version 1.22.

**Open it:** https://timestaticyt.github.io/vs-greenhouse-planner/

## What it does

- Shows, for every planting day of the year, whether a crop gets a full harvest, takes cold or heat damage, or dies.
- Lets you switch the greenhouse bonus (+5 °C) on or off per month, for when you open the roof in summer.
- Plans a four-greenhouse rotation (N → P → K → rest) where all houses are harvested together once the slowest crop is ripe.
- Each house can follow the roof months, stay a greenhouse all year, or be an open field, and "Suggest roof months" finds which months to keep the roof closed and when to open it for the most food.
- Lists what you can plant on a given in-game day, and plans a single field that you replant all year.
- Compares every crop's food per block per day at each soil fertility.
- Plans only with the crops you have. Optionally, enter your seed stock and field sizes: the rotation then plants as many blocks as you have seeds, fills spare blocks with another crop, and counts the seeds you get back (1.2 per ripe block on average).
- On the Hunger tab: list your players (or groups of similar players), each with class, share of time online and activity level. The planner works out how much the group eats in an in-game year from the game's hunger code, including the blackguard's 30 % faster hunger, and compares it with your harvest in a bar.
- Every section can be collapsed, and the page remembers which ones you closed.
- Flax for linen and windmill sails: set how much of the K house grows flax instead of food, up to the whole house. The Hunger tab recommends a share that keeps at least 25 % spare food.
- Food groups: the game gives +2.5 max health per full food group (fruit, vegetable, protein, grain, dairy). The Hunger tab compares your harvest per group with what keeps each group full, and the rotation can be told to fill every group first.
- Food from outside the fields: tell the planner how much of all food, and of each food group, comes from meat, fish, fruit trees, foraging or trading. The fields then only have to cover the rest.
- Shares setups and backs them up: export any of your locations and your group settings into one small file. Importing shows what a file holds; you pick which locations to take (added as a copy or replacing yours of the same name) and whether the group replaces yours or its players are added to your list.
- Switches between English and German (EN/DE, top right). German crop names match the game's German language file.

## Using it with your world

Stand where your crops are and run:

```
/wgen pos climate
/wgen pos latitude
```

Enter the **Year avg** temperature, **Avg. Rainfall** and the latitude. Everything updates right away.

No admin rights? `/wgen` needs them. Open **No admin rights? Set up the climate from temperature readings** and enter a few outside temperatures with the in-game date and hour: two on one day (around 4:00 and 16:00), and two more in another season. The planner fits the game's temperature formula to them. Your settings are saved in your browser and are still there when you come back. If you farm in more than one place, add a location with **New** and switch between them with the **Location** menu; each location keeps its own settings.

## How it works

The temperature model is the game's own formula from `Systems/Temperature.cs` in vssurvivalmod: a seasonal swing of latitude/90 × 65 °C, coldest in mid-January in the north, and a day/night swing of 18 − 13 × rainfall °C, coldest at 4:00. The game's random weather noise is not simulated. Instead you can measure your world's current offset: enter the temperature from `/wgen pos climate` and the in-game hour, and the planner works out how far the weather currently is from the formula. The safety margin covers the rest.

Crop limits, growth times, nutrient use and yields come from the 1.22 game assets. Damage and growth follow the farmland code. Each check below the cold limit or above the heat limit cuts the harvest to 50 % (75 % for carrot, parsnip, rye and fennel), 48 hours of damage kills the crop, and growth slows by 10 % per degree below 10 °C.

Soil fertility (very low to high) is a setting: it changes how fast crops grow, and the rotation and shelf plan track each soil's nutrient levels from one crop to the next.

Not modelled: fertilizer, light and watering.

It's a single static `index.html` with no build step.
