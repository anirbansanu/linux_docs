To restart Docker, you can use the `systemctl` command to start both the `docker.service` and `docker.socket`. Here's how you can do it:

### Restart Docker Service

1. **Start the Docker service**:
   ```bash
   sudo systemctl start docker
   ```

2. **Start the Docker socket** (if it was stopped):
   ```bash
   sudo systemctl start docker.socket
   ```

### Combined Restart Command

Alternatively, you can use a combined command to restart both the Docker service and the Docker socket:
```bash
sudo systemctl start docker docker.socket
```

### Ensure Docker Starts on Boot

If you previously disabled Docker and want to ensure it starts automatically on system boot, you can enable it again:

1. **Enable the Docker service**:
   ```bash
   sudo systemctl enable docker
   ```

2. **Enable the Docker socket**:
   ```bash
   sudo systemctl enable docker.socket
   ```

### Restarting Docker in One Command

You can also restart Docker using the `restart` command:
```bash
sudo systemctl restart docker
```

This command will handle stopping and starting the Docker service, ensuring it restarts correctly.

### Summary

- **Start Docker Service and Socket**:
  ```bash
  sudo systemctl start docker docker.socket
  ```

- **Restart Docker Service**:
  ```bash
  sudo systemctl restart docker
  ```

- **Ensure Docker Starts on Boot**:
  ```bash
  sudo systemctl enable docker
  sudo systemctl enable docker.socket
  ```

Using these commands, you can manage the Docker service and ensure it runs correctly when needed.