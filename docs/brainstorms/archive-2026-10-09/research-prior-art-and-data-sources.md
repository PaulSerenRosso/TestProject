# Research: Prior Art and Free Data Sources for the XR Digital Twin Portfolio Project

Date: 2026-10-09 (all "accessed" dates below are this date)
Status: Research complete for a first pass. Recommendation given, decision belongs to the owner.
Builds on: `docs/brainstorms/portfolio-xr-digital-twin.md`

## 1. Summary
- Prior art is plentiful in **research papers** and **big commercial/government twins** (Virtual Singapore, Willow). It is thin in **small, playable, human-scale "help me decide" tools** that use real weather data. That is the white space.
- For every candidate, the best-supported free data is **outdoor** (weather, air quality, grid carbon, river levels). I found **no free public real-time indoor CO2 feed**. So the "classroom air quality" idea always means: real outdoor data drives a simulated indoor model. That is fine, but the UI must say so.
- Best free data for a stable portfolio: **Open-Meteo** (weather, air quality, flood, historical back to 1940, keyless) and the **UK Carbon Intensity API** (keyless, history since 2017). Both have a licence caveat or a coverage caveat, see section 4.
- Recommendation (section 5): a **single-room "heat and air" twin** (one thermal + CO2 model) where the headline scenario is a **heatwave in a care-home room**, with CO2/ventilation as the second axis. It keeps your classroom/CO2 idea, adds the strongest replay story (real heatwaves from ERA5), and has the clearest prior-art gap.
- Flood/evacuation is the weakest choice for month 1 (scope, terrain data, many prior projects). The energy twin has the best live data but the weakest human-scale decision.

## 2. Goal and context
The owner cannot decide between four simulations (classroom/office air quality, care-home heatwave, flood/evacuation, energy/grid carbon). Constraints: Unity 6.6, Quest 2 later, no backend, one-month first release, A/B scenario comparison, replay provider for stable demos. This document answers two questions: what already exists, and which free data can feed each option.

## 3. TOPIC 1: Prior art

Legend for type: P = personal, C = commercial, Pro = professional/government, V = volunteer/open-source, S = academic/scientific. Source reliability: "paper" = peer-reviewed or preprint, "vendor" = marketing page, "snippet" = I only saw a search summary, not the full page.

