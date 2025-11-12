# Sarusctl 

Turning an EDF into a running container, with minimal friction.
`sarusctl` standardizes how you go from "recipe" to "runnable" containerized deployment.
Give it a EDF file and it will validate it, show you exactly what it resolves to, pulls and migrate the image if needed, and run the container using Podman with sane HPC defaults. Accelerating working with high performance containers with Podman on HPC systems.

## Why it matters
* One file in, one predictable run out. EDF becomes a container with the same steps everywhere. No snowflake deployments.
* Delivery without friction. `sarusctl` pulls the image (if needed), migrates it into a read-only store with Parallax, and launches with ephemeral settings.
* Built-in guardrails. `validate` helps you catch errors early.
* Portable binary, repeatable builds. Prebuilt binaries for amd64 and arm64; devcontainer config ships a static optimized Rust build.

## What sarusctl simplifies for you

* Understands your EDF. It parses the EDF via the `raster` library for validation and rendering. You get clear debugging information or a concrete, pretty printed plan.
* Builds the right Podman contexts. `sarusctl` setups and manages the correct Podman contexts to ensure a consistent setup.
* Pulls and migrates of images on demand. If the image is not present in the RO store in the parallel Filesystem, it pulls with Podman and then migrates it with Parallax, then runs from the EDF.
* Keeps host clean. Runs with managed temporal directories and a read-only imagestore for fast, low-friction work.

## Getting started

* Prebuilt artifacts. CI builds both amd64 and arm64 artifacts.
* Build locally
  ```bash
  cargo build --release
  ./target/release/sarusctl --help
  ```
* Quickstart
  ```bash
  # Check the EDF recipe
  sarusctl validate my_env.edf
  
  # Run it
  sarusctl run my_env.edf cat /etc/os-release
  ```
  
