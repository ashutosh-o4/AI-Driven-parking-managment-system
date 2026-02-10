# AI-Driven Parking Management System

> A production-grade, AI-powered parking management solution for large-scale parking facilities, malls, and commercial complexes.

## Overview

The **AI-Driven Parking Management System** is an intelligent solution designed to streamline parking operations through computer vision, natural language processing, and real-time slot allocation. The system automates vehicle detection, ticket issuance, and parking management, enabling seamless experiences for both customers and facility managers.

This repository contains the **core logic and prototype implementation** of the system. The final production deployment will feature a modern web dashboard, enterprise backend, and integrated AI services.

---

## The Problem We Solve

Large parking facilities face critical operational challenges:

- **Manual slot allocation** leading to inefficient space utilization
- **Time-consuming vehicle registration** and ticket issuance processes
- **Lack of real-time visibility** into parking availability across multiple floors
- **Limited accessibility** for management queries without technical expertise
- **No automated detection** of vehicles entering/exiting the facility

This system addresses these problems through intelligent automation and AI-driven insights.

---

## Architecture Overview

### Current Prototype Architecture (Python)

```
┌──────────────────────────────────────────────────────────────────┐
│                        Web Interface (Flask)                      │
│                    HTML, CSS, JavaScript                          │
└──────────────────────────────────────────────────────────────────┘
                              ↓↑
┌──────────────────────────────────────────────────────────────────┐
│                     Flask Backend (Python)                        │
│  ├─ Voice-to-Query Processing (NLP Module)                       │
│  ├─ Parking Slot Management Logic                                │
│  └─ Database Operations                                          │
└──────────────────────────────────────────────────────────────────┘
                              ↓↑
┌──────────────────────────────────────────────────────────────────┐
│               Database (Supabase PostgreSQL)                      │
│  ├─ Users & Vehicles                                             │
│  ├─ Parking Slots & Availability                                 │
│  └─ Parking Logs & Transactions                                  │
└──────────────────────────────────────────────────────────────────┘
```

### Planned Production Architecture

```
┌──────────────────────────────────────────────────────────────────┐
│              Admin Dashboard & Ticket Machines                    │
│            (React/Vue.js, HTML, CSS, JavaScript)                 │
└──────────────────────────────────────────────────────────────────┘
                              ↓↑
┌──────────────────────────────────────────────────────────────────┐
│                   Spring Boot Backend API                         │
│              (Java, REST APIs, Authentication)                    │
│  ├─ Parking Management APIs                                      │
│  ├─ User & Vehicle APIs                                          │
│  └─ Real-time Slot Availability APIs                             │
└──────────────────────────────────────────────────────────────────┘
         ↓↑                    ↓↑                    ↓↑
┌────────────────┐    ┌────────────────┐    ┌────────────────┐
│  MySQL DB      │    │ Python AI      │    │ Cache/Queue    │
│  (Parking Data)│    │ Services       │    │ (Redis)        │
│                │    │ (CV + NLP)     │    │                │
└────────────────┘    └────────────────┘    └────────────────┘
```

---

## Tech Stack

### Current Prototype
| Component | Technology |
|-----------|-----------|
| **Frontend** | HTML5, CSS3, JavaScript (Vanilla) |
| **Backend** | Python 3.8+, Flask 2.3+ |
| **Database** | PostgreSQL (Supabase) |
| **Voice Processing** | SpeechRecognition, gTTS |
| **NLP** | Rule-based pattern matching |
| **Hosting** | Local/Cloud (flexible) |

### Planned Production Stack
| Component | Technology |
|-----------|-----------|
| **Frontend** | React/Vue.js, TypeScript, Tailwind CSS |
| **Backend** | Spring Boot 3.x (Java 17+) |
| **Database** | MySQL 8.0+, Redis for caching |
| **AI Services** | Python (TensorFlow/PyTorch, YOLO for CV) |
| **API Communication** | REST APIs, WebSockets for real-time updates |
| **Authentication** | JWT, OAuth 2.0 |
| **Deployment** | Docker, Kubernetes (optional) |
| **Monitoring** | Prometheus, Grafana, ELK Stack |

