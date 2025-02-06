---
title: Open Source Deep Research
date: 2025-02-06
draft: false
tags:
  - NetworkChuck
---


## Clone the project

```bash
git clone https://github.com/dzhng/deep-research.git
cd deep-research

```


## .env.local file

```yml
FIRECRAWL_KEY="your_firecrawl_key"
OPENAI_KEY="your_openai_key"
# Optionally, for self-hosted Firecrawl:
# FIRECRAWL_BASE_URL="http://localhost:3002"

```
## Dockerfile

```yml
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

CMD ["npm", "start"]

```


## Docker Compose File

```yml
version: '3.8'
services:
  deep-research:
    build: .
    env_file:
      - .env.local
    tty: true
    stdin_open: true
```

## Make a change to the *package.json* file

### Change this:

`"start": "tsx --env-file=.env.local src/run.ts"`

### to this:

`"start": "tsx src/run.ts"`

## Run The Container

```bash
docker compose run --rm deep-research
```