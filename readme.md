

```
 cd .devcontainer
 podman build -t camel-jbang-ubi8 .
 podman run -dit --name camel-jbang-dev -v /home/keyamamo/Projects/vscode/Manu-AI-Usecase-Demo-2025:/workspace:z camel-jbang-ubi8 /bin/bash
```

dev container attach runnnign containerでアタッチできる

test