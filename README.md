# Plant Disease Recognition System 🌿🔍

An AI-powered web application that identifies 38 different classes of plant diseases from leaf images. Built with **Streamlit** and **TensorFlow/Keras**.

## Features
- **38 Disease Classes:** Covers a wide range of crops including Apple, Corn, Grape, Potato, Tomato, and more.
- **Accurate Predictions:** Uses pre-trained Deep Learning models (using `trained_model.h5`).
- **User-Friendly Dashboard:** Simple navigation and leaf analysis interface.
- **Real-time Feedback:** Shows the top matching prediction and details the confidence scores.
- **Security Hardened:** Implements robust client/server protections against common vulnerabilities.

## How to Run Locally

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/plant-disease-detection.git
cd plant-disease-detection
```

### 2. Set up a Virtual Environment
```bash
python -m venv venv

# On Windows (Command Prompt / PowerShell):
.\venv\Scripts\activate

# On Linux/macOS:
source venv/bin/activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Run the Streamlit App
```bash
streamlit run main.py
```

## Security Controls Implemented

The application has been hardened to prevent unauthorized access, info disclosure, and Denial of Service (DoS) attacks:

1. **File Upload Restrictions**:
   - Enforced file extensions to only accept **`.jpg`**, **`.jpeg`**, and **`.png`**.
   - Maximum upload file size limited to **`5MB`** both programmatically and at the Streamlit server level (via `config.toml`) to prevent memory exhaustion / DoS attacks.
2. **File Validation**:
   - Every uploaded image is verified via `PIL.Image.open()` and `img.verify()` to confirm that it is a valid, uncorrupted image and not a disguised or spoofed script file.
3. **Information Disclosure Prevention**:
   - Configuration `client.showErrorDetails = false` is active, suppressing Python tracebacks or model filepaths in the user interface during errors.
   - Internal loading errors or prediction issues are outputted to `sys.stderr` for server administrators instead of being displayed in the web dashboard.
4. **Server Protections**:
   - CORS is disabled (`server.enableCORS = false`).
   - XSRF Protection is enabled (`server.enableXsrfProtection = true`).
   - File watcher is turned off (`server.fileWatcherType = "none"`) to minimize CPU/file locking overhead and remove exposure paths.

## Model Compatibility
- **Primary Model**: `trained_model.h5` is the active, verified model file. It is fully compatible with TensorFlow 2.21+ / Keras.
- **Secondary Model Note**: `trained_model.keras` contains a layer variable expectation mismatch with modern Keras 3 and is kept as a backup, but the application automatically handles and falls back safely to `trained_model.h5`.

## Technologies Used
- **Python 3.12+**
- **Streamlit** (Web UI & application server)
- **TensorFlow / Keras** (Deep learning inference)
- **NumPy & Pillow** (Image processing & validation)

---
*Created with ❤️ to help farmers and gardeners protect their crops.*
