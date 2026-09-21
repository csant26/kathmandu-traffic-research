## Collecting the data

Since primary data collection at Koteshwor itself wasn’t fully possible for us (site access, filming the main junction safely), we shifted to secondary sources. The idea was not to invent numbers, but to take what already exists from the government and from papers close to our corridor, then check whether those numbers look consistent with each other.

We focused on weekday morning peak, mainly **8:00–9:00 AM**, because that is the period we want to simulate later in SUMO.

---

### Sources

| Source | What we took from it |
|--------|----------------------|
| Department of Roads (DoR) HMIS / SSRN — Gwarko East station (Station No. 158), year 2024/25. Link: https://ssrn.dor.gov.np/traffic_controller/get_detail/Gwarko%20East/1516 | Hourly classified vehicle counts for two days (19 and 20 Jan 2025). Total volume, direction split (a/b columns), and vehicle types (motorcycle, car, tempo/three-wheeler, bus, etc.). This is our main number source. |
| Pradhananga et al. (2021) — *Effectiveness of Reversible Lane Systems… Jadibuti–Koteshwor* (and related write-ups of the same corridor) | Same general corridor as ours. Used for morning direction pattern (heavier Jadibuti → Koteshwor in the morning), and for what to measure later (travel time, queue length, and not forgetting Tinkune as a downstream point). We are **not** copying their reversible-lane solution. |
| Shah, Chaudhary & Kaphle (2022) — Kantipath, BIBECHANA | Vehicle mix for comparison: roughly 66%+ two-wheelers and about 90% private vehicles. Also their use of MAPE when comparing predicted vs observed flow — we keep that in mind for calibration after simulation. |
| Satdobato / Ring Road intersection studies (e.g. Luitel et al. and related VISSIM papers citing ~73% motorcycle) | Nearby valley mix check. Confirms motorcycle-dominated traffic around the Ring Road system, similar order to what we see in DoR. |
| Poudyal & Shahi (2025) — EASTS paper on public transport / congestion in Kathmandu | Context: Koteshwor and Ring Road called out as bad congestion areas; private/motorcycle pressure and weak public transport. Helps explain why our mix is so private-heavy. |
| Chowdhury et al. (2024) — Khulna SUMO calibration | How to think about error after we run SUMO (RMSE on queue / travel time; starting car-following ideas). Not used for Kathmandu volume numbers. |
| Lopez et al. (2018) — Microscopic traffic simulation using SUMO | Validation habits: compare simulated counts to targets; common rule of thumb that most counts should stay within ~15%. |
| Shrestha & Marsini (PCU work at Koteshwor, Tinkune, Jadibuti — cited in Kathmandu intersection reviews) | Local two-wheeler PCU ≈ 0.25 if we ever report PCU. For now we stay in vehicles/hour for SUMO. |
| JICA corridor figure (V/C ≈ 2.22 on Koteshwor–Tinkune, Feb 2019 — cited in reviews) | Only as a reminder that this corridor is known to be oversaturated. Not used as our hourly count. |

**Note on Gwarko East:** it is not the Koteshwor stop line. It is the closest official classified hourly station we could use in the same valley / Ring Road setting. We treat it as a **proxy** for scale, then we will calibrate the simulation against queue behaviour we know from commuting the corridor.

---

### Morning volume (8:00–9:00 AM)

From the DoR Gwarko East detail page (2024/25 counts), total vehicles in the 8–9 AM hour:

| Date | 8:00–9:00 AM total (veh/h, both directions) |
|------|-----------------------------------------------|
| 19 Jan 2025 | 3,752 |
| 20 Jan 2025 | 3,225 |

Taking the mean:

$$
\frac{3752 + 3225}{2} = 3488.5 \approx 3490 \text{ veh/h}
$$

So for our study we take **about 3,490 vehicles per hour** as the design-hour volume (both directions combined).

For context, the same station on those two days also shows roughly:

