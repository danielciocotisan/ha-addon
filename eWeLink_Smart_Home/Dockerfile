# ARG BUILD_FROM
# FROM $BUILD_FROM

FROM node:14-slim

ENV CK_API_ENV=prod

# Repară sursele Debian Buster care nu mai sunt disponibile
RUN sed -i 's|http://deb.debian.org|http://archive.debian.org|g' /etc/apt/sources.list && \
    sed -i '/security/d' /etc/apt/sources.list && \
    apt-get update && apt-get install -y python build-essential && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Pregătește directorul de lucru
RUN mkdir -p /workspace/node_modules

# Copiază fișierele aplicației
COPY ["./dist", "./package.json", "/workspace/"]

# Setează directorul de lucru
WORKDIR /workspace

# Instalează dependențele
RUN npm install --production

# Pornește aplicația (înlocuiește dacă folosești alt fișier de start)
CMD ["node", "dist/index.js"]
