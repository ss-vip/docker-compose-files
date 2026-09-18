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

Semgrep + Trivy 輸出 HTML 及 SARIF 檔案，請將 [security-scan.yaml](https://github.com/ss-vip/docker-compose-files/blob/main/gitea_runner/security-scan.yaml) 檔案存於 `.github\workflows` 路徑內使用，適合 Github actions、Gitea actions 使用。

- 檢查 CVE、SECRET、MISCONFIG 掃描
- 檢查掃描工具版本及新版本提示
- 掃描紀錄與報告 html 檔案生成
