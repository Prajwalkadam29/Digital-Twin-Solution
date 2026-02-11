# Byte-Astra: Industrial Lathe Digital Twin & Predictive Maintenance System

A comprehensive Flask-based web application that provides real-time monitoring, predictive maintenance, and digital twin simulation capabilities for industrial CNC lathe machines. The system integrates machine learning models to predict tool failures, generates synthetic sensor data, and provides role-based dashboards for operators and managers.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [Database Setup](#database-setup)
- [API Documentation](#api-documentation)
- [User Roles](#user-roles)
- [Testing](#testing)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)

---

## Overview

Byte-Astra is a digital twin platform designed for industrial machine monitoring and predictive maintenance. It enables:

- **Real-time monitoring** of multiple CNC lathe machines
- **Sensor data simulation** for testing and development
- **ML-based failure prediction** using historical sensor data
- **Alert generation** based on anomaly detection
- **Role-based access control** for operators and managers
- **Analytics dashboards** for performance tracking
- **Job management** and tool tracking

The system uses MongoDB for data persistence and Flask for the web interface, supporting both single and multiple machine operations.

---

## Features

### Core Features

1. **Digital Twin Simulator**
   - Generate realistic sensor data based on material properties
   - Support for multiple materials (Steel, Aluminum, Wood)
   - Support for various machining operations (turning, facing, threading, drilling, boring, knurling)
   - Tool wear simulation
   - Realistic thermal and mechanical stress modeling

2. **Predictive Maintenance**
   - Machine learning models for tool failure prediction
   - Real-time anomaly detection
   - Risk scoring based on sensor readings
   - Proactive alert generation

3. **Monitoring & Analytics**
   - Real-time sensor data visualization
   - Historical data analysis
   - Performance metrics and KPIs
   - Machine health dashboards

4. **Alert Management**
   - Automated alert generation
   - Alert categorization by severity
   - Alert acknowledgment and resolution tracking
   - Custom alert thresholds

5. **Job Management**
   - Job creation and tracking
   - Tool assignment and management
   - Material and operation type specification
   - Job status monitoring

6. **Authentication & Authorization**
   - Secure login system with password hashing
   - Role-based access control (Manager/Operator)
   - Session management with last login tracking

---

## Project Structure

```
Byte-Astra/
├── app/
│   ├── __init__.py              # Flask app initialization
│   ├── models.py                # MongoDB models and user management
│   ├── routes.py                # Application routes and endpoints
│   ├── forms.py                 # WTForms form definitions
│   ├── simulator.py             # ML model and sensor data generation
│   ├── static/                  # CSS stylesheets
│   │   ├── dashboard.css
│   │   ├── lathe.css
│   │   ├── simulator_form.css
│   │   └── styles.css
│   └── templates/               # HTML templates
│       ├── base.html            # Base template
│       ├── login.html
│       ├── dashboard.html
│       ├── manager_landing.html
│       ├── analytics_dashboard.html
│       ├── jobs.html
│       ├── alerts.html
│       ├── status.html
│       ├── lathe_detail.html
│       ├── simulator_form.html
│       ├── simulator.html
│       ├── alert_form.html
│       └── navbar.html
├── Digital Twin/                # Digital twin documentation
├── Pradnyastra - Unity/         # Unity-based visualization (optional)
├── run.py                       # Application entry point
├── config.py                    # Configuration settings
├── requirements.txt             # Python dependencies
├── .env                         # Environment variables (create locally)
├── create_test_users.py         # Test user setup script
├── test_simulator.py            # Test data generation script
├── analyze_test_data.py         # Data analysis utilities
└── README.md                    # This file
```

---

## Prerequisites

- **Python**: 3.8 or higher
- **MongoDB**: 4.4 or higher (local or cloud instance)
- **pip**: Python package manager
- **Git**: For version control (optional)

### System Requirements

- **RAM**: 4GB minimum (8GB recommended)
- **Disk Space**: 2GB minimum
- **OS**: Windows, macOS, or Linux

---

## Installation

### Step 1: Clone the Repository

```bash
git clone <repository-url>
cd Byte-Astra--main
```

### Step 2: Create a Virtual Environment

```bash
# Windows
python -m venv .venv
.venv\Scripts\activate

# macOS/Linux
python3 -m venv .venv
source .venv/bin/activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

The main dependencies include:

- **Flask**: Web framework
- **flask-cors**: Cross-Origin Resource Sharing
- **flask-socketio**: WebSocket support
- **pymongo**: MongoDB driver
- **flask-wtf**: Form handling
- **scikit-learn**: Machine learning
- **numpy/pandas**: Data processing
- **gevent/eventlet**: Async support

---

## Configuration

### Step 1: Set Up Environment Variables

Create a `.env` file in the project root directory:

```bash
# .env
SECRET_KEY=your_secure_secret_key_here
MONGO_URI=mongodb://localhost:27017/
ML_MODEL_PATH=model.pkl
```

### Configuration Details

| Variable             | Description                               | Default                      |
| -------------------- | ----------------------------------------- | ---------------------------- |
| `SECRET_KEY`         | Flask session secret key                  | `default-secret-key`         |
| `MONGO_URI`          | MongoDB connection string                 | `mongodb://localhost:27017/` |
| `ML_MODEL_PATH`      | Path to trained ML model                  | `model.pkl`                  |
| `SENSOR_INTERVAL`    | Sensor data collection interval (seconds) | `5`                          |
| `SIMULATION_TIMEOUT` | Max simulation runtime (seconds)          | `300`                        |

### MongoDB Connection Examples

**Local MongoDB:**

```
mongodb://localhost:27017/
```

**MongoDB Atlas (Cloud):**

```
mongodb+srv://username:password@cluster.mongodb.net/?appName=Cluster0
```

---

## Running the Application

### Start MongoDB

**Using Docker:**

```bash
docker run -d -p 27017:27017 --name mongodb mongo:latest
```

**Using Local MongoDB:**

```bash
# Windows
mongod

# macOS/Linux
mongod --dbpath /path/to/data
```

### Step 1: Activate Virtual Environment

```bash
# Windows
.venv\Scripts\activate

# macOS/Linux
source .venv/bin/activate
```

### Step 2: Run the Application

```bash
python run.py
```

The application will start at `http://localhost:5000`

### Output

```
 * Serving Flask app 'app'
 * Debug mode: on
 * Running on http://127.0.0.1:5000
 * Press CTRL+C to quit
```

### Access the Application

Open your web browser and navigate to:

```
http://localhost:5000
```

You will be redirected to the login page.

---

## Database Setup

### Create Test Users

Run the user creation script to populate the database with test users:

```bash
python create_test_users.py
```

**Test User Credentials:**

| User ID | Password | Role     | Employee ID |
| ------- | -------- | -------- | ----------- |
| Sahil   | man123   | Manager  | EMP001      |
| Rohit   | man123   | Manager  | EMP002      |
| Yash    | op123    | Operator | EMP003      |
| Raj     | op123    | Operator | EMP004      |
| Jay     | op123    | Operator | EMP005      |

### Generate Test Data

Generate synthetic sensor data for testing:

```bash
python test_simulator.py
```

This script:

- Creates random jobs for 10 simulations
- Generates realistic sensor data
- Populates test databases
- Outputs verification statistics

### Expected Output

```
Generating test data with 10 simulations...
Test data generation complete!

=== Verification ===
Collections: ['SensoryData', 'JobDetails']
SensoryData count: 5000+
JobDetails count: 10
```

---

## Database Structure

### MongoDB Collections

#### Authentication Database: `AuthDB`

**Collection: `users`**

```javascript
{
  "_id": ObjectId,
  "employeeId": "EMP001",
  "userID": "Sahil",
  "passwordHash": "hashed_password",
  "userType": "manager",
  "lastLogin": ISODate("2026-02-12T10:00:00.000Z")
}
```

#### Jobs Database: `Jobs`

**Collections:** `lathe{N}_job_detail` (N = 1 to 20)

```javascript
{
  "JobID": "JOB_20260212_001",
  "JobType": "turning",
  "Material": "Mild Steel",
  "ToolNo": 5,
  "StartTime": ISODate("2026-02-12T10:00:00.000Z"),
  "EstimatedTime": 30,
  "Status": "In Progress"
}
```

#### Sensor Data Database: `SensorData`

**Collections:** `lathe{N}_sensory_data` (N = 1 to 20)

```javascript
{
  "timestamp": ISODate("2026-02-12T10:00:05.000Z"),
  "rpm": 1200,
  "temperature": 45.5,
  "torque": 22.3,
  "vibration": 0.8,
  "power": 150.2,
  "tool_wear": 0.15,
  "failure_probability": 0.05
}
```

#### Alerts Database: `Alerts`

**Collections:** `lathe{N}_alerts` (N = 1 to 20)

```javascript
{
  "_id": ObjectId,
  "lathe_id": "lathe-1",
  "job_id": "JOB_20260212_001",
  "alert_type": "HIGH_TEMPERATURE",
  "severity": "critical",
  "value": 85.5,
  "threshold": 80,
  "timestamp": ISODate("2026-02-12T10:00:05.000Z"),
  "resolved": false
}
```

---

## API Documentation

### Authentication Endpoints

#### Login

```
POST /login
Content-Type: application/x-www-form-urlencoded

userID=Sahil&password=man123
```

**Response:** Redirects to manager/operator dashboard on success

#### Logout

```
GET /logout
```

**Response:** Redirects to login page

### Dashboard Endpoints

#### Manager Dashboard

```
GET /manager
Authentication: Required (Manager role)
```

#### Operator Dashboard

```
GET /dashboard
Authentication: Required (Operator role)
```

#### Analytics

```
GET /analytics
Authentication: Required (Manager role)
```

### Job Management

#### View Jobs

```
GET /jobs/<lathe_id>
Authentication: Required
```

#### Create Job

```
POST /jobs/create
Content-Type: application/x-www-form-urlencoded
Authentication: Required (Operator role)
```

### Simulator Endpoints

#### Start Simulation

```
POST /simulator/start
Content-Type: application/json
Authentication: Required (Operator role)

{
  "lathe_id": "lathe-1",
  "material": "Mild Steel",
  "job_type": "turning",
  "tool_no": 5,
  "duration": 60
}
```

#### Get Sensor Data

```
GET /api/sensor-data/<lathe_id>
Authentication: Required
```

### Debug Endpoints

#### MongoDB Connection Test

```
GET /debug/mongodb
Authentication: Required
```

---

## User Roles

### Manager

- Access to analytics dashboards
- View all machine metrics across the facility
- Generate performance reports
- Monitor system health
- Access to manager landing page

### Operator

- Operate individual machines
- Create and manage jobs
- View real-time sensor data
- Receive and acknowledge alerts
- Access to operator dashboard

---

## Testing

### Run Test Simulator

Generate and verify test data:

```bash
python test_simulator.py
```

### Analyze Test Data

Analyze the generated test data:

```bash
python analyze_test_data.py
```

### Manual Testing

1. **Test Login:**
   - Navigate to http://localhost:5000/login
   - Try manager credentials (Sahil/man123)
   - Try operator credentials (Yash/op123)

2. **Test Simulator:**
   - Create a new job through the job form
   - Start a simulation
   - Monitor real-time sensor data

3. **Test Alerts:**
   - Trigger a high-stress simulation
   - Verify alerts are generated correctly
   - Check alert acknowledgment functionality

---

## Troubleshooting

### Issue: MongoDB Connection Failed

**Solution:**

1. Ensure MongoDB is running:
   ```bash
   # Check MongoDB status
   mongosh  # or mongo for older versions
   ```
2. Verify `MONGO_URI` in `.env` file
3. Check MongoDB port (default: 27017)

### Issue: Port 5000 Already in Use

**Solution:**

```bash
# Change Flask port
export FLASK_ENV=development
python run.py
# Or specify port
flask run --port 5001
```

### Issue: Missing Dependencies

**Solution:**

```bash
# Reinstall all dependencies
pip install --upgrade pip
pip install -r requirements.txt
```

### Issue: ML Model Not Found

**Solution:**
The application will work without a pre-trained model but will use random failure probability. To use predictions:

1. Train an ML model using your data
2. Save it as `model.pkl`
3. Place it in the project root or specify path in `.env`

### Issue: Virtual Environment Not Activating

**Solution:**

```bash
# Windows - Ensure execution policy allows scripts
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser

# Then try activating again
.venv\Scripts\activate
```

---

## Performance Optimization

### For Production Deployment

1. **Disable Debug Mode:**

   ```python
   # run.py
   app.run(debug=False)
   ```

2. **Use Production Server (Gunicorn):**

   ```bash
   gunicorn --workers 4 --bind 0.0.0.0:5000 run:app
   ```

3. **Database Indexing:**
   - Create indexes on frequently queried fields
   - Use MongoDB Atlas for cloud deployment

4. **Caching:**
   - Implement Redis for session caching
   - Cache analytics results

---

## Contributing

### Development Workflow

1. Create a feature branch
2. Make changes and test locally
3. Ensure all tests pass
4. Submit pull request with description

### Code Style

- Follow PEP 8 Python style guide
- Use meaningful variable names
- Add docstrings for functions
- Comment complex logic

---

## License

[Add your license information here]

---

## Support & Documentation

For additional help:

- Check the [Digital Twin documentation](./Digital%20Twin/readme.md)
- Review inline code comments
- Consult the API endpoints section

---

## Version History

### v1.0.0 (Current)

- Initial release
- Core simulator functionality
- ML-based failure prediction
- Multi-machine monitoring
- Role-based access control

---

## Acknowledgments

Built as an industrial IoT solution for predictive maintenance and digital twin simulation of CNC lathe machines.
