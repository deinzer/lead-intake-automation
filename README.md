# Practical Build 1: Lead Intake

## Local environment

Docker Desktop runs n8n in a container: a packaged application with its own dependencies.
The compose.yaml file describes how to run it.

- `image` selects the n8n package to download.
- `127.0.0.1:5678:5678` makes the editor reachable from this Mac at http://localhost:5678.
- `Europe/Berlin` sets the timezone for schedules.
- `n8n_data` stores workflows, credentials and execution history separately from the container.

In a terminal opened in this folder, with Docker Desktop running:

```sh
docker compose up -d
```

This downloads n8n if needed and starts it in the background.

```sh
docker compose stop
```

This stops n8n while keeping your workflows. Start again with `docker compose up -d`.
Avoid `docker compose down -v`: it removes the data volume.
Local workflows run only while Docker and n8n are running and the Mac is awake.

## Learning sequence

1. Start n8n and create your local owner account.
2. Build Manual Trigger → Edit Fields using a fictional lead.
3. Add validation and route demo requests versus other enquiries.
4. Replace the manual input with a POST webhook; send sample JSON.
5. Save leads in an n8n Data Table and return a response.
6. Export the workflow JSON and make a Git checkpoint.
7. Add AI extraction, validate its output, and test missing or ambiguous details.

Git records local checkpoints of files. GitHub can hold a remote copy later.
Exported workflows must be checked for embedded credentials and personal data before committing.
Use fictional leads while learning.

## Sources

- https://docs.n8n.io/deploy/host-n8n/install-options/install-with-docker
- https://docs.docker.com/desktop/setup/install/mac-install/

##
## Workflow v1

Receives a lead through a POST webhook, validates required fields,
calculates a lead score, routes qualified and nurture leads, stores every
outcome in `lead_registry`, and returns a JSON response.
