# Abdullah Essam — CSEN1095 Lab 3 Task 1

**Student ID:** 58-0340  
**Major:** MET

## Cleaning explanation

The source contained 39 submissions and inconsistent faculty, club, city, name, email, fee, and timestamp values. I first profiled the categorical columns, then stripped and lower-cased category text and used explicit dictionaries to map every variant to the allowed faculty, club, and city names; assertions check the allowed values. I collapsed whitespace and title-cased names, trimmed and lower-cased emails, mapped yes/Y/TRUE/1 and no/N/false/0 to booleans, and parsed the ISO and slash-separated timestamps. A first date component above 12 confirms that slash dates are day/month, so I parsed them day-first. After standardization, I counted and removed 3 exact duplicate submissions, then sorted by parsed submission time and kept the latest row for each student_id and canonical club. That removed 4 resubmissions and left 32 rows. The latest submission is the best record because students commonly submitted again to update their fee status, so the newer row reflects their later information. The order matters: after exact duplicates are removed, matching on the uncleaned club text finds only 2 duplicate rows, while canonical club names reveal 4; deduplicating first would miss 2 rows and leave 34 instead of 32. I used student_id plus club as the duplicate key, never the name, so two different students with the same name are not merged. The notebook keeps the supplied CSV unchanged and writes all fixes in code.