### 3.1 Cross-cutting: building/environment digital twins and XR visualisation
| Name | Who / type | What it does | Tech | Link | Lesson |
|---|---|---|---|---|---|
| Lin and Wu, Unity + IoT + BIM digital twin (ICCEPM 2024) | S (paper) | Real-time twin of a building; indoor CO2 vs Taiwan EPA limit; ML on camera + sensors; notes ventilation and occupant count drive CO2 | Unity, IoT, BIM | https://koreascience.or.kr/article/CFKO202431947397342.pdf | Confirms Unity + CO2 is a credible academic pattern. It is a monitoring twin, not a "what if I change X" decision tool. Opportunity: add levers + A/B. |
| Nisiotis, Hadjiliasi, Napp, COMPSAC 2025 (UCLan) | S (paper) | Compares web dashboard vs 2D twin vs VR twin of a mixed-use office for non-expert understanding of indoor air data | Engine not stated in the snippet | https://knowledge.lancashire.ac.uk/id/eprint/55450/ | Closest to your goal. Gives you a ready evaluation idea: test dashboard vs spatial view. Cite it in the README. Verify engine and findings in the full text. |
| Masubuchi and Hiraki, Kajima / Tsukuba (arXiv 2505.15089) | S + industry | Smart-building twin on a metaverse platform; air quality as colour effects; fan speeds mirrored | Commercial metaverse platform (Unity not confirmed) | https://arxiv.org/html/2505.15089v1 | Shows industry interest; visual language of "air as colour" is established. |
| DeltaVR, Univ. of Tartu thesis (2025) | S (student thesis) | VR twin of a building with dashboards for energy, CO2, temperature | VR (details not verified) | https://dspace.ut.ee/bitstreams/ac9ab914-39b4-4d60-b521-502250c8944a/download | Typical: dashboards in VR, little decision-making. Differentiate with interaction + comparison. |
| AI-driven digital twin of a house in VR (arXiv 2212.07102) | S (paper) | Homeowners see CO2 density and temperature inside the model | Not stated | https://arxiv.org/pdf/2212.07102 | Same: visualise invisible gas. |
| AeroViz (VCBM 2021) | S | Immersive visualisation of aerosol spread in a classroom with air filters, iso-surfaces; education aimed | CFD-based; engine not verified | https://conferences.eg.org/vcbm2021/?p=296 | Proves a classroom + aerosol + immersive story is publishable. It uses heavy CFD; your simplified well-mixed model is a deliberate, lighter alternative. |
| Environment Twin (LAU capstone, ~2019-20) | S (student) | Unity desktop weather-event simulator with physical sensors | Unity | https://soe.lau.edu.lb/capstone-projects/environment-twin--a-digital-twin.php | Shows the "Unity + sensors" student pattern. No public code seen. |
| TwinTurbine (Stockholm Univ. course) | S (student) | Unity wind-turbine twin pulling wind/temperature from an API | Unity, web API | https://gitea.dsv.su.se/absh8989/TwinTurbine/src/commit/6a5377fbcc97e902c242f32530f4e4cfaf6cc897 | Same pattern: API-fed Unity twin works at student scale. |
| PlantPulse XR, Emission Vision (Stockholm Univ. DCDC course) | S (student) | Quest/Unity plant twin; mixed-reality CO2 emissions globe | Unity, Meta XR | https://extralitylab.dsv.su.se/project/dcdc/ | Quest + Unity + environmental data is doable in a course; bar for polish is low, so polish is a differentiator. |
| Gemini Unity package | V (open source) | Unity package with basic MQTT support, prefabs for sensor-driven twins | Unity 2020.1.17+, MQTT/JSON | https://github.com/ManuelPozor/Gemini | Old; check maintenance before use. Mostly useful as a reference for an MQTT adapter. |
| Willow (WillowTwin) | C | SaaS twin combining spatial and live building data; energy/sustainability optimisation; 75+ integrations | Proprietary | https://atlas.verdantix.com/vendors/willow | The professional benchmark: knowledge-graph, BMS integration. Your piece cannot compete on integration; compete on clarity and decision experience. Vendor claims, not verified. |
| Virtual Singapore | Pro (government) | City-scale twin; simulates pollution, wind, heat island, flood, energy | Dassault 3DEXPERIENCE (from memory, not verified here) | https://www.tech.gov.sg/technews/5-things-to-know-about-virtual-singapore/ | Names the same scenario families you are considering. Aim: "one room of this idea." |
| Unity digital twin intro | C (Unity) | Official tutorial on twins from sensor + historical data | Unity | https://learn.unity.com/tutorial/introduction-to-digital-twins-with-unity | Shows Unity positions twins as an industry story; recruiters will recognise the vocabulary. |

Not found: Cityzenith (no usable results). Not verified: any public open-source Unity indoor-air twin. Searching GitHub directly ("Unity MQTT air quality") is still open.

### 3.2 Candidate A: Classroom / office air quality
| Name | Who / type | What it does | Link | Lesson |
|---|---|---|---|---|
| Peng and Jimenez, CO2 as proxy for infection risk | S (paper) | Shows risk depends on occupancy, masks, activity: there is no single "safe" CO2 number. Underlies an online risk calculator | https://medrxiv.org/content/10.1101/2020.09.09.20191676.full.pdf | Use it to justify the model and to teach that thresholds depend on context. I could not confirm the exact name/URL of the calculator. |
| Duke classroom airborne-virion calculator | S (university) | Estimates virion concentration and dose in a room | described at https://ncnewsline.com/2020/08/11/online-calculator-weighs-risk-of-airborne-covid-19-transmission-in-classrooms/ | Spreadsheet-style calculators exist: they have no space, no time, no A/B. Opportunity. |
| Argonne/ORNL classroom ventilation simulations | S | CFD of aerosol in a classroom; inlet and door on same wall removes dead zones | https://www.olcf.ornl.gov/2022/02/24/covid-19-in-the-classroom-simulating-the-spread/ | Gives a real finding to turn into a scenario card (layout matters), but your well-mixed model cannot show it. Avoid claiming it. |
| Corsi-Rosenthal box studies (UC Davis etc.) | S | DIY filter boxes cut PM in occupied classrooms by 56-91% (particles), >70% PM2.5 | https://engineering.ucdavis.edu/news/corsi-rosenthal-boxes-reduce-air-pollutants | A cheap lever with real evidence: good decision option (filter vs window vs HVAC). Note it affects particles, not CO2. |
| Vendor CO2 monitors with dashboards (Aranet, AirGradient, etc.) | C | Sensor + app | https://homey.app/en-ie/works-with-homey/airgradient | Consumers see numbers, not consequences of choices. |

