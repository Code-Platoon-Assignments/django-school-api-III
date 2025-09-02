FROM mcr.microsoft.com/devcontainers/base:ubuntu

# Install PostgreSQL server + client
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get install -y postgresql postgresql-contrib \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Environment vars for postgres setup
ENV POSTGRES_USER=vscode \
    POSTGRES_PASSWORD=codeplatoon \
    POSTGRES_DB=vscode

# Create a startup script to initialize the DB
RUN service postgresql start && \
    sudo -u postgres psql -c "CREATE USER ${POSTGRES_USER} WITH PASSWORD '${POSTGRES_PASSWORD}';" && \
    sudo -u postgres psql -c "ALTER USER ${POSTGRES_USER} WITH SUPERUSER;" && \
    sudo -u postgres psql -c "CREATE DATABASE ${POSTGRES_DB} OWNER ${POSTGRES_USER};"

EXPOSE 5432

# Start PostgreSQL automatically
CMD ["bash", "-c", "service postgresql start && tail -f /dev/null"]
