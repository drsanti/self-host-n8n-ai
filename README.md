# Self-Hosted N8N with AI

A Docker Compose setup for running N8N (workflow automation) with AI capabilities using Ollama, backed by PostgreSQL.

## Features

- **N8N**: Latest version with workflow automation capabilities
- **PostgreSQL**: Database backend for N8N data persistence
- **Ollama**: Local AI model server supporting multiple GPU configurations
- **Pre-configured workflows**: Demo data and credentials included

## Quick Start

1. **Clone and setup environment**:
   ```bash
   git clone https://github.com/drsanti/self-host-n8n-ai.git
   cd self-host-n8n-ai
   cp .env.example .env
   ```

2. **Configure environment variables**:
   Edit `.env` file with your settings:
   ```
   POSTGRES_USER=your_postgres_user
   POSTGRES_PASSWORD=your_secure_password
   POSTGRES_DB=n8n
   N8N_ENCRYPTION_KEY=your_encryption_key
   N8N_USER_MANAGEMENT_JWT_SECRET=your_jwt_secret
   ```

3. **Start the services**:

   **CPU-only setup**:
   ```bash
   docker-compose --profile cpu up -d
   ```

   **NVIDIA GPU setup**:
   ```bash
   docker-compose --profile gpu-nvidia up -d
   ```

   **AMD GPU setup**:
   ```bash
   docker-compose --profile gpu-amd up -d
   ```

## Services

### Core Services
- **N8N**: Available at http://localhost:5678
- **PostgreSQL**: Available at localhost:5432
- **Ollama**: Available at http://localhost:11434

### AI Models
The setup automatically pulls the `mistral:latest` model for AI workflows.

## Configuration

### Profiles
- `cpu`: CPU-only Ollama setup
- `gpu-nvidia`: NVIDIA GPU acceleration
- `gpu-amd`: AMD GPU acceleration with ROCm

### Volumes
- `n8n_storage`: N8N workflow and configuration data
- `postgres_storage`: PostgreSQL database files
- `ollama_storage`: AI model storage

## Usage

1. Access N8N at http://localhost:5678
2. Create your first workflow or import demo workflows from `./n8n/demo-data/`
3. Use Ollama nodes in N8N to interact with AI models
4. Models are automatically downloaded on first startup

## File Structure

```
.
├── docker-compose.yml    # Main service configuration
├── .env                  # Environment variables (create from .env.example)
├── n8n/
│   └── demo-data/       # Sample workflows and credentials
└── shared/              # Shared data directory
```

## Troubleshooting

### GPU Issues
- Ensure Docker has GPU support enabled
- For NVIDIA: Install nvidia-docker2
- For AMD: Ensure ROCm drivers are installed

### Port Conflicts
If ports are already in use, modify the port mappings in `docker-compose.yml`:
- N8N: `5678:5678`
- PostgreSQL: `5432:5432`
- Ollama: `11434:11434`

### Storage Issues
Check volume permissions and ensure Docker has access to the storage directories.

## Development

To modify workflows or add new demo data:
1. Edit files in `./n8n/demo-data/`
2. Restart the `n8n-import` service: `docker-compose restart n8n-import`

## License

This project is provided as-is for educational and development purposes.

---

# Self-Hosted N8N with AI (ภาษาไทย)

การตั้งค่า Docker Compose สำหรับรัน N8N (ระบบอัตโนมัติของเวิร์กโฟลว์) พร้อมความสามารถ AI โดยใช้ Ollama และ PostgreSQL

## คุณสมบัติ

- **N8N**: เวอร์ชันล่าสุดพร้อมความสามารถในการสร้างเวิร์กโฟลว์อัตโนมัติ
- **PostgreSQL**: ฐานข้อมูลสำหรับจัดเก็บข้อมูลของ N8N
- **Ollama**: เซิร์ฟเวอร์โมเดล AI ในเครื่อง รองรับการตั้งค่า GPU หลายแบบ
- **เวิร์กโฟลว์ที่กำหนดไว้ล่วงหน้า**: ข้อมูลตัวอย่างและข้อมูลประจำตัวรวมอยู่ด้วย

## เริ่มต้นอย่างรวดเร็ว

1. **Clone และตั้งค่าสภาพแวดล้อม**:
   ```bash
   git clone https://github.com/drsanti/self-host-n8n-ai.git
   cd self-host-n8n-ai
   cp .env.example .env
   ```

