### Example LLM Prompt: Investigating Midwinter in January

I would like to develop a regional rule set for automatically detecting meteorological singularities. As an example, we will investigate **midwinter in January**.

**Region:** [Country, region, location or coordinates]

Proceed as follows:

1. **Meteorological background:** Investigate whether my region has a known, regularly recurring period of midwinter weather in January. Explicitly distinguish between midwinter, late winter and a possible return of winter weather in March. These may have different meteorological causes, time windows and characteristics and must not be combined into a single cold spell. Consider regional weather traditions, scientific studies and possible changes due to climate change. Distinguish traditional assumptions from statistically demonstrated weather patterns.

2. **Historical weather data:** Retrieve data for the last 20 to 30 complete winters through Open-Meteo's Historical Weather API. Use a consistent data source wherever possible. Examine temperature trends, cold spells and any other relevant weather variables in particular.

3. **Statistical analysis:** Determine whether a characteristic period with an increased frequency of cold events can be demonstrated within January. Compare it with the neighbouring winter weeks and also examine developments within the period under investigation. If no robust pattern is discernible, state this explicitly.

4. **Detection rules:** Derive suitable calendar windows, thresholds and conditions from the results to detect the weather pattern using current weather forecasts. Avoid unnecessarily complicated rules and rules fitted merely to individual historical events. Where possible, test the rules against years not previously used for their development.

5. **Results and documentation:** State the period examined, the data used, the frequency of the pattern and the results of testing the rules. Briefly explain how reliable the detection appears to be and what uncertainties remain.

6. **JSON event set:** Create a regional module for *Gordon's Weather Analysis* from the results. Use only the structure and available conditions of the attached example mod. Do not invent new JSON fields or evaluation functions. If the format is missing or a required condition is not supported, ask before creating the JSON.

**Important:** Use only weather data that has actually been retrieved. Do not invent measurements or statistical results. If you cannot access the historical data, explain how we can obtain it and then analyse it together.

Begin with a meteorological assessment of midwinter in my region. Develop the event set only after the historical analysis.
