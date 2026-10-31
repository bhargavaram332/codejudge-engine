# CodeJudge Engine (CodeJudge Lite with Mobile Companion)

**CodeJudge Engine** is a lightweight automated code evaluation platform designed for instructors and students in programming courses. It enables instructors to automate grading while providing students with rapid, consistent feedback on their Python submissions. The system includes a responsive web application and an extended mobile companion app for real-time status tracking.

---

## 🚀 Product Core Promises & Workflow
* **Automated Feedback:** Students submit a Python function and instantly see whether it passes hidden test cases.
* **Hidden Test Confidentiality:** Students never see hidden inputs or expected outputs—only pass counts and final verdicts. Instructors maintain full visibility into all submission details.
* **Multi-Platform Support:** Full-featured desktop/laptop web experience complemented by a read-only real-time mobile tracking app.

---

## 🛠 Tech Stack & Architecture

### Backend & Local API
* **Language:** Python 3 (Standard Library only).
* **Core Modules:** `http.server` (API server), `subprocess` (isolated judging), `json` (data persistence), `tempfile` (isolated execution directories), `time`.
* **Database:** Local JSON files for light file-based storage.

### Web Frontend
* **Technologies:** Vanilla JavaScript (ES6+), HTML5, CSS3.
* **UI Framework:** Bootstrap 5 (Responsive for Mobile, Tablet, and Laptop widths).

### Mobile Companion (Extended Scope)
* **Framework:** React Native hosted via Expo Go (Demonstration mode).
* **Key Features:** Real-time polling hooks, Markdown parsing, and native swipe gestures.

---

## ⚙️ Judge Contract & Verdict Rules

The backend judge executes student code in an isolated Python subprocess with size-limited output capture and a per-test execution timeout. 

### Verdict Priority Rule
When a submission runs against multiple test cases, the first failing test decides the overall submission verdict according to the following priority ladder:
1. **Syntax Error:** Compilation or syntax check failed.
2. **Runtime Error:** Unhandled exception or crash during test execution.
3. **Time Limit Exceeded (TLE):** Execution exceeded the problem's allocated time limit.
4. **Wrong Answer:** Output value did not match expected JSON results (within float tolerances).
5. **Accepted:** Solution passed every sample and hidden test case.

---

## 🔒 Security & Safe Usage Limitations

> ⚠️ **CRITICAL SECURITY WARNING**
> This application runs code using standard local subprocess pipelines. It **does not** utilize secure Docker containers, virtual machines, kernel-level sandboxing, or public internet isolation. 
* **Target Audience:** Strictly trusted classroom code running on an instructor’s local machine.
* **Network Scope:** Intended exclusively for deployment within a closed local area network (LAN). Do not expose this server directly to the public internet.

---

## 📂 Project Setup & Installation

### Prerequisites
* Python 3.10+
* Node.js & npm (for the React Native / Expo Mobile App)
* Expo Go app installed on your physical mobile device (iOS/Android)

### 1. Server & Web Frontend Setup
```bash
# Clone the repository
git clone https://github.com
cd codejudge-engine

# Start the local Python server
python3 src/server.py --port 8000
```
Open `http://localhost:8000` in your web browser to access the Role Selection screen.

### 2. Mobile App Setup (Expo Go)
```bash
cd mobile-companion
npm install

# Start the Expo development server
npx expo start
```
* Ensure your computer and mobile phone are connected to the exact **same Wi-Fi network**.
* Configure the server address in the mobile UI using your computer's **LAN IP Address** (e.g., `192.168.1.X:8000`). *Note: Android Emulators connect to the host machine via `10.0.2.2`*.
* Scan the generated QR code using your phone's camera (iOS) or the Expo Go App (Android) to load the viewer.
Use code with caution.
Would you like me to flesh out the exact API endpoints, write the structural JSON schemas for TestCase / Submission, or provide boilerplate unit tests using Python's unittest framework?