Gap: I found **no game or simulator** where you choose ventilation vs energy cost in a classroom and compare scenarios (searched Unity/itch-style terms; absence of results is not proof).

### 3.3 Candidate B: Heatwave in a care home / building
| Name | Who / type | What it does | Link | Lesson |
|---|---|---|---|---|
| Summertime overheating in London care homes (Gupta et al., 2021) | S (paper) | Monitoring + EnergyPlus; indoor >30 C in daytime vs 26 C guideline; bedrooms hotter at night; night ventilation most effective passive measure | https://radar.brookes.ac.uk/radar/file/c8e6f707-3f1a-4653-bb6c-df1391f26c5c/1/Summertime%20overheating%20in%20London%20care%20homes%20-%202021%20-%20Gupta%20Howard%20Davies%20Mavrogianni%20Tsoulouh%20Jain%20Oikonomou%20Wilkinson.pdf | Directly supplies thresholds (26 C, 30 C) and the lever ranking you can implement and cite. |
| UCL care-home pilot (Oikonomou et al.) | S | Older buildings: albedo helps; newer: ventilation + external shading. Care-specific barriers: window restrictions for security, decisions on behalf of residents | https://discovery-pp.ucl.ac.uk/id/eprint/10128385/1/BSOV2020_Oikonomou.pdf | Real constraints become game rules (e.g. "window limiter", staff routines). That is a design hook. |
| Canadian bioheat + building simulation for LTC homes | S | Health-based overheating limits from dehydration/core temperature | via https://www.mdpi.com/2075-5309/13/2/390/htm (snippet only, not verified) | Shows a more faithful model exists; yours is explicitly simplified. |
| Critical Choices: Heat Edition | Pro (global health NGO exercise) | Paper-style simulation exercise: yes/no decisions on a heatwave timeline within budget; city-mayor framing | https://globalhealthhub.de/fileadmin/general_documents/Critical_Choices_Heat_Edition_simulation_exercise_vf.pdf | Same decision-under-budget idea, but analogue and city level. Yours would be digital, room level, with physics. |
| Europe Heatwave Simulator | C (Steam game) | Survive in a hot Paris apartment | https://www.dezeen.com/?p=2355089 | Shows public appetite for heat as a game theme; entertainment, not decision support. |
| Climate Heatwave Impact Simulator | P/web | Body heat storage dashboard from temperature, humidity, activity | https://thesumancoder.substack.com/p/i-built-a-simulator-that-shows-how | Models the body, not the building; complementary, shows low bar for web toys. |

Gap (stated by my search, with caveat): no result combined a **building thermal model + staff decision game + real heatwave data**. Closest are the papers (physics) plus the paper exercise (decisions).

### 3.4 Candidate C: Flood / evacuation
| Name | Who / type | What it does | Link | Lesson |
|---|---|---|---|---|
| Virtual Flood Experience System (VFES), Japan | S | VR flood risk communication + evacuation training; reconstructs Typhoon 19 (2019) | https://piahs.copernicus.org/articles/386/21/2024/ | Strong prior art with real event replay. Needs terrain/inundation data. |
| Massey University flood safety VR serious game | S | Non-immersive VR; self-efficacy and knowledge increased | https://mro.massey.ac.nz/handle/10179/71394 | Evidence that simple games work. |
| Indonesian VR flood simulator game | S | Users in flood-prone areas; score rose 25% on second play | https://journal.binus.ac.id/index.php/EMACS/article/view/9988 | Same. |
| Exeter / Torbay Unity flood serious game | S | Unity 3D animated flood on terrain encoded in PNG heightmaps | https://piahs.copernicus.org/articles/386/21/2024/ (snippet; confirm exact paper) | Technical trick reusable for terrain. Shows Unity floods have been done. |
| Sudsbury, iAdapt, Burning Lowlands | S | Climate adaptation games on pluvial flooding, teen flood planning, board game for flood/drought/heat | https://meetingorganizer.copernicus.org/EGU26/EGU26-15019.html | Mostly board/educational; Burning Lowlands (2026 EGU) combines flood, drought, heat. |
| Cities: Skylines / SimCity in participatory planning study | C | Rated among 10 games from 170 screened for participatory planning | https://congress.aesop-planning.eu/event/1/contributions/495 | Commercial sim-games are taken seriously by planners. |

