## Collecting the data

- Read this first: [docs/journals/Week6.md](../docs/journals/Week6.md)
- [docs/journals](../docs/journals) (Week 1 – Week 6) shows how the data collection has changed over period.
- Weekday morning, **8:00–9:00**. Phase 1 is the first baseline. Phase 2 replaces it.

---

## Phase 1 — set aside

- Station 158, Gwarko East, 2024/25. This is Gwarko–Lakuri Bhanjyang, not the road to Koteshwor.
- The first route file still used these numbers because it wasn't previously known that this was Lakuri Bhanjyang data and not Koteshwor.

### Sources

| Source | What we took |
|--------|----------------|
| DoR Gwarko East (158), 2024/25. https://ssrn.dor.gov.np/traffic_controller/get_detail/Gwarko%20East/1516 | Hourly classified vehicle counts for two days (19 and 20 Jan 2025). Total volume, direction split (a/b columns), and vehicle types (motorcycle, car, tempo/three-wheeler, bus, etc.). This is our main number source. |
| Pradhananga et al. (2021), Jadibuti–Koteshwor | Same general corridor as ours. Used for morning direction pattern (heavier Jadibuti → Koteshwor in the morning), and for what to measure later (travel time, queue length, and not forgetting Tinkune as a downstream point). We are not copying their reversible-lane solution. |
| Shah, Chaudhary & Kaphle (2022), Kantipath | Vehicle mix for comparison: roughly 66%+ two-wheelers and about 90% private vehicles. Also their use of MAPE when comparing predicted vs observed flow — we keep that in mind for calibration after simulation. |
| Satdobato / Ring Road studies (Luitel et al.) | Nearby valley mix check. Confirms motorcycle-dominated traffic around the Ring Road system, similar order to what we see in DoR. |
| Poudyal & Shahi (2025) | Context: Koteshwor and Ring Road called out as bad congestion areas; private/motorcycle pressure and weak public transport. Helps explain why our mix is so private-heavy. |
| Chowdhury et al. (2024), Khulna | How to think about error after we run SUMO (RMSE on queue / travel time; starting car-following ideas). Not used for Kathmandu volume numbers. |
| Lopez et al. (2018) | Validation habits: compare simulated counts to targets; common rule of thumb that most counts should stay within ~15%. |
| Shrestha & Marsini | Local two-wheeler PCU ≈ 0.25 if we ever report PCU. For now we stay in vehicles/hour for SUMO. |
| JICA, Koteshwor–Tinkune, Feb 2019 | Volume-Capacity ratio (V/C) ≈ 2.22 on Koteshwor–Tinkune, Feb 2019, cited in reviews. Only as a reminder that this corridor is known to be oversaturated. Not used as our hourly count. |

### 8:00–9:00 volume

| Date | Both directions |
|------|----------------:|
| 19 Jan 2025 | 3,752 |
| 20 Jan 2025 | 3,225 |

- Mean: (3,752 + 3,225) / 2 = 3,488.5 ≈ **3,490 veh/h**.
- 19 Jan columns were 2,358 and 1,394, about **63% / 37%**.

### Vehicle composition

- Four-wheeler = car + utility + four-wheel drive. 
- Bus = big + mini + micro. 
- Other stays out of the four classes.

19 Jan 2025, 8:00–9:00:

| Class | Count | Share |
|-------|------:|------:|
| Two-wheeler | 2,867 | 76.4% |
| Four-wheeler | 623 | 16.6% |
| Tempo | 79 | 2.1% |
| Bus | 149 | 4.0% |
| Other | 34 | 0.9% |

- Checked against Kantipath (~66% two-wheelers) and Satdobato (~73%). We did not copy Kantipath.
- Baseline mix: **74% / 18% / 3% / 5%** → 2,583 / 628 / 105 / 174 out of 3,490.
- Private ≈ 92%. Public ≈ 8%.

---

## Phase 2 — 2025/26

