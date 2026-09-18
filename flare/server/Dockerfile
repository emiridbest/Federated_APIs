# FLARE server (orchestrator)
FROM python:3.11-slim
WORKDIR /app

# Install dependencies
RUN pip install --no-cache-dir "nvflare>=2.5,<2.10" pyyaml pydantic numpy uvicorn

# Copy source
COPY adapters/ /app/adapters/
COPY harmonisation/ /app/harmonisation/
COPY spec/ /app/spec/
COPY server/ /app/server/
COPY scripts/ /app/scripts/
COPY flare/app/ /app/flare/app/
COPY flare/__init__.py /app/flare/__init__.py
COPY sites.yaml projects.yaml /app/

# Copy and unpack the server kit
COPY flare/kits/server.tgz /workspace/
RUN mkdir -p /workspace && tar xzf /workspace/server.tgz -C /workspace

ENV PYTHONPATH=/app SERVER_OUT=/server_out

# Expose ports for Render
EXPOSE 8002
EXPOSE 8003

# Always start uvicorn on port 8002
CMD ["uvicorn", "flare.app.server:app", "--host", "0.0.0.0", "--port", "8002"]
