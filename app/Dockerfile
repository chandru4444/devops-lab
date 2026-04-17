# Stage 1 — builder
FROM python:3.12-slim AS builder

WORKDIR /build

COPY requirements.txt .

RUN pip install \
    --no-cache-dir \
    --prefix=/build/install \
    -r requirements.txt

# Stage 2 — final
FROM python:3.12-slim

WORKDIR /app

COPY --from=builder /build/install /usr/local
COPY app.py .

ENV REDIS_HOST=redis

EXPOSE 5000

CMD ["gunicorn", "--bind", "0.0.0.0:5000", "app:app"]
