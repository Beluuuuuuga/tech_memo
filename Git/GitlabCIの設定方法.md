## 資料
### [GitLab CIでユニットテストを自動化する](https://techblog.nhn-techorus.com/archives/12531)
- Pythonで設定する方法が記載されている

### [Continuous Integration With GitLab in 20 Minutes - An Easy Introduction](https://www.srcmake.com/home/gitlabci)
- C++で設定する方法
- [sample-gitlabci-cpp-project](https://github.com/srcmake/sample-gitlabci-cpp-project) 
  - リポジトリ

- chmodで権限を付与しないとエラーになるので注意

```
deploy_Staging:
  stage: deploy
  script: 
    - ls -lsa ./scripts
    - whoami
    - chmod +x ./scripts/RancherDeploy.sh
    - ./scripts/RancherDeploy.sh -k $RANCHERACCESS -s $RANCHERSECRET -a $STAGING_ID
  environment:
    name: Staging
    url: https://Staging.app.net
```

### [.travis.yml](https://github.com/emchristiansen/Billy/blob/master/.travis.yml)
- opencv4のbefore scriptが参考になりそう
