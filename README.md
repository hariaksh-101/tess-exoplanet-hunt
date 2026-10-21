# Hunting Exoplanets with NASA TESS Data

**Author:** Hariaksh Suman Rao, 1st PU (PCM + Computer Science), Bengaluru, India
**Date:** October 2026
**Tools:** Python, Google Colab, Lightkurve, NASA Exoplanet Archive

## What this project does
I used free data from NASA's TESS space telescope to detect exoplanets by the dips in starlight they cause when they pass in front of their stars. First I recovered a known planet to test my method, then I applied it to a planet candidate that has not yet been confirmed.

## Part 1 & 2: Recovering the known planet Pi Mensae c
Pi Mensae is a star about 60 light-years away. I searched its TESS light curve with the Box Least Squares (BLS) method, first with one sector of data and then with six sectors combined.

| | 1 sector | 6 sectors | NASA published |
|---|---|---|---|
| Orbit period | 6.266 days | 6.268 days | 6.2678 days |
| Planet size | 2.02 Earth radii | 2.02 Earth radii | 2.02 Earth radii |
| Transits used | 4 | about 25 | – |

My first six-sector search found a false signal at 18.96 days. I traced it to noise spikes and data gaps, fixed it by cleaning and binning the data, and recovered the correct period.

## Part 3: Investigating the unconfirmed candidate TOI-4597.01
I downloaded NASA's list of TESS planet candidates and chose TOI-4597.01 (TIC 68573534), a bright star with a deep transit.

| | My result | NASA catalogue |
|---|---|---|
| Period | 4.667 days | 4.6664 days |
| Depth | 6,581 ppm | 6,900 ppm |
| Size | about 13.9 Earth radii | 13.2 Earth radii |

**Key findings**
- The host star pulsates about every 45 minutes (likely a δ Scuti-type star). These pulsations are almost as large as the transit, so I measured the depth with medians instead of the lowest point.
- **Vetting test 1 (odd vs even transits):** 6,911 ± 311 ppm vs 6,346 ± 342 ppm, consistent. Passed.
- **Vetting test 2 (secondary eclipse at half-orbit):** −138 ± 179 ppm, no dip found. Passed.

**Conclusion:** the signal behaves like a planet: a possible hot Jupiter orbiting a pulsating star. It is not proven; a brown dwarf or very small star could look similar, and confirming it would need a mass measurement from radial velocity observations.

## Limitations
- Planet sizes depend on star sizes taken from NASA.
- Uncertainties are rough estimates, especially with the star's pulsations.
- Only 6 sectors of data were used for each star.

## How to run it
Open `01_recovering_pi_mensae_c_with_TESS.ipynb` in Google Colab. Run the cells top to bottom (first run installs Lightkurve with `pip install lightkurve`).
Run each cell one at a time not all at once may cause error.

## Acknowledgements
This project uses data from the NASA TESS mission, obtained through the Mikulski Archive for Space Telescopes (MAST), the Lightkurve Python package, and the NASA Exoplanet Archive.
