# docker-gitea
在 Windows 環境，安裝 Docker desktop 做 Gitea 服務，
environment、port、volumes 需調整。

```bash
# build
docker-compose up -d
```

各資料夾內 Compose 檔案分別為：
- gitea: [Gitea](https://docs.gitea.com/zh-tw/) 1.23.1
- gitea_runner: [Gitea Action Runner](https://docs.gitea.com/zh-tw/usage/actions/act-runner)

其他：
- jenkins: [Jenkins](https://github.com/jenkinsci/docker)
- php_apache: PHP 7.4 & Apache
- mariadb: MariaDB
- crontab-ui: [Crontab-ui](https://github.com/alseambusher/crontab-ui)
