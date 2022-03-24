# Applied AI Handbook

This repo contains the [harrison.ai](https://harrison.ai) Applied AI Team (`hai`) engineering handbook.
It holds publicly accessible documentation describing the team and our ways of working.

# Teams

## Venture AI

_Delivering best-in-class models into AI products_

This team works directly with engineering, clinical and product teams within a venture to develop and deploy models for a specific use-case.

## AI Platform

_Building the machine that builds the machine_

This team works on the core platform used by venture AI Teams. They build the tools and infrastructure to support and standardise `mlops` across Harrison.


# Tech stack

## Python

Working in the machine learning domain we've adopted `python` as our lingua-franca.
We are at one with the [zen](https://peps.python.org/pep-0020/#the-zen-of-python) of `python3.8` and think 
[PEP-484](https://peps.python.org/pep-0484/) (type-hints) was the best thing since sliced bread.

### Toolchain

Python has many limitations out of the box.
However, every line of python code generally runs the following gauntlet before being merged:

```
pytest
mypy
pylint
black
isort
pycln
snyk
```

We use `poetry` for packaging and dependency management.
`git` and `Github` for source control with `Github Actions` for `CI/CD` and `Github Pages` for package documentation.
We like the [Gitflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) branching model too.

Private packaging happens on `AWS CodeArtifact`.

We `make` and containerise _all-the-things_ using `docker-compose` and the [3musketeers](https://3musketeers.io/docs/patterns.html#make) pattern and use `cookiecutter` templates for new packages and projects.

Most of team runs `VS Code` and we're currently exploring scalable, containerised remote-development (e.g. [gitpod](https://www.gitpod.io/)).

### Frameworks and Packages

We like `dataclasses` and especially `pydantic` for data structures and configuration. 

#### Machine learning

We sit precariously on both sides of the `pytorch` vs. `tensorflow` debate and have found a way to love both. That being said we expect to `import pytorch` and specifically `pytorch-lightning` more often going forward.

We manage hierarchical model configuration with `hydra`.

Other key packages include `numpy`, `einops`, `boto3`, `scikit-learn`, `tqdm`, `fire`, `matplotlib`, `Pillow`, `opencv`, `pandas`, `plotly`, `pydicom`, `jupyterbook` and `dunamai`.

For compute jobs where `concurrent.futures` doesn't cut it, we pickup frameworks like `ray` and `dask` to get the job done.

#### Services

`HTTP/S` and `REST` is our default API regime and `FastAPI` the framework of choice.
`newman` keeps us honest for API integration tests.

## Infrastructure

We run what we can in the cloud on `AWS`, making use of `S3`, `EC2`, `Athena`, `Lambda` and `EKS` the most amongst an ever growing list of services.

We like `kubernetes` and `helm` for service deployment with `terraform` for infrastructure-as-code.

We also run a serious amount of hardware on-prem for machine learning workloads. Our core infrastructure comprises 8 NVIDIA DGX A100 systems.

Some key stats:
- 20 petaFLOPS Tensor F32 from 64 80GB A100 GPUs
- 5 TB GPU Memory with 2 TB/s Memory Bandwidth
- 2,048 CPU Cores and 16 TB System Memory
- 254 TB Networked Storage with 800Gb Connectivity

We also have 4 legacy DGX workstations that we still use for smaller experiments.
This cluster talks to our cloud assets via `Direct Connect` with a 10Gpbs pipe.

We schedule jobs on the cluster using `slurm` and `ray`.

## Communications

We run sprints from `JIRA` and land most (non-code) documentation in `Confluence`.

We're currently in Microsoft land using `Teams` and `Office365` for comms.