2. **กำหนดค่าตัวแปรสภาพแวดล้อม**:
   แก้ไขไฟล์ `.env` ด้วยการตั้งค่าของคุณ:
   ```
   POSTGRES_USER=your_postgres_user
   POSTGRES_PASSWORD=your_secure_password
   POSTGRES_DB=n8n
   N8N_ENCRYPTION_KEY=your_encryption_key
   N8N_USER_MANAGEMENT_JWT_SECRET=your_jwt_secret
   ```

3. **เริ่มต้นเซอร์วิส**:

   **การตั้งค่าแบบ CPU เท่านั้น**:
   ```bash
   docker-compose --profile cpu up -d
   ```

   **การตั้งค่าแบบ NVIDIA GPU**:
   ```bash
   docker-compose --profile gpu-nvidia up -d
   ```

   **การตั้งค่าแบบ AMD GPU**:
   ```bash
   docker-compose --profile gpu-amd up -d
   ```

## เซอร์วิส

### เซอร์วิสหลัก
- **N8N**: เข้าถึงได้ที่ http://localhost:5678
- **PostgreSQL**: เข้าถึงได้ที่ localhost:5432
- **Ollama**: เข้าถึงได้ที่ http://localhost:11434

### โมเดล AI
ระบบจะดึงโมเดล `mistral:latest` อัตโนมัติสำหรับเวิร์กโฟลว์ AI

## การกำหนดค่า

### โปรไฟล์
- `cpu`: การตั้งค่า Ollama แบบ CPU เท่านั้น
- `gpu-nvidia`: การเร่งความเร็วด้วย NVIDIA GPU
- `gpu-amd`: การเร่งความเร็วด้วย AMD GPU พร้อม ROCm

### โวลุ่ม
- `n8n_storage`: ข้อมูลเวิร์กโฟลว์และการกำหนดค่าของ N8N
- `postgres_storage`: ไฟล์ฐานข้อมูล PostgreSQL
- `ollama_storage`: การจัดเก็บโมเดล AI

## การใช้งาน

1. เข้าถึง N8N ที่ http://localhost:5678
2. สร้างเวิร์กโฟลว์แรกของคุณหรือนำเข้าเวิร์กโฟลว์ตัวอย่างจาก `./n8n/demo-data/`
3. ใช้โหนด Ollama ใน N8N เพื่อโต้ตอบกับโมเดล AI
4. โมเดลจะถูกดาวน์โหลดอัตโนมัติเมื่อเริ่มต้นครั้งแรก

## โครงสร้างไฟล์

```
.
├── docker-compose.yml    # การกำหนดค่าเซอร์วิสหลัก
├── .env                  # ตัวแปรสภาพแวดล้อม (สร้างจาก .env.example)
├── n8n/
│   └── demo-data/       # ตัวอย่างเวิร์กโฟลว์และข้อมูลประจำตัว
└── shared/              # ไดเรกทอรีข้อมูลที่ใช้ร่วมกัน
```

## การแก้ไขปัญหา

### ปัญหา GPU
- ตรวจสอบให้แน่ใจว่า Docker รองรับ GPU
- สำหรับ NVIDIA: ติดตั้ง nvidia-docker2
- สำหรับ AMD: ตรวจสอบให้แน่ใจว่าได้ติดตั้ง ROCm drivers แล้ว

### ความขัดแย้งของพอร์ต
หากพอร์ตถูกใช้งานอยู่แล้ว ให้แก้ไขการแมปพอร์ตใน `docker-compose.yml`:
- N8N: `5678:5678`
- PostgreSQL: `5432:5432`
- Ollama: `11434:11434`

### ปัญหาการจัดเก็บ
ตรวจสอบสิทธิ์โวลุ่มและตรวจสอบให้แน่ใจว่า Docker มีสิทธิ์เข้าถึงไดเรกทอรีการจัดเก็บ

## การพัฒนา

เพื่อแก้ไขเวิร์กโฟลว์หรือเพิ่มข้อมูลตัวอย่างใหม่:
1. แก้ไขไฟล์ใน `./n8n/demo-data/`
2. รีสตาร์ทเซอร์วิส `n8n-import`: `docker-compose restart n8n-import`

## ใบอนุญาต

โปรเจ็กต์นี้จัดทำขึ้นเพื่อการศึกษาและพัฒนาตามที่ให้ไว้