Lesson: flood is the **most crowded** academic area, and its visual payoff needs terrain, water simulation and crowd agents. Avoid for month 1.

### 3.5 Candidate D: Energy / grid carbon
| Name | Who / type | What it does | Link | Lesson |
|---|---|---|---|---|
| En-ROADS + Climate Action Simulation | Pro/S (Climate Interactive, MIT Sloan) | Global policy simulator + role-play; improves knowledge in surveys | https://systemdynamics.org/product/climate-action-simulation-game-en-roads/ | Gold standard for "lever, instant consequence". Global scale; yours is human scale. |
| Powerplay (Gasunie and partners) | C/Pro | Web serious game, you are Minister of Energy; built on the Energy Transition Model | https://power-play.organiq.nl/en/news/powerplay-launches | Free, browser, 60-90 min. National scale, fictional data. |
| Megawatt, Energy Grid Game (TU Delft), Ensured Energy, Go2Zero, Social Mpower, Newtonian Shift | S/Pro | Grid design, port energy, Swiss seasons, district CO2, blackout avoidance, role-play | https://seriousgaming.tudelft.nl/?p=503 and https://arxiv.org/pdf/2508.12799 | The theme is well covered. None found using **live carbon intensity** (my search gave no result; not proof). |
| Electricity Maps | C | Live grid carbon map and API; has free personal tier | https://electricitymaps.com/get-our-data | Existing product shows the data; not a decision game. |

Lesson: crowded at policy scale. The uncovered niche is "building owner shifts a load by hours", which is smaller and less visual.

### 3.6 Better use cases discovered
1. **Combined "heat + air" single-room twin.** Care-home papers show the real trade-off: opening windows cools but is restricted (security, noise); closing raises CO2. This merges your A and B into one model with one coherent scenario and two metrics. No prior art found for it as a playable tool.
2. **Room + carbon-aware cooling/ventilation.** Add UK Carbon Intensity to show when running mechanical ventilation/AC is high-carbon. Optional month-3 extension.
3. **School heat resilience** (classrooms overheating in June/July): same model, same data, larger audience than care homes, lower sensitivity. Good fallback if care-home framing feels risky.

### 3.7 White space and how to differentiate
- **Between papers and dashboards:** Academia gives physics without play; vendors give dashboards without consequences; analogue games give decisions without physics. A small interactive twin with levers + A/B + real replayed weather sits in between.
- **Real events as scenarios:** replay a named historical heatwave (e.g. a UK July 2022 episode; date check needed) in two configurations. Few student projects do this.
- **Honesty layer:** a visible "model limits" panel and cited thresholds (26 C, 30 C) is a credibility edge over most student work.
- **Evaluation hook:** Nisiotis et al. (2025) compared dashboard vs 2D vs VR; you can include a mini version ("dashboard vs spatial view") in the README to show research literacy.
- **Avoid:** CFD-looking claims, fake precision, medical advice claims, and re-implementing a BMS integration story.
- **Reality check on portfolio crowding:** Unity + IoT + building twin is a recognisable student genre (Tartu, Stockholm, Taiwan). Polish, the A/B mechanic and the visible AI pipeline are your differentiators, not the concept.

## 4. TOPIC 2: Free data sources benchmark

Verification note: "verified" means I read the provider's page today. "third-party" means a search result or an unofficial profile. Unverified items are flagged. Unity access in all cases is `UnityWebRequest` GET + JSON (general knowledge: `JsonUtility` cannot parse root arrays or dictionaries well, so plan for Newtonsoft JSON via the Unity package; HTTPS is preferable on Android/Quest).

