# voice-openclaw-neww


## 🚀 Voice OpenClaw – Setup & Commands

### 1. Start the Frontend

Run the following command in the frontend project directory:

```bash
npm start
```

### 2. Activate the Python Virtual Environment

Activate the backend virtual environment:

```bash
source .venv/bin/activate
```

### 3. Start the Backend

Run the FastAPI backend using Uvicorn:

```bash
uvicorn backend.main:app --host 0.0.0.0 --port 8081 --reload
```

**Backend details:**
- Port: `8081`
- Host: `0.0.0.0`
- Auto-reload: Enabled for development

### 4. OpenClaw Commands

#### Gateway Management

| Command | Description |
|---|---|
| `openclaw gateway restart` | Restart the OpenClaw gateway |
| `openclaw gateway stop` | Stop the OpenClaw gateway |

#### OpenClaw Interface

| Command | Description |
|---|---|
| `openclaw tui` | Open the terminal user interface (TUI) |
| `openclaw dashboard` | Open the OpenClaw dashboard in a browser |

#### Models Management

| Command | Description |
|---|---|
| `openclaw models status` | Check the current model status |
| `openclaw models list` | List available models |

#### Skills Management

| Command | Description |
|---|---|
| `openclaw skills list` | List available OpenClaw skills |

#### Configuration & Setup

| Command | Description |
|---|---|
| `openclaw configure` | Configure OpenClaw settings |
| `openclaw onboard` | Run the OpenClaw onboarding process |

### 5. Development Notes

- Run the frontend and backend in separate terminal sessions.
- Activate the Python virtual environment before starting the backend.
- Use `--reload` during development. For production, configure an appropriate deployment setup.
- Ensure OpenClaw is installed and configured before running its commands.

Note: The command source .venv/bin/activate is suitable for Linux/macOS or WSL. If you run the backend directly in Windows PowerShell, use:

```bash
.\.venv\Scripts\Activate.ps1
```


### 5. Gemini API & Google Model Configuration

#### Authentication Setup

Configure OpenClaw to authenticate using a Gemini API key:

```bash
openclaw onboard --auth-choice gemini-api-key
```

#### Google Models

List available models from the Google provider:

```bash
openclaw models list --provider google
```

#### OpenClaw Configuration File

View the current OpenClaw configuration:

```bash
cat ~/.openclaw/openclaw.json
```

Edit the configuration file:

```bash
nano ~/.openclaw/openclaw.json
```

#### Check the Default Model

Check which model is configured as the default model:

```bash
openclaw config get agents.defaults.model
```

#### Configure the Gemini API Key

Set the Google provider's Gemini API key:

```bash
openclaw config set models.providers.google.apiKey YOUR_NEW_GEMINI_API_KEY
```

**Important:** Replace `YOUR_NEW_GEMINI_API_KEY` with your actual Gemini API key. Never commit real API keys or other secrets to GitHub.

### 6. Debugging & Session Management

#### View Gemini Test Results

Display the contents of the Gemini test JSON file:

```bash
cat /tmp/gemini_test.json
```

#### Monitor OpenClaw Logs

Follow OpenClaw logs in real time to monitor activity and troubleshoot errors:

```bash
openclaw logs --follow
```

Press `Ctrl + C` to stop following the logs.

#### Manage OpenClaw Sessions


### 7. Test Gemini API Connection

Use the following command to test whether the Gemini API is accessible and can generate a response.

```bash
KEY="YOUR_GEMINI_API_KEY"; \
curl -s -o /tmp/gemini_test.json -w "HTTP_STATUS=%{http_code}\n" \
-H "Content-Type: application/json" \
-X POST \
"https://generativelanguage.googleapis.com/v1beta/models/gemini-3.5-flash:generateContent?key=$KEY" \
-d '{"contents":[{"parts":[{"text":"Say hello"}]}]}'; \
cat /tmp/gemini_test.json
```

**Purpose:**
- Sends a test prompt (`Say hello`) to the Gemini API.
- Uses `curl` to send a POST request.
- Displays the HTTP response status code.
- Saves the API response to `/tmp/gemini_test.json`.
- Prints the JSON response for inspection.

**Expected result:** An HTTP `200` status indicates that the request succeeded. The response JSON should contain the generated text.

**Requirements:**
- A valid Gemini API key.
- Access to the specified Gemini model.
- Internet connectivity and an available API quota.

**Troubleshooting:**

| Status code | Possible cause |
|---|---|
| `200` | Request succeeded |
| `400` | Invalid request or parameters |
| `401` / `403` | Authentication or permission issue |
| `404` | Model or endpoint not found |
| `429` | Rate limit or quota exceeded |

**Security note:** Replace `YOUR_GEMINI_API_KEY` with your actual API key when running the command. Never commit real API keys to GitHub. The model name shown in this example must also be supported by your Gemini API access.


List the available OpenClaw sessions:

```bash
openclaw sessions list
```

