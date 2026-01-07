name: Dormant Users Audit

on:
  schedule:
    - cron: "0 2 1 * *"   # Monthly
  workflow_dispatch:

jobs:
  audit:
    runs-on: ubuntu-latest
    steps:
      - name: Run Dormant Users Report
        uses: your-org/github-dormant-users-action@v1
        with:
          github_token: ${{ secrets.ORG_AUDIT_TOKEN }}
          org_names: my-org,subsidiary-org
          days_inactive_threshold: 90

      - name: Upload report
        uses: actions/upload-artifact@v4
        with:
          name: dormant-users-report
          path: "*.csv"