| Hour | Two-day mean (approx.) |
|------|-------------------------|
| 7:00–8:00 | ~2,569 |
| **8:00–9:00** | **~3,490** ← we use this |
| 9:00–10:00 | ~4,017 |

9 AM can be even higher at this station, but we stick to 8–9 AM because that matches the morning peak window we chose for the paper.

---

### Day-to-day variation (error on the secondary count)

The two official mornings are not identical. Relative to the mean:

$$
\frac{|3752 - 3225|}{3490} \times 100\% \approx 15.1\%
$$

So even before simulation, we already know the government hour can swing around **±15%** day to day. We will treat 3,490 as a working value inside that band, not as an exact Koteshwor count.

After we build the SUMO baseline, we will also check volume match with the usual scores from the literature (GEH, and MAPE if needed).

---

### Directional split (morning)

On 19 Jan 2025, 8–9 AM, DoR’s two direction columns were about **2,358** and **1,394** (total 3,752). That is roughly **63% / 37%**.

That fits what the Jadibuti–Koteshwor papers say: morning is heavier toward Koteshwor / the city side. We lock:

| Direction (morning) | Share | Vehicles out of 3,490 |
|---------------------|-------|------------------------|
| Toward Tinkune / Kathmandu | 63% | ~2,199 |
| Opposite direction | 37% | ~1,291 |

---

### Vehicle composition

We only keep four classes for the study (enough for public vs private, and for a bus-priority scenario later):

- **Two-wheeler** — motorcycle / scooter (private)  
- **Four-wheeler** — car, jeep, van, taxi, pickup (private)  
- **Tempo** — three-wheeler / tyampo (public)  
- **Bus** — mini, micro, and large bus (public)  

Trucks and similar were under about 1% in the DoR morning hour we checked, so we did not make a separate class for them.

#### What DoR showed (8:00–9:00, 19 Jan 2025)

After grouping DoR’s categories into our four classes:

| Class | Approx. count | Share of that hour |
|-------|---------------|--------------------|
| Two-wheeler | 2,867 | ~76.4% |
| Four-wheeler | 623 | ~16.6% |
| Tempo | 79 | ~2.1% |
| Bus (big + mini + micro) | 149 | ~4.0% |
| Other (folded away) | 34 | ~0.9% |

#### What we finally use

We rounded and adjusted slightly after comparing with other Kathmandu sources (see below):

| Class | Locked share | Vehicles if total = 3,490 |
|-------|--------------|---------------------------|
| Two-wheeler | **74%** | ~2,583 |
| Four-wheeler | **18%** | ~628 |
| Tempo | **3%** | ~105 |
| Bus | **5%** | ~174 |

So private is about **92%** (two-wheeler + four-wheeler) and public about **8%** (tempo + bus).

#### Why this mix is adjusted ?

From the government’s Gwarko East hour, two-wheelers are clearly the majority (~76% before rounding). That is in the same ballpark as Satdobato-type Ring Road results (~73% motorcycle). Kantipath is a different corridor but still shows two-wheelers above ~66% and private vehicles around ~90%, which is the same overall story even if the exact percent is lower than ours. Poudyal & Shahi also point to motorcycle pressure around places like Koteshwor.

We did **not** copy Kantipath’s 66% as our design mix, because our main classified count is DoR. We used Kantipath / Satdobato as a check: if DoR had said something wild like “20% motorcycle,” we would have been suspicious. It didn’t.

Working mix for simulation: **74% / 18% / 3% / 5%**.

---

### Overall data prep for our model later

| Item | Value we are carrying forward |
|------|-------------------------------|
| Peak window | Weekday morning, 8:00–9:00 AM |
| Total volume | ~3,490 veh/h (DoR Gwarko East, 2-day mean) |
| Uncertainty on that total | ~±15% day-to-day |
| Direction | ~63% city-bound / 37% reverse |
| Mix | 74% two-wheeler, 18% four-wheeler, 3% tempo, 5% bus |
