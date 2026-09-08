# NHS England — Appointment Capacity vs. Utilisation

Is the NHS primary care network actually at capacity, or does it just look that way on average? An analysis of 11 months of appointment data against the stated 1.2 million daily capacity ceiling, in Python.

## Problem

GP numbers are falling, patients per GP are rising, and satisfaction is dropping; but there was no clear evidence on whether existing capacity was genuinely being exceeded or whether the issue was distribution. Without that, arguments for expanding resources had nothing to stand on. A 5 Whys analysis located the root cause as the absence of any systematic assessment linking appointment demand, staffing, and capacity.

## Data

Three NHS England appointment datasets covering August 2021 to June 2022, plus a dataset of trending Twitter hashtags.

A metadata review surfaced the most important caveat up front: **data entry by practices is voluntary and unstandardised.** Every finding below inherits that uncertainty. One dataset contained duplicate rows; with no unique record identifier available there was no way to distinguish genuine duplicates from legitimately identical records, so they were retained rather than dropped (removing them risked deleting real appointments).

## Method

Quality checks on formats, columns, missing values, and duplicates, followed by descriptive statistics. Date formats standardised across all three sources.

Analysis was built around user-defined functions rather than repeated inline code, so that category totals, percentages, and plots could be regenerated consistently across eight different grouping variables. Appointments were analysed at daily and monthly resolution and broken down by service setting, national category, healthcare professional type, appointment status, appointment mode, and booking lead time. Capacity was overlaid as an annotation line on every temporal chart to make the comparison direct.

Appointment status was then cross-tabulated against booking lead time and appointment mode using stacked bar charts, to isolate what predicts a missed appointment.

## Findings

**The average hides the answer.** Mean daily utilisation sits at roughly 85% of the 1.2M capacity — which reads as comfortable headroom. Disaggregating by day of week reverses the conclusion entirely: capacity is exceeded five days a week for most of the period, with Mondays and Tuesdays in August 2021 the worst. The only genuine slack falls at Christmas and Easter. **This is the central result of the study, and it is invisible in any aggregate view.**

**Missed appointments concentrate in predictable places.** 4.1% of appointments were unattended. In October 2021, the busiest month, that is approximately 1,565,624 missed appointments; a cost of around £47M at the NHS figure of £30 per appointment. Missed appointments cluster in face-to-face bookings and in appointments booked more than 22 days out. Long lead times themselves cluster in the highest-volume months, so the busiest periods are also the most expensive ones.

**Provision is heavily concentrated in GPs.** GPs account for over 91% of appointments across five service settings; Primary Care Networks and Extended Access Provision together contribute 2.95%.

**13% of appointments are unusable for analysis**, falling into Inconsistent Mapping or Unmapped categories. That is a data quality problem large enough to affect the reliability of any category-level conclusion drawn here.

**COVID is legible in the series.** Total monthly appointments from January 2020 to June 2022 track pandemic phases directly — sharp drops following the March 2020 lockdown and the December 2021 Plan B announcement, recoveries as restrictions eased.

## Recommendations

Make data entry mandatory and standardised; without it, none of this analysis is repeatable at the reliability a resourcing decision requires. Recruit weekend staff and expand Extended Access Provision to flatten the Monday–Tuesday peak rather than simply adding headcount. Have administrative staff confirm attendance for appointments booked more than three weeks ahead, which targets the specific segment where no-shows concentrate. Expand telephone appointments where physical examination is not required, given their lower no-show rate.

## Limitations

The voluntary, non-standardised data entry is the fundamental constraint and cannot be worked around analytically. The Twitter analysis produced nothing usable — "healthcare" was the top hashtag, which confirms only that healthcare is discussed. To be worth anything, that strand would need geotagged tweets filtered by region and mapped against regional utilisation, on a substantially larger sample. Video and online appointment modes make up 0.49% of the data, too few to support conclusions. Staffing levels by practice type and regional variation were out of scope and are the obvious next step.

## Files

| File | Contents |
|---|---|
| `Drwiega_Julita_DA201_Assignment_Notebook.ipynb` | Full analysis — cleaning, functions, all figures |
| `Drwiega_Julita_DA201_Assignment_Report.pdf` | Written report with figures and references |

## Stack

Python · pandas · Seaborn · Matplotlib

---

*Completed as part of the LSE Data Analytics Career Accelerator, 2026. Final grade: 77%.*
