# Ace Stream on macOS

A lightweight, containerized solution to run Ace Stream on macOS using Docker, with network playback support for media players like IINA and VLC.

## Prerequisites

- Docker Desktop for Mac installed and running.
- A media player that supports network streams:
  - [IINA](https://iina.io/) (Highly recommended for macOS)
  - [VLC Media Player](https://www.videolan.org/vlc/)

## Installation & Setup

### 1. Create the Docker Compose file

Create a file named `docker-compose.yml` in your working directory and add the following configuration:

```yaml
services:
  acelink:
    image: blaiseio/acelink
    platform: linux/amd64
    ports:
      - "6878:6878"
    restart: unless-stopped
```

### 2. Start the Ace Stream container
Open your terminal, navigate to the directory containing your docker-compose.yml, and run the following command to start the container in the background:

```bash
docker compose up -d
```

## How to Play Streams
Once the Docker container is up and running, you can stream content by passing your Ace Stream ID or Infohash to your local Ace Stream server.

### 1. Construct the Stream URL
Replace `<INSERT_ACESTREAM_ID_HERE>` with your actual stream ID using this format:
```text
http://localhost:6878/ace/getstream?id=<INSERT_ACESTREAM_ID_HERE>
```
**Fallback Method**:  If the standard id parameter does not work, use the infohash parameter instead:
```text
http://localhost:6878/ace/getstream?infohash=<INSERT_ACESTREAM_ID_HERE>
```
Examples:
- `http://localhost:6878/ace/getstream?id=4b7c5f21b435d79c823e47572655a9c157a3ba12`
- `http://localhost:6878/ace/getstream?infohash=37796ca47026bc190c7dc26827c0dfb6b61d137b`

### 2. Open in your Media Player
Copy your constructed URL and open it in your preferred player:
- **For IINA:** Go to the menu bar and select **File > Open URL…** (or press `Cmd + Shift + O`), paste the link, and click open. paste the link, and click open.
- **For VLC:** Go to the menu bar and select **File > Open Network…** (or press `Cmd + N`), paste the link, and click open.