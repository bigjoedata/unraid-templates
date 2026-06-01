# Unraid Templates - Slopsmith & Companion Services

A collection of Unraid Docker templates to easily deploy and run the **Slopsmith** stack on your Unraid server.

## Available Templates

### 1. Slopsmith Core (`slopsmith`)
The main Slopsmith web application for browsing, playing, and practicing Rocksmith 2014 custom songs (CDLC).
* **Registry**: `ghcr.io/bigjoedata/slopsmith:latest` (or `ghcr.io/slopsmith/slopsmith:latest`)
* **Default Port**: `7000` (safe, unblocked by web browsers)
* **Volumes**:
  * `/dlc` — Map to your Rocksmith CDLC folder (Read-Only recommended).
  * `/config` — Map to your appdata directory for DB, caches, and persistent files.
* **Dynamic Plugins**:
  * Set `SLOPSMITH_PLUGINS_DIR` to `/config/plugins`. This allows you to simply drop custom plugins directly into the `plugins/` subfolder inside your appdata share. Dependencies will be auto-installed persistently.

### 2. Slopsmith Demucs Server (`slopsmith-demucs-server`)
A standalone companion service that offloads resource-heavy PyTorch/Demucs stem-splitting and Whisper lyrics alignment tasks to a separate CUDA-capable GPU.
* **Registry**: `ghcr.io/slopsmith/slopsmith-demucs-server:latest`
* **Default Port**: `8020`
* **GPU Acceleration Setup**:
  1. Ensure you have the **Unraid NVIDIA Driver** plugin installed from Community Applications.
  2. Toggle **Advanced View** in the top-right corner of the container edit page.
  3. Add the following to the **Extra Parameters** field:
     ```text
     --gpus all
     ```
  4. Save and start.
* **Integration**: In the main Slopsmith Web UI, go to **Settings > Sloppak Converter** and set the **Demucs Server URL** to `http://<your-unraid-ip>:8020`.

---

## How to Install (Manually)

Before your templates are officially indexed in Community Applications, you can add them manually to your Unraid server:

1. Copy the XML files from this repository to your Unraid flash drive:
   * Copy `slopsmith/slopsmith.xml` to `/boot/config/plugins/dockerMan/templates-user/my-slopsmith.xml`
   * Copy `slopsmith-demucs-server/slopsmith-demucs-server.xml` to `/boot/config/plugins/dockerMan/templates-user/my-slopsmith-demucs-server.xml`
2. Go to the **Docker** tab in your Unraid WebUI.
3. Click **Add Container** at the bottom.
4. Select the template dropdown and choose **Slopsmith** or **Slopsmith Demucs Server** to deploy.

---

## License

This repository is licensed under the [MIT License](LICENSE).
