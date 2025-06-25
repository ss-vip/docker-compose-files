# docker-compose files
在 Windows 環境，安裝 Docker desktop 使用 docker-compose 建立服務，
environment、port、volumes 依需求調整。

```bash
# build
docker-compose up -d
```

各資料夾內 yml 檔案分別為：
- gitea: [Gitea](https://docs.gitea.com/zh-tw/) 1.23.1
- gitea_runner: [Gitea Action Runner](https://docs.gitea.com/zh-tw/usage/actions/act-runner)
- jenkins: [Jenkins](https://github.com/jenkinsci/docker)
- php_apache: PHP 7.4 & Apache
- mariadb: MariaDB
- crontab-ui: [Crontab-ui](https://github.com/alseambusher/crontab-ui)
- n8n: [n8n](https://github.com/n8n-io/n8n)
