SonarQube (with persistence) + Community Branch

This is not working

```sh
docker run -d \
  --name sonarqube \
  --restart unless-stopped \
  -p 9000:9000 \
  -v sonarqube_data:/opt/sonarqube/data \
  -v sonarqube_logs:/opt/sonarqube/logs \
  -v sonarqube_extensions:/opt/sonarqube/extensions \
  mc1arke/sonarqube-with-community-branch-plugin:latest
```

```sh
docker rm -f sonarqube || true
```

This was working

```sh
docker run -d \
  --name sonarqube \
  --restart unless-stopped \
  -p 9000:9000 \
  mc1arke/sonarqube-with-community-branch-plugin:latest
```

```sh
# Stop the container first (optional but safe)
docker rm -f sonarqube || true

# Change owner inside the volumes to UID 1000 (Sonar user)
docker run --rm -v sonarqube_data:/data alpine sh -c "chown -R 1000:1000 /data || true; chmod -R u+rwX /data || true"
docker run --rm -v sonarqube_logs:/data alpine sh -c "chown -R 1000:1000 /data || true; chmod -R u+rwX /data || true"
# If you have an extensions volume
docker run --rm -v sonarqube_extensions:/data alpine sh -c "chown -R 1000:1000 /data || true; chmod -R u+rwX /data || true"

# Start container again
docker run -d --name sonarqube --restart unless-stopped -p 9000:9000 \
  -v sonarqube_data:/opt/sonarqube/data \
  -v sonarqube_logs:/opt/sonarqube/logs \
  -v sonarqube_extensions:/opt/sonarqube/extensions \
  mc1arke/sonarqube-with-community-branch-plugin:latest
```
