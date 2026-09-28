# WRRA pulsar forecast monitoring

**Author:** Wonsik Choi  
**Model:** WRRA Physics Series IV, v4.2 (forecast registered 2026-09-01)  
**Audit date:** 2026-09-28  
**Status:** No eligible completed post-registration ON/OFF interval has been verified; prospective forecast remains unscored.

## Purpose / 연구 목적

This repository tracks published and archived observations of intermittent pulsars PSR J1832+0029 and PSR J1841−0500 against the **frozen**, event-relative dwell-time predictions of WRRA Series IV v4.2. The central test is a **complete ON or OFF state that begins after 2026-09-01**, with independently established transition boundaries. Archived observations from before the freeze can audit the historical record but cannot count as a prospective success.

이 저장소는 WRRA 제4편 v4.2의 동결예측을 원관측과 대조합니다. **2026-09-01 이후 시작되어 종료된 상태구간**을 채점 대상으로 삼습니다. 동결일 전 자료를 뒤늦게 찾았다는 이유로 미래예측 적중으로 계산하지 않습니다.

## Frozen forecast: do not retune

The paper specifies the survival function `S(T | T50, k) = 2^[-(T/T50)^k]`, shared shape `k = 2.418`, and the following medians and reported 95% intervals. The model is a statistical dwell-time proposal, not a demonstrated physical mechanism for pulsar state changes.

| Pulsar | State | Median (days) | Reported 95% interval (days) |
| --- | --- | ---: | ---: |
| J1832+0029 | OFF | 644 | 164–1286 |
| J1832+0029 | ON | 1497 | 381–2989 |
| J1841−0500 | OFF | 580 | 148–1158 |
| J1841−0500 | ON | 221 | 56–441 |

**Freeze rule:** never update the four medians, shape, or intervals in response to later observations. A changed model must receive a new version and a separately dated forecast.

## Observation ledger and provenance

| Target | Observation / publication | Evidence | Boundary inference |
| --- | --- | --- | --- |
| J1832+0029 | Wang et al. (2020), measurements through MJD 58210 (2018-04-02) | Previously reported OFF episode; used in historical modeling | Historical, before freeze. |
| J1832+0029 | Parkes archive `uwl_211209_001109_b2.rf` (filename suggests 2021-12-09) | Folded-profile archive; a pulse candidate appears in the profile | Candidate ON epoch, not a transition date. Archive metadata and pipeline verification needed. |
| J1832+0029 | Parkes archive `uwl_240212_004842_b2.rf` (filename suggests 2024-02-12) | Folded-profile archive; a pulse candidate appears in the profile | Candidate ON epoch, not evidence of uninterrupted ON since 2021. |
| J1832+0029 | Parkes archive `uwl_240301_001114_b2.rf` (filename suggests 2024-03-01) | Profile affected by interference in preliminary inspection | Unclassified. |
| J1832+0029 | Parkes archive `uwl_240812_131621_b2.rf` (filename suggests 2024-08-12) | No secure pulse classification from preliminary folded-profile inspection | **Do not assert OFF** from this one archive view; no documented sensitivity threshold, raw-data confirmation, or repeated timing measurement. |
| J1841−0500 | Bause et al. (first posted 2025-09-17), S1-band observation MJD 60503 (2024-07-12) | Serendipitous detection in MeerKAT imaging, including circular polarization | One detection epoch, not an ON boundary or completed ON duration; predates freeze. |

**Date caveat:** Parkes filename dates are only provisional dates parsed from filenames. The portal's session/display dates can differ; obtain observation headers before treating any of them as authoritative UTC boundaries. Do not treat the preliminary profile inspection as a peer-reviewed timing result.

### Sources

- [WRRA Series IV v4.2](https://github.com/Wonsik-Choi-janefather) — Wonsik Choi, frozen model registered 2026-09-01; the precise source document is `WRRA_물리연작_IV_펄서튜닝_WRRA전향예측_동결모형_최원식_v4.2.docx`. The model values above are transcribed from that document.
- [Wang et al., intermittent-pulsar timing (2020)](https://arxiv.org/abs/2005.05558).
- [CSIRO PULSE@Parkes, J1832+0029 archive](https://pulseatparkes.atnf.csiro.au/pulsarShow.php?psr=J1832%2B0029); search the exact filenames listed above. Example [2024-08-12 file entry](https://pulseatparkes.atnf.csiro.au/pulsarSchoolShow.php?id=260&psr=J1832%2B0029).
- [Bause et al., MeerKAT paper](https://arxiv.org/html/2509.14043v1), sections 2.2 and 4.2. This paper targets magnetars; J1841−0500 appears serendipitously.

## Scoring protocol

1. Verify raw observation UTC/MJD, exposure, instrument band, dispersion measure, radio-frequency-interference handling, detection significance and non-detection flux limits. Obtain repeat epochs and, where possible, phase-connected pulse times of arrival and state-dependent spin-down.
2. Bound each transition by the **last securely classified old-state epoch** and **first securely classified new-state epoch**. Preserve gaps and ambiguous epochs. For two transitions, propagate their date intervals into a dwell-time interval; do not substitute the midpoint for a measured duration.
3. A complete, eligible interval must begin **after 2026-09-01** and end at a verified subsequent transition. If its duration is measured with sufficient precision, mark **inside 95% interval** / **outside 95% interval**; if the allowed duration straddles the interval edge, mark **indeterminate**. Also report the median error in days, without optimizing parameters. A single outside result is a forecast miss, not by itself proof that a probabilistic model is impossible; assess repeated trials and calibration.
4. Incomplete ongoing states are **right-censored**; a missing earlier boundary is **left-censored**; states with both boundaries uncertain are **interval-censored**. Record them, but do not call them hits or failures based on a guessed midpoint. Compare censored evidence to the predeclared survival model only with a prespecified likelihood analysis.
5. Keep archival audits separate from the post-freeze holdout. New *publication date* does not turn a pre-freeze *observation date* into a post-freeze event.

## Correction to an earlier informal comparison

A preliminary interpretation proposed that J1832+0029 switched OFF between 2024-02-12 and 2024-08-12 and assigned its ON duration `795–2324 days`, then described its midpoint as about `+4.2%` from the 1497-day forecast. **This is not a valid score.** The August profile does not securely establish an OFF state, intervening state changes are unexcluded, the start boundary is uncertain, and both proposed epochs precede the 2026-09-01 registration. The midpoint is arbitrary under interval censoring. Withdraw the “hit” characterization.

**Current verdict (2026-09-28): unscored for both pulsars.** The 2024 J1841 image confirms an archived detection, not a completed state; no eligible post-registration state interval with two secure transition boundaries is recorded here. The frozen parameters remain unchanged.

## Contributing a new observation

Provide pulsar ID, facility and band, observation start/end in UTC and MJD, raw file or DOI, exposure and sensitivity, pulse/timing evidence, previous and next classified epochs, treatment of RFI, inferred transition-date ranges, whether the interval began after the freeze, and the resulting scoring classification. Link primary data or a dated paper. Preserve revisions in the Git history; never overwrite the frozen table.
