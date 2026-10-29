# Temocillin susceptibility comparison

Comparison of EUCAST disc diffusion vs Etest MIC for temocillin susceptibility
testing, run from `temocillin_data.rds` (`Temocillin_review.qmd`).

## EUCAST interpretation criteria for temocillin

Source: EUCAST Clinical Breakpoint Tables v16.1, valid from 2026-06-24
(https://www.eucast.org/fileadmin/eucast/pdf/breakpoints/v_16.1_Breakpoint_Tables.pdf).

> **Temocillin (infections originating from the urinary tract), E. coli,
> Klebsiella spp. (except K. aerogenes) and P. mirabilis**
>
> | | MIC (mg/L) | Disk content | Zone diameter (mm) |
> |---|---|---|---|
> | Susceptible (S) | ≤ 0.001 | 30 µg | ≥ 50 |
> | Resistant (R) | > 16 | | < 17 |
>
> Footnote F: "Ignore isolated colonies within the inhibition zone."

The S breakpoint (MIC ≤0.001 mg/L, zone ≥50mm) is set below what's
achievable, so results are effectively binary: **I** ("susceptible,
increased exposure": MIC 0.001–16 mg/L, zone 17–49mm) or **R** (MIC >16
mg/L, zone <17mm). True "S" calls should be rare/absent — this matches
`temocillin_data.rds`, where S occurs in only 3 of 13,484 rows.

**Organism restriction**: EUCAST only validates this breakpoint for E. coli,
Klebsiella spp. (excluding K. aerogenes) and P. mirabilis — this is exactly
the inclusion criteria already coded as `organisms_of_interest` in
`Temocillin_review.qmd`.

**Specimen caveat**: EUCAST states the breakpoint applies to infections
"originating from the urinary tract." The cohort is mostly Blood specimens
(574/613 in the Both==1 inclusion-criteria subset) rather than Urine. This
is not necessarily a violation of the breakpoint's intent — Enterobacterales
bacteraemia (especially E. coli/Klebsiella/Proteus) is frequently secondary
to a urinary source (urosepsis), so a Blood specimen can still represent a
urinary-tract-originating infection. The specimen data doesn't confirm
source, though, so this should be treated as a documented assumption, not a
settled fact, if findings are reported externally.
