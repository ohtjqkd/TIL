DB 추가
Resource -> find add-ons -> heroku postgress [무료]

## GitActions setting
프로젝트에 .github 디렉토리 생성
.github/workflows 디렉토리 생성
.github/workflows/deploy.yml
```
name: Deploy

on:
  push:
    branches: [ main ]
  workflow_dispatch:


jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3
      - name: Deploy to Heroku
        uses: AkhileshNS/Heroku-deploy@v3.12.12
        with:
          heroku_api_key: ${{ secrets.HEROKU_DEPLOY_KEY }}
          heroku_email: ohtjqkd@gmail.com
          heroku_app_name: [app name]
```

./Profile
```
web: java -Dserver.port=$PORT $JAVA_OPTS -jar build/libs/{project_name}-0.0.1-SNAPSHOT.jar
```

./system.properties
```
java.runtime.version={version}
```

Github -> repository -> setting -> secret key
new repository key
HEROKU_DEPLOY_KEY에 heroku api key 넣기