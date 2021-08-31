- Задание_1
- составьте Dockerfile-манифест для elasticsearch
```
FROM centos:7

RUN cd /opt && \
	curl https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.13.3-linux-x86_64.tar.gz \
		> elasticsearch-7.13.3-linux-x86_64.tar.gz && \
	curl https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.13.3-linux-x86_64.tar.gz.sha512 \
		> elasticsearch-7.13.3-linux-x86_64.tar.gz.sha512 && \
	sha512sum -c elasticsearch-7.13.3-linux-x86_64.tar.gz.sha512 && \
	tar -xzf elasticsearch-7.13.3-linux-x86_64.tar.gz && \
	rm -f elasticsearch-7.13.3-linux-x86_64.tar.gz* && \
	useradd -r es_user && \
	chown -R es_user /opt/elasticsearch-7.13.3/

WORKDIR /opt/elasticsearch-7.13.3/

RUN	mkdir -p /var/lib/elasticsearch && \
	chown -R es_user /var/lib/elasticsearch && \
	echo 'node.name: netology_test' >> config/elasticsearch.yml && \
	echo 'path.data: /var/lib/elasticsearch' >> config/elasticsearch.yml && \
	echo 'network.host: 0.0.0.0' >> config/elasticsearch.yml && \
	echo 'discovery.type: single-node' >> config/elasticsearch.yml && \
	echo 'xpack.security.enabled: false' >> config/elasticsearch.yml && \
        echo 'path.repo: /opt/elasticsearch-7.13.3/snapshots' >> config/elasticsearch.yml && \
	mkdir snapshots && chown es_user snapshots

EXPOSE 9200
USER es_user
ENTRYPOINT ["bin/elasticsearch"]
```

- Задание_2






