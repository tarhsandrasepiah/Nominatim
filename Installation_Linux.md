#  Installing Nominatim from Source on Ubuntu

This guide walks you through the installation and usage of [Nominatim](https://github.com/osm-search/Nominatim) on an Ubuntu system, starting from scratch. It's ideal for developers or enthusiasts who want to run their own geocoding server using OpenStreetMap data.

---

##  Prerequisites

Ensure your system is up-to-date and that you have `git`, `Python3`, and `PostgreSQL` installed.

```bash
sudo apt update
sudo apt install git python3-venv python3-pip postgresql postgresql-contrib build-essential
```

---

##  Step-by-Step Installation

### 1. Create Project Directory

```bash
mkdir nominatim
cd nominatim
```

### 2. Install Virtualenv

```bash
sudo apt install virtualenv
```

### 3. Clone the Nominatim Repository

```bash
git clone https://github.com/osm-search/Nominatim.git
```

### 4. Create and Activate a Virtual Environment

```bash
virtualenv ~/nominatim-venv
```

### 5. Install Nominatim API and Database Packages

```bash
cd Nominatim
~/nominatim-venv/bin/pip install ./packaging/nominatim-{db,api}
```

### 6. Install Required Web Server Dependencies

```bash
~/nominatim-venv/bin/pip install uvicorn falcon
```

---

## Import OSM Data

Download a `.osm.pbf` file from [Geofabrik](https://download.geofabrik.de/) (e.g., for Colombia):

```bash
nominatim import --osm-file colombia-latest.osm.pbf
```

**Important:** If you've previously run the import and want to restart, you may need to drop the old database:

```bash
sudo -u postgres dropdb nominatim
```

---

##  Test a Query

Try searching for a place:

```bash
nominatim search --query Berlin
```

---

##  Start the API Server

Start the web server to serve API requests:

```bash
nominatim serve
```

This will launch the service on `http://localhost:8000`.

---

##  Done!

You're now running Nominatim on your local machine. From here, you can:
- Query using the API
- Explore reverse geocoding
- Build on top of the Nominatim search infrastructure

---

##  Resources

- Official Docs: [https://nominatim.org](https://nominatim.org)
- GitHub Issues: [https://github.com/osm-search/Nominatim/issues](https://github.com/osm-search/Nominatim/issues)
- OSM Community: [https://community.openstreetmap.org](https://community.openstreetmap.org)

---
