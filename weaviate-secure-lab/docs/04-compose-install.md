# Install Weaviate with Docker Compose

In this step, you will start the Weaviate vector database using **Docker Compose**.

Docker Compose allows you to define and run multi-container applications using a single configuration file. In this lab, Docker Compose is used to start Weaviate with all required configuration (ports, storage, and security settings) already defined.

---

## What Docker Compose is doing here

Docker Compose reads a file named `docker-compose.yml` and uses it to:
- Download the correct Weaviate container image
- Start the container with the correct configuration
- Expose the required ports
- Attach persistent storage so data is not lost
- Apply security-related settings at startup

You do **not** need to write Docker commands manually. Docker Compose handles this for you.

---

## Where the configuration file must be

The file named `docker-compose.yml` **must be located in the root of the repository**, meaning the same folder as `README.md`.

Your folder should look like this:

```
weaviate-secure-lab/
├── README.md
├── docker-compose.yml
├── docs/
└── backups/
```

If `docker-compose.yml` is not in this location, Docker Compose will fail.

---

## Start Weaviate

Make sure:
- Docker is installed
- Docker is running
- Your terminal is inside the project folder

Run the following command:

```bash
docker compose up -d
```

### What this command does
- `docker compose` tells Docker to use Docker Compose
- `up` creates and starts the services defined in the file
- `-d` means “detached mode,” so the container runs in the background

After running this command, Weaviate should start automatically.

---

## What you should see

When the command runs successfully, you will see output similar to:

```text
Creating network "weaviate-secure-lab_default" ...
Creating volume "weaviate-secure-lab_weaviate_data" ...
Creating weaviate ... done
```

This means Docker has:
- Created a network
- Created persistent storage
- Started the Weaviate container

---

## Verify the container is running

To confirm that Weaviate is actually running, run:

```bash
docker ps
```

### What success looks like

You should see a row that includes:
- A container named `weaviate`
- A status of `Up` (for example: `Up 30 seconds`)
- Ports showing `127.0.0.1:8080->8080`

This confirms that Weaviate is running.

---

## If something goes wrong

### Error: `no configuration file provided`
This means Docker Compose cannot find `docker-compose.yml`.

**Fix**
- Make sure you are inside the project folder
- Make sure the file is named exactly `docker-compose.yml`

---

### Container starts then immediately stops
This usually means there is a configuration error.

**Fix**
- Run:
  ```bash
  docker compose logs
  ```
- Look for error messages
- Do not continue until the container stays running

---

## Important notes

- Weaviate is running **locally only** and is not exposed to the network
- The container will continue running until you stop it
- You do not need to restart Weaviate unless instructed

---

Next: [Verify Weaviate is Running](05-verify-running.md)
