# Secrets Configuration

This folder intentionally does not contain 
actual secret values for security reasons.

## How to create the required secrets:

### PostgreSQL credentials
kubectl create secret generic pg-secrets \
  --from-literal=POSTGRES_PASSWORD='your_password'

### MySQL credentials
kubectl create secret generic mysql-secrets \
  --from-literal=MYSQL_ROOT_PASSWORD='your_password'

### pgAdmin credentials
kubectl create secret generic pgadmin-secrets \
  --from-literal=PGADMIN_DEFAULT_EMAIL='admin@example.com' \
  --from-literal=PGADMIN_DEFAULT_PASSWORD='your_password'

### TLS certificate for Ingress
openssl genrsa -out tls.key 2048
openssl req -new -x509 -key tls.key -out tls.crt \
  -days 365 -subj "/CN=pgadmin.local"

kubectl create secret tls pgadmin-tls \
  --cert=tls.crt --key=tls.key
