# Detecting Explosive Price Dynamics and Financial Contagion in the S&P 500

## Overview

This project investigates whether the long-run evolution of the S&P 500 contains episodes of explosive price behavior and whether such episodes interact with market shocks in a way consistent with financial contagion. The analysis is conducted on monthly data covering the period 1996–2026 and combines right-tailed unit root testing with a custom contagion indicator.

The main objective is to distinguish between normal long-run market growth and statistically significant explosive dynamics, then extend this analysis by linking speculative pressure to shock intensity in order to identify fragile or contagion-prone market states.

## Financial markets as complex adaptive systems

Financial markets can be understood as complex adaptive systems (CAS), in which heterogeneous agents interact through prices, information, liquidity, and expectations. These interactions generate nonlinear dynamics, feedback loops, speculative episodes, and systemic instability that cannot be explained only by the behavior of individual market participants.

From this perspective, explosive price movements and contagion are not isolated anomalies, but emergent outcomes of an interconnected and adaptive financial system. The present project can therefore be interpreted as an empirical test of how a major financial market index, the S&P 500, exhibits features consistent with complex adaptive system behavior, especially during periods of heightened instability.

## Research objective

The project has two main goals:

1. detect periods of explosive behavior in the S&P 500 using the GSADF framework  
2. construct an indicator of financial fragility and contagion by combining speculative intensity with rolling market shocks

This allows the analysis to move beyond simple price inspection and toward a more formal identification of instability regimes.

## Conceptual framework

The project is motivated by the view of financial markets as complex adaptive systems. In such systems, heterogeneous agents interact through prices, information, and liquidity, generating nonlinear dynamics, feedback loops, and systemic interdependence. Within this framework, explosive episodes and contagion are treated as emergent features of the market rather than isolated anomalies.

## Data

The analysis uses monthly observations for the S&P 500 index (SPX) covering the period 1996–2026. The data were collected from Investing.com and then imported into Python for cleaning, transformation, and econometric testing.

Main variable used in the core analysis:

- `SP500` – S&P 500 index level (SPX, USD, monthly data, source: Investing.com)

Derived series:

- log-price series
- monthly log returns
- rolling volatility of returns (6-month window)
- GSADF statistic
- rolling ADF statistic
- EXCF composite indicator
- contagion score

## Methodology

### 1. Data preparation
The dataset is uploaded into Google Colab, read into a pandas DataFrame, cleaned, and converted into a time-indexed monthly series. The S&P 500 price is transformed into logarithmic form.

### 2. Bubble detection using GSADF
The Generalized Sup Augmented Dickey-Fuller (GSADF) procedure is applied to the log-price series. This method recursively estimates right-tailed ADF statistics over multiple subsamples and identifies periods in which the market displays explosive dynamics.

The implementation includes:
- right-tailed ADF statistic
- recursive GSADF sequence
- SADF statistic
- bootstrap critical values at 90%, 95%, and 99%

### 3. Additional instability measure
A rolling ADF statistic is computed over a fixed window in order to capture local instability patterns over time.

### 4. EXCF indicator
The GSADF and rolling ADF statistics are normalized and combined into a composite score:

- 60% weight for normalized GSADF
- 40% weight for normalized rolling ADF

This produces the EXCF indicator, which is then classified into three qualitative market states:
- `Normal`
- `Speculative Pressure`
- `Potential Bubbles`

### 5. Contagion framework
To study financial contagion, the EXCF indicator is combined with a rolling volatility-based shock proxy. Both series are normalized, and the contagion score is defined as their product:

`contagion_score = excf_norm × shock_norm`

This ensures that contagion becomes high only when speculative pressure and market stress occur simultaneously.

The contagion map distinguishes between:
- `Fragile system`
- `Potential contagion`

## Main findings

The results indicate that the 2008–2009 crisis was the only clearly dominant explosive episode in the sample. In that period, the GSADF statistic exceeded the 95% and 99% bootstrap critical values, providing the strongest evidence of abnormal market dynamics.

Earlier spikes, especially before 2008, and the more recent upward movements after 2020 are still relevant, but they remain weaker from a statistical point of view. These periods are better interpreted as signs of speculative pressure or renewed market tension rather than as fully confirmed bubble episodes.

The EXCF indicator confirms this interpretation: the 2008–2009 episode is the only one entering the strongest regime of potential bubbles, while most other highlighted intervals remain in the speculative pressure zone.

The contagion indicator leads to the same conclusion. It identifies the global financial crisis as the only clear regime of potential financial contagion, whereas other periods show only moderate fragility rather than systemic contagion of comparable intensity.

## Interpretation

One important result is that the strong and persistent upward trend of the S&P 500 after 2009 does not automatically translate into statistically explosive behavior. This makes the study especially relevant, because it shows that long-run market appreciation and genuine explosive instability are not the same phenomenon.

The framework therefore helps separate:
- sustained market growth
- speculative tension
- fully developed explosive episodes
- contagion-prone systemic stress

## Repository structure

The repository contains the dataset used in the analysis, the Python notebook, the final HTML output, and the README file. The file `SP.txt` is the input dataset that must be uploaded into Python/Google Colab when running the analysis.

- `SP.txt` – input dataset used in Python/Google Colab
- `SP500.xlsx` – dataset in Excel format
- `BubblecontagionSP500.ipynb` – Python notebook containing the full analysis
- `BubblecontagionSP500.html` – exported HTML version of the notebook
- `README.md` – project description and methodology
