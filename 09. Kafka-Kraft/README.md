# Kafka Cluster with KRaft and AKHQ

Этот проект разворачивает Kafka кластер в режиме KRaft (без Zookeeper) с SASL авторизацией и веб-интерфейсом AKHQ.

## Требования

- Docker
- Docker Compose
- Внешняя сеть Traefik (для AKHQ)

## Быстрый старт

1. **Создайте необходимые файлы конфигурации:**

```
# kafka_server_jaas.conf
mkdir -p /opt/kafka
cat > /opt/kafka/kafka_server_jaas.conf << EOF
KafkaServer {
    org.apache.kafka.common.security.plain.PlainLoginModule required
    username="kafka-admin"
    password="admin_pass"
    user_kafka-admin="admin_pass"
    user_alice="alice-secret"
    user_bob="bob-secret";
};
EOF

# client.properties
cat > /opt/kafka/client.properties << EOF
security.protocol=SASL_PLAINTEXT
sasl.mechanism=PLAIN
sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="kafka-admin" password="admin_pass";
EOF
```

2. **Запустите кластер:**
```
cd /opt/kafka
docker-compose up -d
```

3. **Доступ к интерфейсам:**
  
AKHQ: https://kafka.yourdomain.com  
Логин: admin  
Пароль: admin. 
Kafka brokers: kafka:19092 (внутри сети Docker)