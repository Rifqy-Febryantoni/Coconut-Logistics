# Cesium Logistic Platform

Platform Peta Digital 3D (berbasis Cesium) untuk memvisualisasikan rantai pasok kelapa di Indonesia guna menekan biaya logistik.

## Arsitektur & Teknologi

*   **Frontend**: Node.js
*   **Backend**: Golang
*   **Database**: PostgreSQL + PostGIS (Optimasi data spasial)
*   **Cache**: Redis

## Cara Menjalankan Project Secara Lokal

### Prasyarat

*   [Docker](https://www.docker.com/products/docker-desktop) and [Docker Compose](https://docs.docker.com/compose/install/)

### Instalasi

1.  **Clone repositori ini:**
    ```bash
    git clone https://github.com/Rifqy-Febryantoni/Coconut-Logistics.git
    cd Coconut-Logistics
    ```

2.  **Gandakan file env:**
    ```bash
    cp .env.example .env
    ```

3.  **Buka file `.env` dan isi dengan konfigurasi rahasia (password lokal, API keys).** Jangan pernah commit file `.env`!

4.  **Jalankan container (Database, Cache, Backend, Frontend):**
    ```bash
    docker-compose up -d --build
    ```

    Database PostGIS siap di port 5432, Redis di port 6379, App Golang di port 8080, dan Frontend Node.js di port 3000.

## Standar Operasional (Workflow & Keamanan)

*   **Manajemen Rahasia (Secrets):** Password database, API Key **haram** dimasukkan ke Git. Data asli hanya disimpan di dalam file `.env`.
*   **Aturan Branching Git:**
    *   `main`: Lingkungan *Production* (Suci, tidak boleh di-*push* langsung).
    *   `staging`: Lingkungan *Testing/QA*.
    *   `feature/...`: Cabang tempat *developer* bekerja.
*   **Pull Request (PR):**
    Dilarang *push* langsung ke `main` atau `staging`. Setiap *developer* wajib membuat *branch* baru dengan format `feature/nama-fitur` lalu membuat Pull Request ke `staging` dan melewati pengecekan (*Code Review*) sebelum kodenya digabungkan. Pipeline CI/CD akan berjalan otomatis saat PR dibuat.