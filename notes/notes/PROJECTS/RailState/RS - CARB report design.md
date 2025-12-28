CARB email report

### 4. **Report Generation and Delivery**
- **T5.1** Generate per-sensor Excel sheet. (Columns: sensor ID, locomotive ID ACC, inoperative days, uptime.)
- **T5.2** Generate summary. (average values for each category)
- **T6.1** Compose email with summary and attach Excel report.
- **T6.2** Send report to CARB mailing list by the 15th of each month.

---

The final report is an email that should contain the following values:

- **per-sensor inoperative days count**: int - top 5 + all sensors with more than 15 inoperative days?
- **human readable Locomotive ID accuracy**: float
- **railcar type accuracy**: float
- **Emissions Tier recognition ratio**: float
- **Container type matching ratio**: float

Per-sensor columns:
- sensor, locomotive ACC (loccomotive grouping), uptime/downtime

summary:
- locomotive ACC (per-sensor loco)
- emission tier recognition: float (CSV api request)
- railcar type matching: float (per-sensor summary)
- container type acc: float (per-sensor summary)


```
curl 'http://localhost:5002/api/v1/visit-previews?page=0&page_size=10' -H "Authorization: Bearer $TOKEN"
```


```
gcloud builds list --limit=50 --page-size=50 \
  --format="csv(id, status, substitutions.REPO_NAME, substitutions.BRANCH_NAME, substitutions.TRIGGER_NAME, createTime)" \
  | awk -F',' 'NR==1 {print "ID,STATUS,REPO,BRANCH,TRIGGER,TIME"; next}
  {print $1","$2","$3","substr($4,1,30)","substr($5,1,30)","$6}' \
  | column -t -s',' \
  | GREP_COLORS='ms=01;32' grep --color=always -E 'SUCCESS|$' \
  | GREP_COLORS='ms=01;33' grep --color=always -E 'WORKING|$' \
  | GREP_COLORS='ms=01;31' grep --color=always -E 'FAILURE|$'

```