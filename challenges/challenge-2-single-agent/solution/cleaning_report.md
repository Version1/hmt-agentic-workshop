# Cleaning Report

## Summary
- Original row count: 1010
- Cleaned row count: 476
- Output schema verified on reload: yes

## Issues Found
- Missing values (blank cells): 133
- Missing values (sentinel strings): 111
- Malformed dates detected: 219
- Exact duplicate rows: 284
- Near-duplicate rows removed: 250
- Expenditure formatting issues normalised: 98
- Expenditure out-of-range values flagged (<500 or >15000): 9
- GDP growth out-of-range values observed (outside -20 to 20): 24
- Normalisation changes (department/category/date/number formatting): 570

## Actions Taken
- Stripped whitespace from text columns (`month`, `department`, `category`).
- Mapped department name variants to canonical department codes.
- Normalised date variants to `YYYY-MM` where unambiguous.
- Removed exact duplicates (kept first occurrence).
- Removed near-duplicates for the same month/department/category where one metric appeared amended within tolerance and the other matched.
- Normalised `expenditure_gbp_millions` by removing currency symbols, commas, quotes, and `M` suffixes, then converted to numeric.
- Added `expenditure_flag` and marked out-of-range expenditure values as `out_of_range`.
- Normalised category variants to canonical lowercase underscore values only.
- Filled missing numeric values using department-level averages (expenditure rounded to whole number, GDP growth rounded to 1 decimal).

