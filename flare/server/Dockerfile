FROM python:3.11-slim
WORKDIR /app

RUN pip install --no-cache-dir "nvflare>=2.5,<2.10" pyyaml pydantic numpy

COPY adapters/ /app/adapters/
COPY harmonisation/ /app/harmonisation/
COPY spec/ /app/spec/
COPY server/ /app/server/
COPY scripts/ /app/scripts/
COPY flare/app/ /app/flare/app/
COPY flare/__init__.py /app/flare/__init__.py
COPY sites.yaml projects.yaml /app/

ENV PYTHONPATH=/app SERVER_OUT=/server_out

EXPOSE 8002
EXPOSE 8003

CMD ["bash", "-c", "mkdir -p /workspace && cp -r /etc/secrets/* /workspace/ && if [ \"$ROLE\" = \"server\" ]; then bash scripts/start_server.sh; else bash scripts/start_client.sh; fi"]
