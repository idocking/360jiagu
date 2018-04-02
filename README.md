360jiagu
========

容器化360加固Linux版

```bash
docker run -it --rm -e USERNAME=username -e PASSWORD=password -e KEYSTORE_PATH=/output/keystore.jks -e KEYSTORE_PASSWORD=123456 -e ALIAS=alias -e ALIAS_PASSWORD=123456 -v $PWD:/output idocking/360jiagu:latest jiagu /output/app-release-unsigned.apk /output -autosign
```