- Source: [DoR traffic page](https://ssrn.dor.gov.np/traffic), year 2025/26.
- Replaced the 158 area because it's outside our corridor.
- The following three stations are the only government counts relevant to the Koteshwor corridor:

| Station | Where | Toward Koteshwor | Away | Days |
|---------|-------|------------------|------|------|
| **60** Ring Road (Manohara Bridge) | 100 m south of that bridge. Gwarko–Balkumari. | **B** Gwarko → Balkumari | **A** Balkumari → Gwarko | 22–24 Feb 2026 |
| **64** Manohara Bridge | 100 m east of the river, Araniko. Manohara–Sallaghari. | **A** Sallaghari → bridge | **B** bridge → Sallaghari | 22–24 Feb 2026 |
| **65** Sinamangal | At the Sinamangal intersection. Tinkune–Sinamangal–Gaushala. | **A** Gaushala → Sinamangal | **B** Sinamangal → Gaushala | 28–30 Apr 2026 |

### 8:00–9:00 data as presented on the website

| Station | From | To | Website | Morning 1 | Morning 2 | Mean |
|---------|------|----|---------|----------:|----------:|-----:|
| 60 | Gwarko | Balkumari | B, Gwarko → Balkumari | 2,426 | 2,645 | 2,535.5 |
| 60 | Balkumari | Gwarko | A, Balkumari → Gwarko | 1,769 | 1,878 | 1,823.5 |
| 64 | Sallaghari | Koteshwor | A, Sallaghari → Manohara Bridge | 5,031 | 5,546 | 5,288.5 |
| 64 | Koteshwor | Sallaghari | B, Manohara Bridge → Sallaghari | 2,107 | 1,830 | 1,968.5 |
| 65 | Sinamangal | Tinkune | A, Gaushala → Sinamangal | 1,294 | 1,087 | 1,190.5 |
| 65 | Sinamangal | Gaushala | B, Sinamangal → Gaushala | 2,227 | 2,399 | 2,313 |

### Composition

- Same two mornings, added, then divided by 2. 
- Two-wheeler = motorcycle. 
- Four-wheeler = car + utility + four-wheel drive. 
- Tempo = three-wheeler. 
- Bus = big + mini + micro.

| From | To | Vehicles | Two-wheeler | Four-wheeler | Tempo | Bus | Other |
|------|----|----------:|------------:|-------------:|------:|----:|------:|
| Gwarko | Balkumari | 2,535.5 | 1,463.5 (57.7%) | 813.5 (32.1%) | 23 (0.9%) | 165 (6.5%) | 70.5 (2.8%) |
| Balkumari | Gwarko | 1,823.5 | 909 (49.8%) | 676.5 (37.1%) | 5.5 (0.3%) | 175 (9.6%) | 57.5 (3.2%) |
| Sallaghari | Koteshwor | 5,288.5 | 3,967.5 (75.0%) | 960.5 (18.2%) | 0.5 (0%) | 288 (5.4%) | 72 (1.4%) |
| Koteshwor | Sallaghari | 1,968.5 | 1,166.5 (59.2%) | 494 (25.1%) | 0 | 257.5 (13.1%) | 50.5 (2.6%) |
| Sinamangal | Tinkune | 1,190.5 | 585 (49.1%) | 465.5 (39.1%) | 0 | 132 (11.1%) | 8 (0.7%) |
| Sinamangal | Gaushala | 2,313 | 1,541 (66.6%) | 661 (28.6%) | 0 | 98 (4.2%) | 13 (0.6%) |

- To show a demo of the above calculation, let's take one cell as an example.
- Koteshwor → Sallaghari, station 64.

| | 22 Feb | 23 Feb | Sum | ÷ 2 |
|--|-------:|-------:|----:|----:|
| Vehicles | 2,107 | 1,830 | 3,937 | 1,968.5 |
| Two-wheeler | 1,291 | 1,042 | 2,333 | 1,166.5 |
| Four-wheeler | 510 | 478 | 988 | 494 |
| Tempo | 0 | 0 | 0 | 0 |
| Bus | 259 | 256 | 515 | 257.5 |
| Other | 47 | 54 | 101 | 50.5 |

- 22 Feb four-wheeler: car 349 + utility 112 + four-wheel drive 49 = 510. Bus: big 31 + mini 122 + micro 106 = 259.
- 23 Feb four-wheeler: 331 + 96 + 51 = 478. Bus: 18 + 131 + 107 = 256.
- The reason for Tempo count being 0 for Bhaktapur and Sinamangal side is because Tempo only operates on Ring-Road and they are outside that range.

### Directional split

- Knowing vehicle composition and count is simply not enough.
- Since Koteshwor is a junction involving three different places, we have to know the to/from combinations for each.
- If we just define the above data for our .rou.xml, vehicles will start from Sallaghari and end at Koteshwor and that's it.
- The vehicles will randomly appear at Gwarko and magically disappear at Koteshwor.
- It won't take turns, it won't move to other directions which is the very source of traffic.
- We have to make vehicles move realistically for which we need to make vehicles move from Sallaghari to Tinkune/Gwarko side randomly.
- We don't have exact numbers, so we use our own assumption, and we have to triangulate the data.
- We have to take into consideration that it's our "assumption", hence there's a possibility that the data isn't going to be precise.
- Assuming:
i) The three toward-Koteshwor means all reach Koteshwor.
ii) No U-turn.
iii) Nobody enters from Tinkune (Koteshwor-Tinkune is one-way. The only way it could enter is from Sinamangal side which is already involved in the count. We couldn't find a separate Tinkune side data)

| Entries (toward Koteshwor) | Vehicles | Exits (away from Koteshwor) | Vehicles |
|---------|----------:|-------|----------:|
| Gwarko → Balkumari | 2,535.5 | Balkumari → Gwarko | 1,823.5 |
| Sallaghari → Koteshwor | 5,288.5 | Koteshwor → Sallaghari | 1,968.5 |
| Sinamangal → Tinkune | 1,190.5 | Sinamangal → Gaushala | 2,313 |
| **Sum** | **9,014.5** | **Sum** | **6,105** |

A vehicle that reaches Koteshwor also leaves it.

Entries: 2,535.5 + 5,288.5 + 1,190.5 = **9,014.5**

Exits: 1,823.5 + 1,968.5 + 2,313 = **6,105**

Tinkune has no count of its own. Assuming nobody enters from Tinkune, the vehicles that did not leave on the three counted roads leave toward Tinkune:

9,014.5 − 6,105 = **2,909.5**

Now, let's try to determine the from-to combinations for each.

The 1,968.5 leaving toward Bhaktapur did not come from Bhaktapur, and nothing entered from Tinkune. So they had to have come from Gwarko and/or Sinamangal.

(Gwarko → Balkumari) 2,535.5 + (Sinamangal → Tinkune) 1,190.5 = **3,726**

- Gwarko: 2,535.5 / 3,726 = **68.0%** → 1,968.5 × 68.0% = **1,339.5** 
- Sinamangal: 1,190.5 / 3,726 = **32.0%** → 1,968.5 × 32.0% = **629.0**

**A simple explanation of above calculation:**

- No U-turns means vehicles that went to Bhaktapur didn't come from Bhaktapur.
- So the vehicles could've only come from Sinamangal or/and Gwarko.
- We know from data that 1968.5 vehicles go to Bhaktapur. What we don't know is out of that 1968.5, what percentage is from Gwarko and/or Sinamangal?
- Based on total count of vehicles of Gwarko+Sinamangal, we know 68% of vehicles are from Gwarko in total, so 68% of 1968.5 is from Gwarko.
- This is just an assumption we've made to figure out the to-from data combinations.
- Each other exit is split the same way: shared by the entrances that did not come in on that road, in proportion to those entrance totals. The cells in a column add up to that exit. The cells in a row do not add back to that entrance.
- #Note: Previously, we took Sinamangal to Tinkune count as 1190.5 from website. In the table below, Sinamangal to Tinkune is shown as 384.2. Tinkune as a whole covers both Sinamangal and Baneshwor side. So while 1190.5 vehicles come from Sinamangal/Gaushala side to Tinkune/Koteshwor side, only 384.2 goes to the Tinkune/Baneshwor side based on our count.

| From \ To | Gwarko / Balkumari | Bhaktapur | Sinamangal | Tinkune(Baneshwor) | Row sum | Entered |
|-----------|-------------------:|----------:|-----------:|--------:|--------:|--------:|
| Gwarko / Balkumari | — | 1,339.5 | 749.6 | 818.4 | 2,907.5 | 2,535.5 |
| Bhaktapur | 1,488.4 | — | 1,563.4 | 1,706.9 | 4,758.7 | 5,288.5 |
| Sinamangal | 335.1 | 629.0 | — | 384.2 | 1,348.3 | 1,190.5 |
| Tinkune | 0 | 0 | 0 | — | 0 | 0 |

- Now let's try to find the composition of vehicles within that from-to count.
- A cell keeps the mix of the entrance it came from. 
- Gwarko → Bhaktapur is 1,339.5.
- Based on original vehicle composition, we know: Gwarko → Balkumari is 57.7% two-wheelers, 32.1% four-wheelers, 0.9% tempo, 6.5% bus, 2.8% other.

So,

- Two-wheeler: 1,339.5 × 57.7% = **772.9**
- Four-wheeler: 1,339.5 × 32.1% = **430.0**
- Tempo: 1,339.5 × 0.9% = **12.1**
- Bus: 1,339.5 × 6.5% = **87.1**
- Other: 1,339.5 × 2.8% = **37.5**

- Every other cell is that count times the mix of its own entrance. 
- Bhaktapur’s mix is 75.0 / 18.2 / 0 / 5.4 / 1.4. 
- Sinamangal’s is 49.1 / 39.1 / 0 / 11.1 / 0.7. 
- Other stays out of the route file. 

| From | To | Vehicles | Two-wheeler | Four-wheeler | Tempo | Bus | Other |
|------|----|----------:|------------:|-------------:|------:|----:|------:|
| Gwarko | Bhaktapur | 1,339.5 | 772.9 | 430.0 | 12.1 | 87.1 | 37.5 |
| Gwarko | Sinamangal | 749.6 | 432.5 | 240.6 | 6.7 | 48.7 | 21.0 |
| Gwarko | Tinkune | 818.4 | 472.2 | 262.7 | 7.4 | 53.2 | 22.9 |
| Bhaktapur | Gwarko | 1,488.4 | 1,116.3 | 270.9 | 0 | 80.4 | 20.8 |
| Bhaktapur | Sinamangal | 1,563.4 | 1,172.5 | 284.5 | 0 | 84.4 | 21.9 |
| Bhaktapur | Tinkune | 1,706.9 | 1,280.2 | 310.7 | 0 | 92.2 | 23.9 |
| Sinamangal | Gwarko | 335.1 | 164.5 | 131.0 | 0 | 37.2 | 2.3 |
| Sinamangal | Bhaktapur | 629.0 | 308.8 | 245.9 | 0 | 69.8 | 4.4 |
| Sinamangal | Tinkune | 384.2 | 188.6 | 150.2 | 0 | 42.6 | 2.7 |

### Verifying our from-to composition

Let's test data going to Gwarko.

From above table based on our assumption against real data:
- Bhaktapur → Gwarko, two-wheeler column: 1,116.3
- Sinamangal → Gwarko, two-wheeler column: 164.5
- 1,116.3 + 164.5 = **1,280.8 two-wheelers**

The actual site data:
 **909 two-wheelers**

Same for others:

| Exit | | Two-wheeler | Four-wheeler | Tempo | Bus | Other |
|------|--|------------:|-------------:|------:|----:|------:|
| Balkumari → Gwarko | Counted | 909 | 676.5 | 5.5 | 175 | 57.5 |
| | From our cells | 1,280.8 | 401.9 | 0 | 117.6 | 23.2 |
| | Difference | +371.8 | −274.6 | −5.5 | −57.4 | −34.3 |
| Koteshwor → Sallaghari | Counted | 1,166.5 | 494 | 0 | 257.5 | 50.5 |
| | From our cells | 1,081.7 | 675.9 | 12.1 | 156.9 | 41.9 |
| | Difference | −84.8 | +181.9 | +12.1 | −100.6 | −8.6 |
| Sinamangal → Gaushala | Counted | 1,541 | 661 | 0 | 98 | 13 |
| | From our cells | 1,605.1 | 525.2 | 6.7 | 133.1 | 42.9 |
| | Difference | +64.1 | −135.8 | +6.7 | +35.1 | +29.9 |

- The vehicle totals match: 1,488.4 + 335.1 = 1,823.5. The types do not. Our cells put 70.2% two-wheelers on that exit. The site counted 49.8%.
- This discrepancy exists because there's no way to know for certain which vehicle turns where.
- We can try to align the vehicle count (which we did), but we can't pinpoint the composition without falling into the rabbithole
- This is simply a margin of error.
- This is the data we'll be proceeding with for our simulation.

**Final rounded-off table for .rou.xml**

| From | To | Vehicles | Two-wheeler | Four-wheeler | Tempo | Bus |
|------|----|----------:|------------:|-------------:|------:|----:|
| Gwarko | Bhaktapur | 1,302 | 773 | 430 | 12 | 87 |
| Gwarko | Sinamangal | 730 | 433 | 241 | 7 | 49 |
| Gwarko | Tinkune | 795 | 472 | 263 | 7 | 53 |
| Bhaktapur | Gwarko | 1,467 | 1,116 | 271 | 0 | 80 |
| Bhaktapur | Sinamangal | 1,542 | 1,173 | 285 | 0 | 84 |
| Bhaktapur | Tinkune | 1,683 | 1,280 | 311 | 0 | 92 |
| Sinamangal | Gwarko | 333 | 165 | 131 | 0 | 37 |
| Sinamangal | Bhaktapur | 625 | 309 | 246 | 0 | 70 |
| Sinamangal | Tinkune | 382 | 189 | 150 | 0 | 43 |
