# ABOUT
Easy to reach backup.

# USED ELEMENTS
postgres: PostgreSQL database server (version 16.2) named postgres. Uses a volume to persist data (./data/postgres:/var/lib/postgresql/data).

pgbackups: Creates backups of the PostgreSQL database (postgres) using the prodrigestivill/postgres-backup-local image. Backups are stored in a volume (./data/postgres_backup:/var/opt/pgbackups). Configure scheduling and retention with environment variables.

pgadmin: Provides a web interface (port 8888) for managing the PostgreSQL database using the dpage/pgadmin4 image. Uses a volume to persist user data (./data/pgadmin-data:/var/lib/pgadmin).

keycloak: Keycloak server (version 24.0.1) named auth_keycloak for user authentication and authorization. Relies on the postgres service for its database and configures the connection details through environment variables.

apisix: API Gateway (Apache APISIX version 3.8.0) named apisix. Uses a volume to mount the configuration file (./apisix_conf/config.yaml:/usr/local/apisix/conf/config.yaml). Depends on the etcd service for service discovery.

etcd: etcd distributed key-value store (Bitnami image, version 3.5.11) named etcd. Uses a volume to persist data (./data/etcd_data:/bitnami/etcd).

apisix-dashboard: Web UI (port 9009) for managing the APISIX gateway using the apache/apisix-dashboard image. Depends on the apisix service.

rabbitmq: Message broker (RabbitMQ version 3.12.13) named rabbitmq. Uses volumes to persist data (./data/rabbitmq_data:/var/lib/rabbitmq) and logs (./data/rabbitmq_log/log:/var/log/rabbitmq).

redis-cache: In-memory data store (Redis version 7.2.4). Uses a volume to persist data (./data/redis_cache:/data).

redis-gui: Web UI (port 5540) for managing the Redis cache using the oblakstudio/redisinsight image.


## USED PORTS
 - postgres: None explicitly exposed
 - pgbackups: Uses port 8080 for health checks if configured (HEALTHCHECK_PORT=8080)
 - pgadmin: 8888
 - keycloak: 8080
 - apisix: 9180, 9080, 9091, 9446, 9092
 - etcd: 2379
 - apisix-dashboard: 9009
 - rabbitmq: 5672, 15672
 - redis-cache: 6379
 - redis-gui: 5540