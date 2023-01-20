```
docker run -d \
-p 5212:5212 \
--mount type=bind,source=<path_to_your_config>,target=/cloudreve/conf.ini \
--mount type=bind,source=<path_to_your_db>,target=/cloudreve/cloudreve.db \
-v <path_to_your_uploads>:/cloudreve/uploads \
-v <path_to_your_avatar>:/cloudreve/avatar \
cloudreve/cloudreve:latest
```