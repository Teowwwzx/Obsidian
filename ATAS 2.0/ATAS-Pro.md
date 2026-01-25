http://localhost:8081/

http://localhost:3003/d/adlklp6/atas-pro?orgId=1&from=now-30m&to=now&timezone=Asia%2FKuala_Lumpur&refresh=10s

http://localhost:9000/#!/3/docker/containers


![[Pasted image 20260125175111.png]]
### Detailed Implementation 1. Production Process Manager ( Dockerfile & requirements.txt )
I switched your entry command to use Gunicorn . This is the industry standard for Python web apps because it handles process signals and worker management much better than raw Uvicorn.

Dockerfile

```
# Added Healthcheck (Standard for K8s/AWS ECS)
HEALTHCHECK --interval=30s --timeout=30s --start-period=5s --retries=3 \
  CMD curl -f http://localhost:8000/health || exit 1

# Switched to Gunicorn with Uvicorn workers
CMD ["gunicorn", "app.main:app", "--workers", "4", "--worker-class", "uvicorn.
workers.UvicornWorker", "--bind", "0.0.0.0:8000"]
``` 2. Health Check Endpoint
I added a lightweight /health endpoint. This is crucial for Load Balancers (AWS ALB / Nginx) to know if they can send traffic to this container.

main.py

```
@app.get("/health")
def health_check():
    return {"status": "ok", "version": "1.0.0"}
``` 3. Auto-Migrations
Your docker-entrypoint.sh had migrations commented out. In a modern CI/CD flow, you want the application to ensure the DB is ready before accepting traffic.

docker-entrypoint.sh

```
# Uncommented for automation
echo "Running database migrations..."
alembic upgrade head
```