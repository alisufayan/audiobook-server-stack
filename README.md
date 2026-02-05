# audiobook-server-stack
A lightweight Docker Compose stack for self-hosted audiobook downloading and streaming. Perfect for Raspberry Pi or any Linux server.

## Services

| Service | Description | URL |
|---------|-------------|-----|
| **qBittorrent** | Torrent client | http://localhost:8080 |
| **AudiobookShelf** | Audiobook server | http://localhost:13378 |

## Quick Start

```bash
# 1. Create download directory (data/ is auto-created by Docker)
sudo mkdir -p /srv/torrents/complete/audiobooks
sudo chown -R $(id -u):$(id -g) /srv/torrents

# 2. Start services
docker compose up -d

# 3. Get qBittorrent temporary password (randomly generated on first run)
docker logs qbittorrent | grep "password"

# 4. Configure
# - qBittorrent: http://localhost:8080
#   Login: admin / <temp password from logs>
#   Then change password in Settings → Web UI
#   Set download path to: /downloads/complete/audiobooks
# - AudiobookShelf: http://localhost:13378
#   Create library with folder: /torrents-complete-audiobooks
```

## Usage

1. **Download audiobooks:**
   - Open qBittorrent Web UI: http://localhost:8080
   - Paste magnet links or upload .torrent files
   - Files download to `/srv/torrents/complete/audiobooks` (host path)

2. **Library setup in AudiobookShelf:**
   - Open http://localhost:13378
   - Create new library
   - **Folder path:** `/torrents-complete-audiobooks` (container path)
   - AudiobookShelf auto-detects downloaded books

3. Listen via web UI or mobile apps

### Mobile Apps

**iOS (Recommended): BookPlayer**
- Connect to your AudiobookShelf server
- Stream or download audiobooks for offline listening
- Auto-syncs progress across devices

**Android**: Official AudiobookShelf app from GitHub releases

## Directory Structure

```
/srv/torrents/complete/audiobooks  # Downloads (host)
./data/qbittorrent/config          # qBittorrent config
./data/audiobookshelf/             # AudiobookShelf data
```

