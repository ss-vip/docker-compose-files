# docker-compose files

### 在 Windows 環境，安裝 Docker desktop 使用 docker-compose 建立服務。

> environment、port、volumes 依需求調整。

```bash
# build
docker-compose up -d
```

### 各資料夾內 yml 檔案分別為：
- gitea: [Gitea](https://docs.gitea.com/zh-tw/) 1.23.1
- gitea_runner: [Gitea Action Runner](https://docs.gitea.com/zh-tw/usage/actions/act-runner)
- jenkins: [Jenkins](https://github.com/jenkinsci/docker)
- php_apache: PHP 7.4 & Apache
- mariadb: MariaDB
- crontab-ui: [Crontab-ui](https://github.com/alseambusher/crontab-ui)
- n8n: [n8n](https://github.com/n8n-io/n8n)

---

### Security workflows

Semgrep + Trivy 輸出 SARIF，將 yaml 檔案存於 `.github\workflows` 路徑內使用，適合 Github、Gitea actions 使用。

> 漏洞 + 密鑰 + IaC 掃描紀錄與合併阻擋

```yaml
name: Security Audit to SARIF
on: [push, pull_request]

jobs:
  scan:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      # SARIF 存放資料夾
      - name: Create Reports Directory
        run: mkdir -p reports

      # 1. Semgrep 輸出 SARIF
      - name: Install Semgrep
        run: pip install --break-system-packages --ignore-installed semgrep

      # 顯示 log
      - name: Show Semgrep Findings
        run: semgrep scan --config="p/security-audit" --severity ERROR || true

      - name: Run Semgrep SAST
        run: semgrep scan --config="p/security-audit" --sarif --output=reports/semgrep-results.sarif --error --severity ERROR

      # 2. Trivy 輸出 SARIF
      - name: Install Trivy
        run: |
          curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sh -s -- -b /usr/local/bin

      # 顯示 log
      - name: Show Trivy Findings
        run: trivy fs --scanners vuln,secret,config --format table --severity HIGH,CRITICAL . || true

      - name: Run Trivy SCA
        run: trivy fs --scanners vuln,secret,config --format sarif --output reports/trivy-results.sarif --exit-code 1 --severity HIGH,CRITICAL .

      # 3. SARIF 存檔
      - name: Upload SARIF Artifacts
        uses: actions/upload-artifact@v3
        with:
          name: security-sarif-reports
          path: reports/
```
