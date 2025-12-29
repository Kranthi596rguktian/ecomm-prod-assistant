Project-Github-Link: https://github.com/sunnysavita10/ecomm-prod-assistant

These are all the commands that you need to run on your command prompt

1.	Write Python in your terminal
2.	If you have Python, then no need to install it
3.	 uv --version
4.	If you are not able to get the version
5.	Pip install uv
6.	import shutil
7.	print(shutil.which("uv"))
8.	 
9.	 6. Uv init <my-project-name>
10.	7. uv pip list
11.	 
12.	8. uv python list
13.	uv venv env --python cpython-3.10.18-windows-x86_64-none
14.	uv venv <your-env-namne> --python <your-python-version>
15.	Note: Please use either 3.10, 3.11, or 3.12
16.	Command Prompt (CMD)  .\<your-env-nanme>\Scripts\activate.bat
17.	Git Bash ya WSL terminal, or MAC Terminal:
a.	source <your-env-nanme>/Scripts/activate
b.	
18. If your git is asking for a login to publish the repo, execute the command below
c.	git config --global user.name "Your Name"
d.	git config --global user.email "your-email@example.com"
19. UV add <package_name>
20. Uv add -r requirements.txt
21. Streamlit run <give your streamlit python filename>
22. Install the live server extension in VS Code for testing the HTML

For accessing the DataStax, here is a link: https://accounts.datastax.com/session-service/v1/login


# ecomm-prod-assistant

A small utility project that provides an API and Streamlit UI to assist with product-related tasks for e-commerce workflows (search, ingestion, and small assistant features). This README gives a concise overview, setup steps, and common commands to run locally, with Docker, and for basic deployment.

## Key links
- Repository: https://github.com/sunnysavita10/ecomm-prod-assistant
- DataStax login: https://accounts.datastax.com/session-service/v1/login
- Vector DB comparison: https://superlinked.com/vector-db-comparison

## Overview
This repository contains a FastAPI backend and a Streamlit frontend to prototype product assistant features. It also includes helper scripts, workflows, and example MCP servers for local testing.

## Features
- FastAPI application (API endpoints)
- Streamlit UI for rapid testing
- MCP server examples and agentic workflows
- Dockerfile for containerized runs

## Prerequisites
- Python 3.10, 3.11, or 3.12 recommended
- Git
- Docker (for container runs)
- (Optional) AWS CLI and kubectl for deployments

## Quick setup (recommended)
1. Create and activate a virtual environment

	Windows (CMD):
	```powershell
	python -m venv .venv
	.\.venv\Scripts\activate.bat
	```

	Git Bash / WSL / macOS:
	```bash
	python -m venv .venv
	source .venv/bin/activate
	```

2. Install dependencies

	```bash
	pip install -r requirements.txt
	```

Notes: This project previously referenced `uv` commands (a wrapper environment). You can use them if you have `uv` installed, otherwise standard Python/`pip` commands above work.

## Running locally

- Start the FastAPI app (adjust module path if your package name differs, e.g. `product_assistant` vs `prod_assistant`):

```bash
uvicorn prod_assistant.router.main:app --reload --port 8000
# or if your package name is `product_assistant`:
uvicorn product_assistant.router.main:app --reload --port 8000
```

- Run the Streamlit UI (replace with the actual Streamlit file you want to run):

```bash
streamlit run scrapper_ui.py
# or
streamlit run <your_streamlit_file.py>
```

- Some local MCP servers or workflows used for testing live features are under `prod_assistant/mcp_servers/` and `prod_assistant/workflow/` (or `product_assistant/*` depending on your package name). Example test files referenced in earlier notes:

```text
prod_assistant/mcp_servers/product_search_server.py
prod_assistant/workflow/agentic_workflow_with_mcp_websearch.py
# Update the paths to match your workspace if you have `product_assistant` instead of `prod_assistant`.
```

## Docker

- Build the image:

```bash
docker build -t prod-assistant .
```

- Run a container (port mapping example):

```bash
docker run -d -p 8000:8000 --name product-assistant prod-assistant
```

Useful Docker commands:

```bash
docker ps
docker stop <container_id>
docker rm <container_id>
docker images
docker rmi <image_id>
```

## Deployment / Kubernetes (quick commands)

After pushing images and creating resources in AWS EKS, common troubleshooting and inspection commands:

```bash
aws eks update-kubeconfig --name <eks-cluster-name> --region <aws-region>
kubectl get nodes
kubectl get svc -o wide
kubectl describe svc <service-name>
kubectl get pods -o wide
kubectl logs <pod-id>
```

## Secrets and environment variables
The project references several secrets used for deployment and external services. Store these in your CI/CD secret manager (do NOT commit them):

- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_REGION`
- `ECR_REGISTRY`
- `ECR_REPOSITORY`
- `EKS_CLUSTER_NAME`
- `GROQ_API_KEY`
- `GOOGLE_API_KEY`
- `ASTRA_DB_API_ENDPOINT`
- `ASTRA_DB_APPLICATION_TOKEN`
- `ASTRA_DB_KEYSPACE`

## Notes about packaging
- To install this project in editable mode (local development):

```bash
pip install -e .
# or install from `requirements.txt` if it contains `-e .`
pip install -r requirements.txt
```

## Project structure (top-level)
- `main.py` — project entry / examples
- `scrapper_ui.py` — Streamlit UI
- `requirements.txt` — Python dependencies
- `product_assistant/` (or `prod_assistant/`) — main package code
- `templates/`, `static/` — frontend assets

## Contributing
- Open an issue or submit a PR. Keep changes focused and add tests where applicable.

## License
This repository does not specify a license in the README. Add a `LICENSE` file if you intend to publish under a specific license.

---

