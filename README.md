# Hospital-Bed-Capacity-Occupancy-Analysis
Exploratory data analysis (EDA) of bed capacity and occupancy across 737 healthcare facilities in Pune, India, using the Pune Municipal Corporation (PMC) hospital infrastructure dataset.

The project started as a bed occupancy rate calculation. Along the way, a data audit showed that the standard calculation could not be trusted with this dataset. The analysis therefore documents why, and replaces it with metrics the data can genuinely support.

# Table of Contents
1. Business Question
2. Key Findings
3. Dataset
4. Methodology
5. Limitations
6. Recommendations


How is hospital bed capacity distributed across Pune, and where is there evidence of capacity strain that should guide resource allocation and staffing?

Intended audience: hospital administrators and public-health planners.

# Key Findings
# Finding
1	Occupancy cannot be reliably computed from the data as supplied. 663 of 737 rows (90%) share an identical footfall value of 2,550 patients per month. This covers every private facility and is almost certainly a placeholder, not an observation.
2	The original formula was invalid. footfall ÷ (beds × 30) treats every visit as a full day in a bed. It produced a median of about 1,000%, with 94% of inpatient facilities above 100%. Footfall counts visits (including outpatients), not bed-days.
3	Capacity is highly concentrated. The 10 largest facilities hold 29% of all 16,009 beds, and the median facility has only 7.
4	Private facilities hold about 93% of all beds (14,853 vs 1,156). Most public sites are zero-bed dispensaries, so the public network's role is mainly outpatient.
5	Patient load per bed varies widely across the 20 public inpatient facilities (median about 152 patients per bed per month), giving a ranked shortlist for capacity review.
6	Estimated occupancy is extremely sensitive to assumptions. Varying the admitted share (2–10%) and average length of stay (2–5 days) moves the median estimate from about 20% to over 250%, so a single occupancy figure would be unsafe to present.
7	Staffing fields look partly templated. Median nurses per facility stays at 2 regardless of size, so beds-per-nurse ratios (2.5 for small sites up to about 62 for 100+ bed sites) are indicative only.

# Dataset
Size	737 facilities × 17 columns
Coverage	Pune Municipal Corporation, five administrative zones
Contents	Facility type, ownership (public/private), beds, emergency beds, doctors, nurses, midwives, monthly patient footfall, pharmacy and ambulance availability
Source	Publicly available PMC dataset (add your source link here)

Data quality issues found:

 1. Ward No. is 100% empty and City Name is a single constant value.
 2. 43 inconsistent spellings of facility type (for example "Genral", "Opthlm", "Canser").
 3. Inconsistent Yes/No coding (YES, Yes, N.A.).
 4. 54 zero-bed facilities (outpatient dispensaries) where occupancy is undefined.
 5. 29 duplicated facility names, and 68 rows where emergency beds exceed total beds.
 6. Placeholder footfall on 90% of rows (see Key Findings).
    
# Methodology
 1. Audit before cleaning. Missingness, duplicates, and a specific test of whether the occupancy inputs are trustworthy.
 2. Clean and standardise. Clear column names, 43 raw facility labels mapped to 11 groups, Yes/No fields unified, zone recovered from zone names where possible, and flag columns (footfall_is_placeholder, is_inpatient) so problem rows stay visible instead of being silently dropped.
 3. Capacity analysis. Facilities by type and ownership, bed distribution (log scale, because it is heavily skewed), concentration of beds, and totals by zone.
 4. Staffing and services. Beds per nurse and per doctor by facility type and size band, with pharmacy and ambulance coverage by ownership.
 5. Occupancy, handled honestly.
    - Why the naive formula fails.
    - Patients per bed per month for public facilities, where footfall is real, as a pressure index rather than a percentage.
    - Sensitivity analysis of estimated BOR across admission-share and length-of-stay assumptions: Estimated BOR = (footfall × admission share × ALOS) ÷ (beds × 30) × 100
# Findings, limitations and recommendations written for non-technical stakeholders.
