# anythingllm_addon/Dockerfile
ARG BUILD_FROM=ghcr.io/hassio-addons/base/amd64:8.0.6

FROM $BUILD_FROM

LABEL maintainer="artemis"

# Install any system packages that AnythingLLM needs
RUN apk add --no-cache \
    python3 py3-pip git ca-certificates && \
    update-ca-certificates

# Create a user for the service (optional but good practice)
RUN adduser -D anythingllm

WORKDIR /opt/anythingllm

# Clone or copy your AnythingLLM repo
# For demo purposes we clone a placeholder repo.
# Replace this with the real repository you want to run.
RUN git clone https://github.com/Mintplex-Labs/anything-llm.git . && \
    pip install --no-cache-dir -r requirements.txt

# Set permissions
RUN chown -R anythingllm:anythingllm /opt/anythingllm

USER anythingllm

# Expose the web GUI port (Streamlit default)
EXPOSE 8501

# Entrypoint that starts AnythingLLM
ENTRYPOINT ["python", "-m", "streamlit", "run", "app.py", "--server.port=8501"]