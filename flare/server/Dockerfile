# FLARE server (orchestrator) -- sits OUTSIDE every TRE. Never sees row-level data.
FROM python:3.11-slim

# Set working directory
WORKDIR /app

# Install NVFLARE and dependencies
RUN pip install --no-cache-dir "nvflare>=2.5,<2.10" pyyaml pydantic numpy

# Copy project source
COPY adapters/ /app/adapters/
COPY harmonisation/ /app/harmonisation/
COPY spec/ /app/spec/
COPY server/ /app/server/
COPY scripts/ /app/scripts/
COPY flare/app/ /app/flare/app/
COPY flare/__init__.py /app/flare/__init__.py
COPY sites.yaml projects.yaml /app/

# Copy and unpack the server kit (generated during provisioning)
COPY flare/kits/server.tgz /workspace/
RUN mkdir -p /workspace && tar xzf /workspace/server.tgz -C /workspace

# Environment variables
ENV PYTHONPATH=/app SERVER_OUT=/server_out

# Expose NVFLARE ports
EXPOSE 8002
EXPOSE 8003

# Start the NVFLARE server using its startup script
CMD ["bash", "-c", "if [ -f /workspace/federated_apis/prod_00/flare-server/startup/start.sh ]; then bash scripts/start_server.sh; else echo 'no server kit in /workspace; idling'; sleep infinity; fi"]
