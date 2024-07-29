# Usage

1. copy and paste the requeired dev container
2. Copy the specific service present in the docker compose that is referenced in the .devcontainer.json file
3. Edit the workspace path to your respective folder at devcontainer.json and Dockerfile
4. Expose required volume

Example:
devcontainer.json

```

{
	"name": "Hello World", # My project name
	"dockerComposeFile": [
		"../../docker-compose.yml"
	],
	"service": "node",
	"workspaceFolder": "/workspace/hello_world",
	"forwardPorts": [
		"3002:3000",
		"8000:8000"
	],
	"customizations": {
		"vscode": {
			"extensions": [
				"ms-azuretools.vscode-docker",
				"mquandalle.graphql",
				"Prisma.prisma",
				"GitHub.copilot",
				"GitHub.copilot-chat"
			]
		}
	}
}
```

DockerFile

```
FROM node:20.7.0-alpine

WORKDIR  /workspace/hello_world
```

docker-compose.yml

```
  node:
    build:
      dockerfile: ./.devcontainer/node/DockerFile
    container_name: hello_world
    stdin_open: true
    tty: true
    volumes:
      - ./:/workspace/hello_world
    ports:
      - 3001:3000
    depends_on:
      - meta
```
