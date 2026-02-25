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
    *   `staging`: Lingkungan *Testing/QA*. Tempat berkumpulnya semua fitur baru sebelum rilis.
    *   `feature/...` atau `fix/...`: Cabang tempat *developer* bekerja.
*   **Workflow Developer (Cara Berkontribusi):**
    1. Pastikan Anda berada di branch `staging` terbaru:
       ```bash
       git checkout staging
       git pull origin staging
       ```
    2. Buat branch baru dari `staging` sesuai fitur yang dikerjakan:
       ```bash
       git checkout -b feature/nama-fitur-anda
       ```
    3. Lakukan *commit* dan *push* hasil kerja Anda ke remote branch:
       ```bash
       git push origin feature/nama-fitur-anda
       ```
    4. Buka GitHub, buat **Pull Request (PR)** dari branch Anda menuju `staging`.
    5. Tunggu proses *Code Review* dan pastikan semua tes CI/CD (GitHub Actions) lolos (*Passed*).
    6. Jika sudah disetujui, gabungkan (Merge) PR tersebut ke `staging`.