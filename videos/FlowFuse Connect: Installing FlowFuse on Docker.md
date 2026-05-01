# Step 1 - Create or mount your working directory
Create a directory:

````
mkdir -p demo
````

Mount it:

````
cd demo
````
# Step 2 - docker-compose.yml
Use this command to create your docker-compose.yml file:

````
cat > docker-compose.yml <<'EOF'
services:
  device-agent:
    image: flowfuse/device-agent:latest
    container_name: flowfuse-device-agent
    restart: unless-stopped
    ports:
      - "1880:1880"
    volumes:
      - ./data:/opt/flowfuse-device
EOF
````
# Step 3 - Create the data folder
Issue this command to create a data folder:

````
mkdir -p data
````
# Step 4 - Register your device
Using the install command from the FlowFuse create flow, extract the three word passphrase and insert it into this command:

````
docker compose run --rm device-agent \
  flowfuse-device-agent \
    -o three-word-passphrase \
    -u https://app.flowfuse.com \
    --otc-no-start
````
# Step 5 - Run Docker and verify
Issue the command to compose up:
````
docker compose up -d
````

Then verify it's running:

````
docker ps
````

Then go to FlowFuse.com, look in your remote instances directory, and validate it's working!