---

## Core Features

### Current Implementation (Prototype)
✅ Voice-to-query interface with natural language processing  
✅ Real-time parking slot availability tracking  
✅ Rule-based voice command mapping  
✅ Text-to-speech feedback  
✅ Web interface for slot management  
✅ Basic parking log tracking  
✅ Multi-floor slot organization  

### Planned Features (Production)
- [ ] **Computer Vision Integration**: Automatic license plate recognition (ALPR) and vehicle detection
- [ ] **Dynamic Slot Allocation**: AI-driven assignment based on vehicle type, entry point, and floor occupancy
- [ ] **Automatic Ticket Issuance**: Nearby kiosk integration for parking ticket generation
- [ ] **Real-Time Dashboard**: Live monitoring of all parking floors, slot status, and revenue
- [ ] **Admin Voice Commands**: Hands-free management queries via NLP
- [ ] **Mobile App**: Customer-facing app for ticket management and space booking
- [ ] **Payment Integration**: Automated billing and multiple payment methods
- [ ] **Access Control**: Barrier/gate integration with automated entry/exit
- [ ] **Analytics & Reporting**: Utilization rates, revenue tracking, occupancy trends
- [ ] **Role-Based Access Control**: Admin, operator, and customer roles
- [ ] **Multi-Facility Management**: Support for multiple locations
- [ ] **IoT Integration**: Sensor-based floor availability updates

---

## Database Schema

The system uses a relational model with the following core tables:

```
USERS
├─ user_id (PK, UUID)
├─ name, email, phone
├─ created_at, updated_at

VEHICLES
├─ vehicle_id (PK, UUID)
├─ user_id (FK → USERS)
├─ vehicle_number, vehicle_type
├─ created_at, updated_at

PARKING_SLOTS
├─ slot_id (PK, Serial)
├─ floor_number, slot_number
├─ slot_type (standard, compact, accessible)
├─ status (available, occupied, maintenance)
├─ hourly_rate
├─ created_at, updated_at

PARKING_LOGS
├─ log_id (PK, UUID)
├─ vehicle_id (FK → VEHICLES)
├─ slot_id (FK → PARKING_SLOTS)
├─ entry_time, exit_time
├─ total_amount, payment_status
├─ created_at

Views:
├─ available_slots_view → Real-time available slots
└─ current_parking_status → Active occupancy details
```

---

## Quick Start (Prototype)

### Prerequisites
- Python 3.8+
- Git
- Modern web browser with microphone support
- Supabase account (free tier available)