## Missing Value Cell Log
| Source Row | Column | Marker |
|---:|---|---|
| 2 | expenditure_gbp_millions | - |
| 5 | expenditure_gbp_millions | blank |
| 6 | gdp_growth_pct | NULL |
| 7 | gdp_growth_pct | blank |
| 9 | gdp_growth_pct | n/a |
| 11 | expenditure_gbp_millions | NULL |
| 15 | expenditure_gbp_millions | blank |
| 16 | expenditure_gbp_millions | #N/A |
| 17 | gdp_growth_pct | - |
| 22 | gdp_growth_pct | blank |
| 23 | expenditure_gbp_millions | - |
| 24 | expenditure_gbp_millions | n/a |
| 26 | expenditure_gbp_millions | blank |
| 28 | expenditure_gbp_millions | #N/A |
| 28 | gdp_growth_pct | #N/A |
| 30 | expenditure_gbp_millions | - |
| 31 | gdp_growth_pct | blank |
| 32 | expenditure_gbp_millions | blank |
| 38 | expenditure_gbp_millions | #N/A |
| 39 | gdp_growth_pct | blank |
| 40 | gdp_growth_pct | #N/A |
| 43 | expenditure_gbp_millions | - |
| 47 | gdp_growth_pct | blank |
| 56 | gdp_growth_pct | blank |
| 57 | expenditure_gbp_millions | blank |
| 61 | expenditure_gbp_millions | blank |
| 79 | gdp_growth_pct | blank |
| 81 | expenditure_gbp_millions | NULL |
| 83 | gdp_growth_pct | n/a |
| 89 | gdp_growth_pct | n/a |
| 93 | gdp_growth_pct | n/a |
| 95 | expenditure_gbp_millions | n/a |
| 95 | gdp_growth_pct | blank |
| 98 | expenditure_gbp_millions | - |
| 107 | expenditure_gbp_millions | blank |
| 110 | gdp_growth_pct | blank |
| 111 | expenditure_gbp_millions | blank |
| 115 | gdp_growth_pct | blank |
| 120 | gdp_growth_pct | blank |
| 122 | expenditure_gbp_millions | #N/A |
| 122 | gdp_growth_pct | #N/A |
| 135 | gdp_growth_pct | blank |
| 136 | expenditure_gbp_millions | blank |
| 146 | expenditure_gbp_millions | blank |
| 148 | expenditure_gbp_millions | blank |
| 151 | expenditure_gbp_millions | N/A |
| 152 | expenditure_gbp_millions | blank |
| 165 | gdp_growth_pct | n/a |
| 168 | expenditure_gbp_millions | blank |
| 172 | gdp_growth_pct | blank |
| 174 | gdp_growth_pct | N/A |
| 176 | gdp_growth_pct | n/a |
| 177 | expenditure_gbp_millions | #N/A |
| 177 | gdp_growth_pct | #N/A |
| 185 | gdp_growth_pct | - |
| 189 | gdp_growth_pct | blank |
| 192 | gdp_growth_pct | blank |
| 193 | expenditure_gbp_millions | n/a |
| 201 | expenditure_gbp_millions | blank |
| 206 | expenditure_gbp_millions | blank |
| 207 | expenditure_gbp_millions | blank |
| 211 | expenditure_gbp_millions | blank |
| 215 | gdp_growth_pct | n/a |
| 216 | gdp_growth_pct | #N/A |
| 227 | gdp_growth_pct | blank |
| 233 | expenditure_gbp_millions | blank |
| 235 | expenditure_gbp_millions | - |
| 241 | gdp_growth_pct | #N/A |
| 244 | gdp_growth_pct | blank |
| 247 | expenditure_gbp_millions | blank |
| 249 | gdp_growth_pct | N/A |
| 257 | expenditure_gbp_millions | blank |
| 258 | expenditure_gbp_millions | blank |
| 261 | gdp_growth_pct | blank |
| 264 | expenditure_gbp_millions | blank |
| 267 | gdp_growth_pct | - |
| 275 | expenditure_gbp_millions | - |
| 278 | gdp_growth_pct | blank |
| 281 | expenditure_gbp_millions | blank |
| 283 | expenditure_gbp_millions | N/A |
| 286 | expenditure_gbp_millions | blank |
| 303 | expenditure_gbp_millions | blank |
| 305 | gdp_growth_pct | NULL |
| 310 | expenditure_gbp_millions | N/A |
| 312 | gdp_growth_pct | blank |
| 313 | gdp_growth_pct | blank |
| 318 | expenditure_gbp_millions | blank |
| 321 | expenditure_gbp_millions | blank |
| 322 | gdp_growth_pct | #N/A |
| 331 | expenditure_gbp_millions | - |
| 333 | gdp_growth_pct | n/a |
| 334 | expenditure_gbp_millions | blank |
| 339 | expenditure_gbp_millions | #N/A |
| 339 | gdp_growth_pct | #N/A |
| 348 | expenditure_gbp_millions | blank |
| 353 | expenditure_gbp_millions | blank |
| 359 | gdp_growth_pct | n/a |
| 370 | expenditure_gbp_millions | N/A |
| 377 | gdp_growth_pct | #N/A |
| 382 | expenditure_gbp_millions | N/A |
| 387 | expenditure_gbp_millions | - |
| 389 | expenditure_gbp_millions | blank |
| 393 | gdp_growth_pct | - |
| 394 | expenditure_gbp_millions | N/A |
| 397 | expenditure_gbp_millions | #N/A |
| 397 | gdp_growth_pct | N/A |
| 403 | expenditure_gbp_millions | blank |
| 404 | expenditure_gbp_millions | #N/A |
| 407 | expenditure_gbp_millions | n/a |
| 410 | expenditure_gbp_millions | blank |
| 416 | gdp_growth_pct | blank |
| 423 | expenditure_gbp_millions | blank |
| 426 | gdp_growth_pct | blank |
| 427 | gdp_growth_pct | n/a |
| 436 | expenditure_gbp_millions | - |
| 438 | gdp_growth_pct | NULL |
| 451 | expenditure_gbp_millions | blank |
| 455 | gdp_growth_pct | blank |
| 461 | expenditure_gbp_millions | blank |
| 462 | gdp_growth_pct | blank |
| 466 | expenditure_gbp_millions | #N/A |
| 471 | gdp_growth_pct | blank |
| 476 | expenditure_gbp_millions | blank |
| 480 | expenditure_gbp_millions | blank |
| 485 | gdp_growth_pct | blank |
| 486 | expenditure_gbp_millions | - |
| 491 | gdp_growth_pct | blank |
| 493 | expenditure_gbp_millions | blank |
| 496 | gdp_growth_pct | n/a |
| 498 | gdp_growth_pct | blank |
| 501 | gdp_growth_pct | N/A |
| 502 | gdp_growth_pct | blank |
| 505 | expenditure_gbp_millions | #N/A |
| 506 | expenditure_gbp_millions | #N/A |
| 512 | expenditure_gbp_millions | n/a |
| 515 | gdp_growth_pct | blank |
| 518 | gdp_growth_pct | n/a |
| 520 | gdp_growth_pct | n/a |
| 525 | expenditure_gbp_millions | blank |
| 528 | gdp_growth_pct | blank |
| 541 | gdp_growth_pct | blank |
| 548 | expenditure_gbp_millions | blank |
| 554 | gdp_growth_pct | blank |
| 558 | expenditure_gbp_millions | #N/A |
| 558 | gdp_growth_pct | N/A |
| 559 | gdp_growth_pct | #N/A |
| 560 | gdp_growth_pct | blank |
| 570 | gdp_growth_pct | n/a |
| 575 | expenditure_gbp_millions | - |
| 576 | gdp_growth_pct | #N/A |
| 581 | gdp_growth_pct | n/a |
| 583 | expenditure_gbp_millions | blank |
| 587 | gdp_growth_pct | blank |
| 588 | expenditure_gbp_millions | blank |
| 592 | expenditure_gbp_millions | N/A |
| 593 | gdp_growth_pct | blank |
| 595 | gdp_growth_pct | blank |
| 596 | expenditure_gbp_millions | blank |
| 605 | expenditure_gbp_millions | blank |
| 606 | gdp_growth_pct | - |
| 608 | expenditure_gbp_millions | blank |
| 616 | expenditure_gbp_millions | n/a |
| 616 | gdp_growth_pct | blank |
| 618 | expenditure_gbp_millions | blank |
| 621 | expenditure_gbp_millions | - |
| 623 | expenditure_gbp_millions | #N/A |
| 631 | gdp_growth_pct | blank |
| 635 | gdp_growth_pct | blank |
| 637 | expenditure_gbp_millions | N/A |
| 639 | expenditure_gbp_millions | #N/A |
| 641 | gdp_growth_pct | - |
| 644 | expenditure_gbp_millions | blank |
| 647 | expenditure_gbp_millions | N/A |
| 652 | gdp_growth_pct | blank |
| 657 | expenditure_gbp_millions | #N/A |
| 657 | gdp_growth_pct | #N/A |
| 668 | expenditure_gbp_millions | blank |
| 675 | gdp_growth_pct | #N/A |
| 678 | expenditure_gbp_millions | blank |
| 680 | expenditure_gbp_millions | blank |
| 684 | expenditure_gbp_millions | N/A |
| 696 | expenditure_gbp_millions | blank |
| 700 | gdp_growth_pct | blank |
| 703 | expenditure_gbp_millions | blank |
| 706 | expenditure_gbp_millions | - |
| 711 | gdp_growth_pct | blank |
| 719 | gdp_growth_pct | n/a |
| 724 | gdp_growth_pct | blank |
| 725 | expenditure_gbp_millions | blank |
| 728 | gdp_growth_pct | blank |
| 734 | expenditure_gbp_millions | blank |
| 735 | gdp_growth_pct | blank |
| 736 | expenditure_gbp_millions | blank |
| 743 | expenditure_gbp_millions | blank |
| 748 | expenditure_gbp_millions | N/A |
| 749 | expenditure_gbp_millions | #N/A |
| 773 | expenditure_gbp_millions | - |
| 774 | gdp_growth_pct | blank |
| 777 | gdp_growth_pct | - |
| 784 | expenditure_gbp_millions | blank |
| 786 | expenditure_gbp_millions | blank |
| 787 | gdp_growth_pct | blank |
| 788 | expenditure_gbp_millions | - |
| 791 | expenditure_gbp_millions | N/A |
| 794 | gdp_growth_pct | blank |
| 797 | expenditure_gbp_millions | blank |
| 805 | expenditure_gbp_millions | blank |
| 816 | expenditure_gbp_millions | N/A |
| 820 | expenditure_gbp_millions | blank |
| 824 | expenditure_gbp_millions | blank |
| 831 | gdp_growth_pct | - |
| 833 | expenditure_gbp_millions | #N/A |
| 833 | gdp_growth_pct | #N/A |
| 834 | expenditure_gbp_millions | #N/A |
| 836 | gdp_growth_pct | blank |
| 837 | gdp_growth_pct | blank |
| 847 | expenditure_gbp_millions | #N/A |
| 849 | gdp_growth_pct | blank |
| 853 | expenditure_gbp_millions | blank |
| 863 | expenditure_gbp_millions | blank |
| 866 | expenditure_gbp_millions | blank |
| 868 | expenditure_gbp_millions | blank |
| 877 | gdp_growth_pct | blank |
| 884 | gdp_growth_pct | blank |
| 890 | gdp_growth_pct | blank |
| 895 | expenditure_gbp_millions | blank |
| 896 | expenditure_gbp_millions | - |
| 900 | gdp_growth_pct | - |
| 905 | expenditure_gbp_millions | n/a |
| 906 | gdp_growth_pct | blank |
| 913 | gdp_growth_pct | N/A |
| 918 | gdp_growth_pct | - |
| 927 | expenditure_gbp_millions | blank |
| 934 | gdp_growth_pct | NULL |
| 937 | expenditure_gbp_millions | blank |
| 941 | gdp_growth_pct | blank |
| 955 | expenditure_gbp_millions | - |
| 962 | expenditure_gbp_millions | #N/A |
| 964 | expenditure_gbp_millions | blank |
| 966 | expenditure_gbp_millions | N/A |
| 970 | gdp_growth_pct | blank |
| 982 | expenditure_gbp_millions | blank |
| 993 | gdp_growth_pct | blank |
| 997 | expenditure_gbp_millions | blank |

## Assumptions
- Challenge 2 convention writes outputs under `solution/`; files were written to `solution/cleaned_data.csv` and `solution/cleaning_report.md`.
- Near-duplicates were evaluated after date normalisation and exact de-duplication.
- GDP out-of-range values were reported but not altered unless missing values were filled via department averages.
- Category values not mappable to the canonical list were set to missing and preserved as missing text.
