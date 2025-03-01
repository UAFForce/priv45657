## Setup 

### Prerequisites 

Make sure you have the following installed:

- Node.js (v14 or above) 
- npm (Node Package Manager) 

### Development Mode 

1. Clone this repository:

   ```bash
   git clone https://github.com/uafforce/priv45657.git
   cd priv45657
   ```

2. Install the required dependencies:

   ```bash
   npm install
   ```

3. Create the necessary files:
   - `data/proxies.txt` - List of proxies.
   - `data/uas.txt` - List of user agents.

4. Run the server in development mode:

   ```bash
   npm run dev
   ```

   - The **frontend** runs on `http://localhost:5173`.
   - The **backend** runs on `http://localhost:3000`.

---

### Production Mode 💥

1. Clone the repository and navigate to the project directory:

   ```bash
   git clone https://github.com/uafforce/priv45657.git
   cd priv45657
   ```

2. Install the dependencies:

   ```bash
   npm install
   ```

3. Build the project:

   ```bash
   npm run build
   ```

4. Start the server in production mode:

   ```bash
   npm run start
   ```

   In production mode, both the **frontend** and **backend** are served on the same port (`http://localhost:3000`).

> Don't forget to add the necessary files `data/proxies.txt` and `data/uas.txt`.

## Usage 

Once the server is up and running, you can interact with it via the frontend:

1. **Start Attack**:
   - Set up the attack parameters: target URL, attack method (HTTP Flood, Slowloris, TCP, etc...), packet size, duration, and delay.
   - Press "Start Attack" to initiate the stress test.

2. **Stop Attack**:
   - Press "Stop Attack" to terminate the ongoing attack.

### Example Request

```json
{
  "target": "http://example.com",
  "attackMethod": "http_flood",
  "packetSize": 512,
  "duration": 60,
  "packetDelay": 500
}
```

## Adding Proxies and User-Agents

Access to the ``data/proxies.txt`` and ``data/uas.txt`` can now be done fully in the frontend. Click the text button to the right of the beam button to open up the editor.

## Worker-Based Attack Handling 

Each attack type is handled in a separate worker thread, ensuring that the main server remains responsive. The attack workers are dynamically loaded based on the selected attack method (HTTP, etc...).


### Adding New Attack Methods 

To extend the server with new attack methods (e.g., Minecraft, TCP, UDP, DNS), you can create new worker files and add them to the server configuration.

For example:

- Add a new attack method in the frontend settings.
- Create the corresponding worker file (e.g., `minecraftAttack.js`).
- Update the attack handler configuration to include the new method.

```javascript
const attackHandlers = {
  http_flood: "./workers/httpFloodAttack.js",
  http_slowloris: "./workers/httpSlowlorisAttack.js",
  tcp_flood: "./workers/tcpFloodAttack.js",
  minecraft_ping: "./workers/minecraftPingAttack.js",

  // Add more protocols as needed!
  your_protocol: "./workers/yourProtocolAttack.js"
};
```

---

### FAQs

**1. What operating system does MMB support?**

> **Windows**, **Linux**, **Mac** and **Android (untested)**

**2. It crashes on startup, giving a "concurrently" error**

> Try running two terminals instead of one, in the first one use "npm run dev:client", and in the other one "npm run dev:server". (This happened to several people with Windows 11)

**3. I go to "<http://localhost:3000>" and nothing appears.**

> Port `3000` is the server port, to see the UI you must use port `5173` (<http://localhost:5173>)

**4. Requests fail to be sent to the target server (Read timeout and variations)**

> You must put the corresponding proxies in the file `data/proxies.txt`. On each line, put a different proxy that will be used to perform the attack. The format must be the following:
>
> - `protocol://user:password@host:port` (Proxy with authentication)
> - `protocol://host:port`
> - `host:port` (Uses http as default protocol)
> - `host` (Uses 8080 as default port)

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Disclaimer

Please note that this project is not for educational purposes only and should  be used for malicious purposes.