### Installation & Setup

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd AI-Parking-Management-System
   ```

2. **Set up Python environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```
   
   *Note: PyAudio may require additional setup on Windows. See [Troubleshooting](#troubleshooting) below.*

4. **Configure Supabase**
   - Create a project at [supabase.com](https://supabase.com)
   - Copy your Project URL and API Key
   - Create a `.env` file:
     ```env
     SUPABASE_URL=https://your-project.supabase.co
     SUPABASE_KEY=your-anon-key
     FLASK_ENV=development
     FLASK_DEBUG=True
     ```

5. **Initialize database**
   - In Supabase SQL Editor, run the schema from `supabase_schema.sql`

6. **Run the application**
   ```bash
   python app.py
   ```
   
   Access the interface at `http://localhost:5000`

### Voice Commands (Prototype)

**Slot Management**
- "Show available slots"
- "Book slot 3"
- "Release slot 5"
- "Status of slot 2"

**Data Queries**
- "Show all vehicles"
- "Show users"
- "Show parking logs"

---

## Project Roadmap

### Phase 1: Core Prototype (Current)
- [x] Voice-to-query functionality
- [x] Slot management backend
- [x] Web interface
- [ ] Comprehensive testing & documentation

### Phase 2: Enhanced Prototype
- [ ] Computer vision integration (vehicle detection)
- [ ] Improved NLP with machine learning
- [ ] Mobile web interface
- [ ] Payment gateway integration

### Phase 3: Enterprise Backend
- [ ] Spring Boot API development
- [ ] MySQL database migration
- [ ] JWT authentication & authorization
- [ ] Real-time WebSocket updates
- [ ] API documentation (Swagger/OpenAPI)

### Phase 4: Full Integration
- [ ] React/Vue.js admin dashboard
- [ ] Customer mobile app
- [ ] IoT sensor integration
- [ ] Multi-facility support
- [ ] Production deployment

### Phase 5: Advanced Features
- [ ] AI-driven pricing optimization
- [ ] Predictive analytics
- [ ] Advanced access control
- [ ] Integration with city parking systems

---

## Project Structure

```
AI-Parking-Management-System/
├── app.py                      # Flask main application
├── config.py                   # Configuration management
├── nlp_module.py              # NLP & voice command processing
├── voice_module.py            # Voice recognition wrapper
├── supabase_module.py         # Database operations
├── requirements.txt           # Python dependencies
├── supabase_schema.sql        # Database schema
├── .env                       # Configuration (DO NOT commit)
├── templates/
│   ├── index.html            # Web interface
│   └── dashboard.html        # Admin dashboard
├── static/
│   └── style.css             # Styling
└── README.md                 # This file
```

---

## Troubleshooting

### Issue: PyAudio Installation Fails
**Solution**: On Windows, use `pipwin`:
```bash
pip install pipwin
pipwin install pyaudio
```

On macOS:
```bash
brew install portaudio
pip install pyaudio
```

### Issue: Microphone Not Detected
- Check browser microphone permissions
- Verify microphone is working in system settings
- Restart the application

### Issue: Voice Recognition Not Working
- Ensure internet connection (Google Speech Recognition API is used)
- Speak clearly and at normal volume
- Check console logs for API errors

### Issue: Database Connection Failed
- Verify `SUPABASE_URL` and `SUPABASE_KEY` in `.env`
- Ensure your Supabase project is active
- Check network connectivity to Supabase

---

## Configuration

### Environment Variables

```env
# Supabase
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_KEY=your-anon-key

# Flask
FLASK_ENV=development
FLASK_DEBUG=True
FLASK_HOST=0.0.0.0
FLASK_PORT=5000
SECRET_KEY=your-secret-key

# Voice Settings
VOICE_TIMEOUT=5
VOICE_PHRASE_LIMIT=10
VOICE_LANGUAGE=en-US

# Logging
LOG_LEVEL=INFO
LOG_FILE=app.log
```

---

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -am 'Add feature'`
4. Push to the branch: `git push origin feature/your-feature`
5. Submit a pull request

---

## Security Considerations

- **Never commit `.env` files** to version control
- Use **Supabase Row-Level Security (RLS)** for production
- Implement **HTTPS** in production deployments
- Validate all user inputs on both frontend and backend
- Use **JWT tokens** for API authentication in production
- Regularly update dependencies for security patches

---

## Performance Optimization

- Database queries are indexed for common access patterns
- Connection pooling is handled automatically by Supabase/Spring Boot
- Voice processing timeouts are configurable
- Consider Redis caching for frequently accessed data
- Implement pagination for large datasets in production

---

## Disclaimer

⚠️ **This project is currently under active development.** While the core logic and prototype are functional, the system is not yet production-ready. Features and APIs are subject to change.

- Current implementation is a **proof-of-concept** built in Python
- Database uses Supabase (can be migrated to MySQL)
- Production deployment will use Spring Boot + MySQL
- Some features are planned and not yet implemented

Suitable for **demonstration, learning, and prototype validation** purposes.

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## Support & Contact

For questions, suggestions, or issues:
- Check the [Troubleshooting](#troubleshooting) section
- Review relevant documentation (Flask, SpeechRecognition, Supabase)
- Create an issue in the repository

---

## Acknowledgments

- **Flask**: [Flask Documentation](https://flask.palletsprojects.com/)
- **Supabase**: [Supabase Docs](https://supabase.com/docs)
- **Speech Recognition**: [SpeechRecognition Library](https://github.com/Uberi/speech_recognition)
- **Text-to-Speech**: [gTTS Documentation](https://gtts.readthedocs.io/)

---

**Last Updated**: February 2026  
**Status**: Under Active Development 🚀
