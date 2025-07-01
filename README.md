# Solvers Build Guide for Xtools-ROBLOX-MULTI-TOOL

This guide explains how to build the `Solvers` directory, which provides Go-based solutions for the [Xtools-ROBLOX-MULTI-TOOL](https://github.com/KKAKSUUWH/Xtools-ROBLOX-MULTI-TOOL) project. These solvers are designed to handle specific tasks like captcha solving, automation, and other backend functionalities for the tool.

---

## 🚀 About Xtools-ROBLOX-MULTI-TOOL
[Xtools-ROBLOX-MULTI-TOOL](https://github.com/KKAKSUUWH/Xtools-ROBLOX-MULTI-TOOL) is a high-performance Roblox multitool built with commercial-grade logic. It includes features like account management, social engagement, group automation, and more. The `Solvers` directory enhances this tool by providing backend logic for specific tasks.

---

## Prerequisites
- [Go](https://golang.org/dl/) installed on your system (version 1.16 or later recommended).
- Basic familiarity with the command line.
- Access to the [Xtools-ROBLOX-MULTI-TOOL](https://github.com/KKAKSUUWH/Xtools-ROBLOX-MULTI-TOOL) repository.

---

## Building the Solvers

### Step 1: Prepare the Workspace
1. Navigate to the `Solvers` directory in the XtoolsAddons project:
   ```bash
   cd /path/to/XtoolsAddons/Solvers
   ```

2. Choose the solver you want to build (e.g., `Syllara` or `freecap(NotTested)`).

### Step 2: Set Up the Go Module
1. Copy the solver file (e.g., `Syllara`) to the root of the `Solvers` directory and rename it to `main.go`:
   ```bash
   cp Syllara main.go
   ```

2. Initialize a Go module for the solver:
   ```bash
   go mod init Addon
   ```

3. Resolve dependencies:
   ```bash
   go mod tidy
   ```

### Step 3: Build and Run
1. Build the solver:
   ```bash
   go build
   ```

2. Run the compiled binary:
   ```bash
   ./Addon
   ```

---

## Usage Example: `Syllara` Solver
The `Syllara` solver is designed to handle captcha challenges for the [Xtools-ROBLOX-MULTI-TOOL](https://github.com/KKAKSUUWH/Xtools-ROBLOX-MULTI-TOOL). Below are the usage instructions for different scenarios:

### For Xtools Users
The solver is **preconfigured** to work seamlessly with the [Xtools-ROBLOX-MULTI-TOOL](https://github.com/KKAKSUUWH/Xtools-ROBLOX-MULTI-TOOL). No additional setup is required. Simply:
1. Ensure the solver is running on the correct port (default: `8080`).
2. The tool will automatically detect and use the solver for captcha challenges.

### For Custom Tool Users
If you are integrating the solver into a **custom tool**, use the following `curl` examples to interact with it:

#### 1. Start the Solver Server
Run the compiled `Syllara` binary with the required flags:
```bash
./Addon -l "https://your-captcha-api-endpoint.com" -p "8080" -k "your-api-key" -v
```
- `-l`: The API endpoint URL for the captcha solver.
- `-p`: The port to run the server on (default: `8080`).
- `-k`: The API key for the captcha solver (required).
- `-v`: Enable verbose logging (optional).

#### 2. Send a Request to the Solver
Use `curl` to create a task:
```bash
curl -X POST http://localhost:8080/createTask \
  -H "Content-Type: application/json" \
  -d '{
    "key": "your-api-key",
    "challengeInfo": {
      "publicKey": "your-public-key",
      "site": "roblox.com",
      "surl": "https://roblox-api.arkoselabs.com",
      "capiMode": "interactive",
      "styleTheme": "light",
      "languageEnabled": true,
      "jsfEnabled": true,
      "extraData": {"blob": "your-blob-data"}
    },
    "browserInfo": {
      "Cookie": "your-cookie",
      "Sec-Ch-Ua": "\"Chromium\";v=\"137\", \"Not.A/Brand\";v=\"24\"",
      "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/137.0.0.0 Safari/537.36",
      "Mobile": false
    },
    "proxy": "your-proxy",
    "cookie_str": "your-cookie-str"
  }'
```

#### 3. Retrieve the Task Result
After creating a task, fetch the result using the `taskId`:
```bash
curl -X GET http://localhost:8080/taskResult/your-task-id
```

#### Expected Response
```json
{
  "status": "completed",
  "result": {
    "solution": "captcha-token",
    "gameInfo": {
      "variant": "variant-name",
      "waves": 3
    },
    "success": true
  }
}
```

---

## Integration Notes
- **Xtools Users**: The solver is preconfigured. No manual interaction is needed.
- **Custom Tool Users**: Ensure the solver outputs match your tool's input requirements and configure the server IP/port accordingly.

---

## Troubleshooting
- **Dependency Issues**: Ensure your `GOPATH` and `GOROOT` are correctly set.
- **Syntax Errors**: Verify the solver file (`main.go`) has no syntax errors before building.
- **Tool Compatibility**: If the solver fails to integrate, check the [Xtools-ROBLOX-MULTI-TOOL documentation](https://docs.xtools.ink) for updates.

---

## Contributing
Contributions to the `Solvers` directory are welcome! Follow these guidelines:
1. Maintain the existing structure and naming conventions.
2. Test your solver with the [Xtools-ROBLOX-MULTI-TOOL](https://github.com/KKAKSUUWH/Xtools-ROBLOX-MULTI-TOOL) before submitting.

---

## License
This project is licensed under the [MIT License](LICENSE), the same as the [Xtools-ROBLOX-MULTI-TOOL](https://github.com/KKAKSUUWH/Xtools-ROBLOX-MULTI-TOOL).
