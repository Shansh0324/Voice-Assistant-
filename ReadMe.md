# AI Voice Assistant

An advanced AI voice assistant with comprehensive system control capabilities, built with Python and modern AI technologies.

## Features

### Core Capabilities
- **Voice Interaction**: Real-time speech recognition and text-to-speech
- **Web & Information**: Search the web, get weather information, send emails
- **File Management**: Create, delete, copy, move files and directories
- **System Monitoring**: View system information, running processes, network status
- **Application Control**: Open and manage applications, kill processes
- **System Control**: Shutdown, restart, lock the system, manage volume
- **Recycle Bin**: Empty and manage recycle bin (Windows)
- **Clipboard**: Set and get clipboard content
- **Screen Capture**: Take screenshots
- **Network Tools**: Ping hosts, check connectivity
- **Registry Access**: Read Windows registry values (Windows only)

## Prerequisites

Before setting up the AI Voice Assistant, ensure you have:

- **Python 3.8 or higher** installed on your system
- **Git** for cloning the repository
- **Microphone and speakers** for voice interaction
- **Internet connection** for AI services and web searches

## Installation & Setup

### 1. Clone the Repository

```bash
git clone <repository-url>
cd ai_voice_assistant
```

### 2. Create Virtual Environment

**Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

**macOS/Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Environment Configuration

Create a `.env` file in the project root with your API keys:

```env
# Google Cloud Speech-to-Text API
GOOGLE_APPLICATION_CREDENTIALS=path/to/your/service-account-key.json

# OpenAI API (if using OpenAI for text generation)
OPENAI_API_KEY=your_openai_api_key

# Email Configuration (for email functionality)
EMAIL_ADDRESS=your_email@gmail.com
EMAIL_PASSWORD=your_app_password

# Weather API (optional)
WEATHER_API_KEY=your_weather_api_key
```

### 5. Google Cloud Setup (Required for Speech Recognition)

