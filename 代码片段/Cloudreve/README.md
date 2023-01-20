```
mkdir -vp cloudreve_data/{uploads,avatar} \
&& touch cloudreve_data/conf.ini \
&& touch cloudreve_data/cloudreve.db
```

```
docker run -d \
--name cloudreve \
-p 5212:5212 \
--restart always \
--mount type=bind,source=/root/cloudreve_data/conf.ini,target=/cloudreve/conf.ini \
--mount type=bind,source=/root/cloudreve_data/cloudreve.db,target=/cloudreve/cloudreve.db \
-v /root/cloudreve_data/uploads:/cloudreve/uploads \
-v /root/cloudreve_data/avatar:/cloudreve/avatar \
cloudreve/cloudreve:latest
```