### 4.1 Benchmark table
| Source | Data | Update freq. | Auth / key | Rate limit | Licence and portfolio use | Coverage | Reliability / downtime | History (replay) | Unity ease |
|---|---|---|---|---|---|---|---|---|---|
| **Open-Meteo forecast / historical weather** https://open-meteo.com/en/terms | Temp, humidity, wind, radiation, precip; hourly | Hourly model updates | None for non-commercial (page silent; air-quality page states "not needed for non-commercial") | Free: <10,000/day, 5,000/h, 600/min (verified) | CC BY 4.0 data; **free API non-commercial only**. "Promotional activities" counted as commercial: a job-seeking portfolio is a grey area (see 4.3) | Global | Third-party trackers show a few incidents; forum reports of timeouts in late Mar and early Apr 2026; no SLA found | ERA5 from 1940, 0.25 deg hourly, ~5 day delay (verified: https://open-meteo.com/en/docs/historical-weather-api) | Excellent: simple URL, flat JSON arrays |
| **Open-Meteo air quality** https://open-meteo.com/en/docs/air-quality-api | PM2.5/10, O3, NO2, CO2 etc., European and US AQI, pollen (Europe) | Europe forecast daily (4 days); global 12-hourly (5 days) | None for non-commercial | Same Open-Meteo limits | CC BY 4.0; mandatory CAMS attribution (verified) | Europe 0.1 deg; global 0.4 deg | As above | European reanalysis from 2013; forecast archive from Oct 2023 | Excellent. Model (CAMS) output, not sensor measurements. |
| **Open-Meteo flood (GloFAS)** https://open-meteo.com/en/docs/flood-api | Modelled river discharge (m3/s), daily | Daily | None for non-commercial | Same | CC BY 4.0 | Global 5 km (v4) | As above | From 1984 (reanalysis through July 2022, then seamless forecast) | Easy; caveat: nearest-river snapping at 5 km can be wrong. Discharge only, not water level or inundation. |
| **MET Norway Locationforecast** https://api.met.no/doc/TermsOfService | Forecast weather | Respect `Expires` header | None, but **identifying User-Agent required** | 20 req/s cap; use caching, 4-decimal coordinates (5+ decimals can give 403) | CC BY 4.0; do not use "Yr" name/logo | Global | Mature national service; no incident data checked | Forecast only (no long archive via this API) | Good; must set User-Agent header in Unity (`SetRequestHeader`). |
| **NWS api.weather.gov** https://www.weather.gov/documentation/services-web-api | Forecasts, alerts (7 days), station observations | Obs delayed up to 20 min | No key; User-Agent required (key planned in future) | Not public, "generous" | Open data, free for any purpose | US only | Not checked | Recent observations only | Moderate: 2-step grid lookup. Useful only for a US scenario. |
| **OpenAQ v3** https://docs.openaq.org/using-the-api/rate-limits | Measured outdoor air quality from reference stations and sensors | Station dependent, often hourly | **Free API key**, limits scoped to key | 60/min, 2,000/h (verified) | Open data with attribution; check terms per source (not fully verified) | Global but patchy | Not checked | Full archive on AWS S3 (docs link) | Good. Needs key stored (not shipped in a public repo). |
| **WAQI / aqicn** https://aqicn.org/api/ | City AQI, station data | Hourly-ish (not verified) | **Token required** | 1,000 req/s default | **Cannot be redistributed/archived, cannot be used in paid apps; for-profit public use needs agreement; non-profit public use needs email notification** (verified) | Global | Not checked | Separate historical platform, not verified | Easy but terms are restrictive for a **replay** provider: caching/archiving data is forbidden. Avoid. |
| **Sensor.Community** https://github.com/opendata-stuttgart/meta/wiki/EN-APIs | Citizen PM, temp, humidity, pressure from DIY sensors | Per minute; 5-min averages | None; **User-Agent required** | Not stated | Licence not stated on the page I read (I believe ODbL, **unverified**; the project site returned 403) | Global, dense in Europe | Community-run; not checked | Daily CSV archive (archive.sensor.community) | Easy. Raw data is noisy; good for a "real citizen sensors" panel. No CO2 in typical sensors. |
| **UK Carbon Intensity API** https://carbon-intensity.github.io/api-definitions/ | Half-hourly national and regional (GB) gCO2/kWh, forecast to 96h+, generation mix | 30 min | None (verified per operation) | Not documented in what I read | CC BY 4.0 (verified from https://carbonintensity.org.uk/) | **Great Britain only** | Not checked | Since 2017-09-26; API range max 14 days per intensity call, stats 30 days | Excellent; clean JSON. |
| **Electricity Maps free API** https://electricitymaps.com/get-our-data | Carbon intensity and mix, real time | Real time | Key (free personal) | Not published; 429 on throttle (third-party) | **Non-commercial only**; free tier reportedly limited to one zone and last 24 h; commercial from about EUR 6,000/yr (third-party) | Global but 1 zone free | Not checked | 24 h on free tier | Fine, but 24 h history is poor for replay. Official portal moved to https://app.electricitymaps.com/docs (not read). Details unverified. |
| **ENTSO-E Transparency** (REST) | EU load, generation, prices, day-ahead | Hourly/15 min | Free **security token** after registration (third-party) | 400 req/min per IP/token, 10-min ban (third-party) | Regulatory open publication; terms not read | EU | Not checked | Long archive | Poor for Unity: XML responses (I believe, unverified), heavy query rules. Skip. |
| **UK EA flood monitoring** https://environment.data.gov.uk/flood-monitoring/doc/reference | River/tide levels, flows, flood warnings, flood areas, 3-day forecast | Readings 15 min (transmitted 1-2x/day); warnings 15 min | None | No numeric limit; ask to use bulk `/data/readings` every 15 min | OGL v3.0 with attribution (verified) | England | Not checked | API: last ~4 weeks; archive: daily CSV dumps | Excellent: JSON-LD style `items` arrays. Best real "river gauge" source. |
| **USGS Water Services** https://waterservices.usgs.gov/docs/instantaneous-values/ | US streamflow/level | ~15 min readings, hourly transmission | None | Not stated | US public domain (general knowledge, unverified here) | US | **Legacy service to be decommissioned early 2027**; migration to `api.waterdata.usgs.gov` (OGC API Features) per USGS posts reported by search (https://waterdata.usgs.gov/blog/api-waterservices-decom/) | Long | Avoid building on legacy; new API format would need testing. |
| **Public MQTT brokers** (test.mosquitto.org, broker.hivemq.com, broker.emqx.io) | Any publish/subscribe stream | Real time | None | Not stated | Topics and messages are public; no SLA seen. A 2022 benchmark showed latency and reliability issues (https://goughlui.com/2022/10/23/project-benchmarking-public-free-mqtt-brokers/) | n/a | Unreliable for demos; TLS support conflicting between sources | None | Needs a third-party C# MQTT library; WebSocket ports exist (8000/8080 etc.). Only useful if you publish your own simulated "room sensor" stream to show the architecture. |
| Firebase etc. | Hosted realtime DB | Real time | Project + key | Free tier | Account required | - | - | - | **Not needed**: you said no backend; mention only as an optional future replay host. Not researched. |

Indoor CO2 / IoT public feeds: AirGradient lets owners opt in to share **outdoor** data to its map and OpenAQ (https://telescopescanada.ca/products/airgradient-open-air-award-winning-outdoor-monitor-outdoor-air-quality-monitor, vendor listing); I did not find a documented public API or any public indoor CO2 feed. Conclusion: **indoor CO2 must be simulated** (or recorded by you if you buy a sensor later; that could be a nice "real room" replay file).

### 4.2 Source agreement and reliability
- Licences and limits for Open-Meteo, MET Norway, EA, WAQI, OpenAQ, USGS timeline: read from the providers' own pages (high reliability).
- Electricity Maps free tier, ENTSO-E rate limits, MQTT broker behaviour, Open-Meteo uptime: from third-party profiles, forums or status trackers (low to medium reliability). Not confirmed by the providers.
- USGS decommission dates differ across posts (late 2025, late 2026, Q1 2027); the most recent reported post says early 2027.

### 4.3 Risks and caveats to resolve
1. **Open-Meteo "non-commercial" wording.** The terms list "promotional activities" under commercial use. A hiring portfolio is ambiguous. Options: (a) email Open-Meteo and ask; (b) in the demo ship **replay files** (CC BY 4.0 data, attributed) and make live mode optional; (c) use MET Norway as the live provider for the weather (CC BY 4.0, no non-commercial clause on the page I read). Not legal advice.
2. **WAQI forbids caching/archiving**, which conflicts with a replay provider. Avoid.
3. **Replay dataset licensing:** CC BY 4.0 (Open-Meteo, MET Norway, UK Carbon Intensity) and OGL (EA) allow redistribution with attribution; ship an attribution screen.
4. **Quest 2:** HTTPS required for most endpoints, keys must not be committed to the public repo (OpenAQ, Electricity Maps).
5. **Model vs data mismatch:** CAMS and GloFAS are model outputs on coarse grids (11-45 km, 5 km), not measurements. Label them as modelled.

## 5. Mapping use cases to data, and recommendation

### 5.1 Mapping
| Use case | Best data | Replay data | Weakness |
|---|---|---|---|
| Classroom/office air quality | Open-Meteo weather (outdoor temp for ventilation heat loss) + Open-Meteo air quality (outdoor PM/NO2 on window opening) | ERA5 + CAMS reanalysis | Indoor CO2 is purely simulated; no live truth to compare. |
| Care-home heatwave | Open-Meteo weather (temp, humidity, solar radiation) forecasts + ERA5 for historical heatwaves; optional MET Norway as live backup | ERA5 from 1940: any heatwave, any location | Needs a thermal model (single-zone RC) and cited thresholds; must handle sensitivity of care topic. |
| Flood/evacuation | UK EA gauges (England) or Open-Meteo flood (global, discharge only) | EA 4-week API + daily CSV archive; GloFAS from 1984 | Gauge level is not inundation; needs terrain + water sim + crowd agents. Highest scope. |
| Energy/grid carbon | UK Carbon Intensity (GB) | History since 2017 | GB-only (or Electricity Maps 1 zone, 24 h); decision is abstract and visual payoff low. |

### 5.2 Challenging your assumptions
- **"Classroom air quality is the best fit" is true for the decision, not for the data.** The data you can get free is outdoor. Real-time indoor CO2 is not available. The strongest asset of the classroom idea (CO2 and ventilation) is simulated anyway.
- **Weather is the only truly global, keyless, long-history driver.** Heat uses it better than CO2 does: heat is directly driven by outdoor temperature and sun, while CO2 depends on occupants and air exchange.
- **"Real data" for the A/B comparison means weather, not building.** Both A and B should run on the same replayed day; that is a fair-comparison feature, so lean into it.
- **Care-home framing carries responsibility.** Models that look medical invite criticism. Keep it "operational comfort and staff decision exercise", cite thresholds, avoid health claims. A school classroom heatwave is the safer sibling.
- **Flood is tempting visually but is the weakest fit** for one month, desktop-first, Quest 2.

### 5.3 Recommendation
**Pick the "Heat and Air in one room" twin, with a heatwave scenario as the headline.**
- Model: single-zone room with two state variables (temperature and CO2), driven by outdoor temp, solar and occupancy from the data provider. One simplified model, clearly labelled.
- Levers: window opening (day/night), external shading, fan/AC (with energy cost), occupancy schedule, optional "window limiter" rule (from the UCL care-home barriers).
- Metrics: hours above 26 C and 30 C, peak CO2, energy used. A/B: two lever sets on the same replayed heatwave.
- Providers: Simulated (dev) -> Replay (ERA5 heatwave file, attributed) -> Live (Open-Meteo or MET Norway forecast). Add Open-Meteo air quality in month 2 (decision: open window vs outdoor PM). Add UK Carbon Intensity in month 3 as a carbon-aware cooling option, if you want an energy angle.
- Room type: start with a **care-home bedroom** for the narrative, or a **classroom** if you prefer lower sensitivity; the model is identical.

Why:
- Keeps your favourite (ventilation/CO2) while adding the strongest replay (real heatwaves).
- Clearest prior-art gap: physics papers + paper exercise exist; a playable twin was not found.
- Smallest scope of the four; one model; scales to VR as a room.
- Data risk is low: one keyless global source plus replay files.

Trade-offs:
- Open-Meteo licence ambiguity for a portfolio (mitigated by replay files and MET Norway fallback).
- Thermal model credibility (needs a simple RC model plus a validation sanity check against a cited paper's trends, not exact values).
- Less "dramatic" visually than flood; compensate with strong UI, colour language and A/B ghosting.

What would change my mind:
- If you want a **non-environmental audience** or the strongest "live data" story: pick UK energy (best live API) but accept GB-only and abstract decisions.
- If Open-Meteo replies "portfolio not allowed" and MET Norway coverage is insufficient: lean on replay files only.
- If you want maximum visual impact and have terrain assets: flood, but only as month 4+.

## 6. Open questions
- Is a portfolio demo "non-commercial" under Open-Meteo's terms? (email them; not answered.)
- Is Sensor.Community data ODbL? (my belief only; site returned 403.)
- Electricity Maps current free-tier limits (read official docs at https://app.electricitymaps.com/docs).
- ENTSO-E response format and official limits (unverified).
- Open-Meteo real uptime history (status page must be checked manually).
- Which named historical heatwave to use, and which location (needs a date and station check in ERA5).
- Engine of the Nisiotis, Masubuchi and Tartu projects (not verified).
- Whether any public open-source Unity air-quality twin exists on GitHub (not searched directly).

## 7. Decision
Undecided by the owner. Recommendation: heat-and-air single-room twin (section 5.3).

## 8. Handoff for project manager
Next steps (if the recommendation is accepted):
1. Owner confirms use case and room type (care-home bedroom vs classroom).
2. Write the one-paragraph vision and the MVP: desktop, UI Toolkit dashboard, simulated provider, one decision loop (window/shading/fan), A/B comparison on a shared timeline.
3. Define `IDataSource` with Simulated, Replay (JSON file recorded from Open-Meteo, attributed) and Live providers; month 2 live Open-Meteo or MET Norway.
4. Tech-architect spike: single-zone thermal + CO2 model; list formulas and cite thresholds (26 C, 30 C) from the care-home papers.
5. Email Open-Meteo about portfolio use; prepare MET Norway User-Agent fallback.
6. Add an attribution screen (Open-Meteo, CAMS, MET Norway, UK Carbon Intensity if used) and a "Model limits" panel.
7. Keep API keys out of the repo (OpenAQ, Electricity Maps if ever used).
8. Verify Unity 6.6 world-space UI Toolkit support (still open from the main brainstorm).

Open risks: licence ambiguity, model credibility, care-home sensitivity, scope creep into CFD or agents.

## 9. Sources (accessed 2026-10-09)
- Open-Meteo terms: https://open-meteo.com/en/terms
- Open-Meteo air quality: https://open-meteo.com/en/docs/air-quality-api
- Open-Meteo historical: https://open-meteo.com/en/docs/historical-weather-api
- Open-Meteo flood: https://open-meteo.com/en/docs/flood-api
- MET Norway terms: https://api.met.no/doc/TermsOfService
- NWS API: https://www.weather.gov/documentation/services-web-api
- OpenAQ rate limits: https://docs.openaq.org/using-the-api/rate-limits
- WAQI API terms: https://aqicn.org/api/
- Sensor.Community API wiki: https://github.com/opendata-stuttgart/meta/wiki/EN-APIs
- UK Carbon Intensity: https://carbonintensity.org.uk/ and https://carbon-intensity.github.io/api-definitions/
- UK EA flood monitoring: https://environment.data.gov.uk/flood-monitoring/doc/reference
- USGS waterservices: https://waterservices.usgs.gov/docs/instantaneous-values/ and https://waterdata.usgs.gov/blog/api-waterservices-decom/ (via search summary)
- Electricity Maps (search summaries only): https://electricitymaps.com/get-our-data
- Public MQTT broker benchmark: https://goughlui.com/2022/10/23/project-benchmarking-public-free-mqtt-brokers/ (search summary)
- Prior art links as listed in section 3.