1. **Create a Google Cloud Project:**
   - Go to [Google Cloud Console](https://console.cloud.google.com/)
   - Create a new project or select an existing one

2. **Enable APIs:**
   - Enable the following APIs:
     - Cloud Speech-to-Text API
     - Cloud Text-to-Speech API
     - Google Generative AI API

3. **Create Service Account:**
   - Go to "IAM & Admin" > "Service Accounts"
   - Create a new service account
   - Download the JSON key file
   - Place it in a secure location and update the path in your `.env` file

### 6. Audio Setup

**Windows:**
- Ensure your microphone is properly configured
- Test microphone in Windows Settings > System > Sound

**macOS:**
- Grant microphone permissions to Terminal/your IDE
- Test microphone in System Preferences > Security & Privacy > Privacy > Microphone

**Linux:**
- Install ALSA or PulseAudio if not already installed
- Test microphone with: `arecord -d 5 test.wav`

## Usage

### Starting the Assistant

1. **Activate the virtual environment:**
   ```bash
   # Windows
   venv\Scripts\activate
   
   # macOS/Linux
   source venv/bin/activate
   ```

2. **Run the assistant in the console:**
   ```bash
   python .\agent.py console
   ```

3. **Voice Commands:**
   - Speak clearly into your microphone
   - Use natural language commands like:
     - "What's the weather in New York?"
     - "Open Chrome browser"
     - "Take a screenshot"
     - "What files are in my Documents folder?"

### Example Commands

**System Control:**
- "Shutdown my computer"
- "Restart the system"
- "Lock my computer"
- "Set volume to 50%"

**File Operations:**
- "Create a new folder called 'Projects'"
- "Delete the file 'old_document.txt'"
- "Copy 'report.pdf' to Desktop"
- "Open the file 'presentation.pptx'"

**Information & Web:**
- "Search for Python tutorials"
- "What's the weather like today?"
- "Send an email to john@example.com"

**System Monitoring:**
- "Show running processes"
- "Check system information"
- "Test network connectivity"

## Safety Features

The assistant includes built-in safety protocols:

- **Confirmation prompts** for destructive actions
- **Error handling** with clear explanations
- **Cross-platform compatibility**
- **Secure credential management**

## Troubleshooting

### Common Issues

1. **Microphone not working:**
   - Check system microphone permissions
   - Ensure microphone is set as default input device
   - Test microphone in system settings

2. **Google Cloud API errors:**
   - Verify service account key is correctly configured
   - Ensure APIs are enabled in Google Cloud Console
   - Check billing is enabled for the project

3. **Audio playback issues:**
   - Check speaker/headphone connections
   - Verify audio drivers are up to date
   - Test audio output in system settings

4. **Import errors:**
   - Ensure virtual environment is activated
   - Reinstall dependencies: `pip install -r requirements.txt`
   - Check Python version compatibility

### Getting Help

- Check the logs in the `KMS/logs/` directory for detailed error information
- Ensure all dependencies are properly installed
- Verify API keys and credentials are correctly configured

## Development

### Project Structure

```
ai_voice_assistant/
├── agent.py          # Main assistant application
├── tools.py          # System control tools and functions
├── prompts.py        # AI prompts and instructions
├── requirements.txt  # Python dependencies
├── .env             # Environment variables (create this)
├── .gitignore       # Git ignore patterns
├── KMS/             # Knowledge management system
│   └── logs/        # Application logs
└── venv/            # Virtual environment (created during setup)
```

### Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

---

**Note:** This assistant has extensive system control capabilities. Use responsibly and always confirm destructive actions before execution.

AGENT_INSTRUCTION = """
You are an advanced AI assistant with comprehensive system control capabilities. You can help users with:

## CORE CAPABILITIES:
- **Web & Information**: Search the web, get weather information, send emails
- **File Management**: Create, delete, copy, move files and directories
- **System Monitoring**: View system information, running processes, network status
- **Application Control**: Open and manage applications, kill processes
- **System Control**: Shutdown, restart, lock the system, manage volume
- **Recycle Bin**: Empty and manage recycle bin (Windows)
- **Clipboard**: Set and get clipboard content
- **Screen Capture**: Take screenshots
- **Network Tools**: Ping hosts, check connectivity
- **Registry Access**: Read Windows registry values (Windows only)

## BEHAVIOR GUIDELINES:
1. **Safety First**: Always confirm destructive actions (delete, shutdown, kill processes)
2. **Clear Communication**: Explain what you're doing before executing system commands
3. **Error Handling**: Provide clear explanations if operations fail
4. **Cross-Platform**: Adapt responses based on user's operating system
5. **Helpful Suggestions**: Offer alternatives when specific tools aren't available

## SAFETY PROTOCOLS:
- Ask for confirmation before:
  - Deleting files permanently
  - Shutting down or restarting the system
  - Killing important processes
  - Emptying recycle bin
  - Making registry changes
- Warn users about potential consequences of destructive actions
- Suggest safer alternatives when appropriate

## RESPONSE STYLE:
- Be conversational and friendly
- Provide step-by-step explanations for complex operations
- Offer additional help or related suggestions
- Use appropriate technical language based on user expertise level

You have extensive system control capabilities - use them responsibly to help users efficiently manage their computer systems.
"""

SESSION_INSTRUCTION = """
Welcome! I'm your comprehensive system assistant. I can help you with:

🔧 **System Management**
- Monitor system performance and processes
- Control applications and processes
- Manage system power (shutdown, restart, lock)

📁 **File Operations**
- Create, delete, copy, move files and folders
- Open files with default applications
- List directory contents
- Manage recycle bin

🌐 **Web & Communication**
- Search the web for information
- Get weather updates for any city
- Send emails through Gmail

🖥️ **System Tools**
- Take screenshots
- Control system volume
- Manage clipboard content
- Check network connectivity
- Access Windows registry (Windows only)

💡 **Smart Features**
- Cross-platform compatibility (Windows, macOS, Linux)
- Safety confirmations for destructive actions
- Detailed error reporting and suggestions
- Contextual help and recommendations

Just tell me what you'd like to do, and I'll help you accomplish it safely and efficiently!

What would you like me to help you with today?
"""