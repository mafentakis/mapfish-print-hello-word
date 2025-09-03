
# MapFish Print Example

Want to see MapFish Print in action? This guide will help you quickly set up and test the MapFish Print service with a simple browser interface.

## Prerequisites

- Docker and Docker Compose installed on your system
- A web browser

## Quick Setup

### 1. Start the MapFish Print Service

Start a local instance of MapFish Print v3 by executing:

```bash
cd docker
docker-compose -f docker-compose.yml up --build
```

This will:
- Build and start the MapFish Print v3 service
- Make it available at `http://localhost:18083/print`
- Set up the necessary print configurations

### 2. Verify the Service

Once the containers are running, you can verify the service is working by visiting:
- **Print Service Capabilities**: http://localhost:18083/print/default/capabilities.json

### 3. Test with the Browser Interface

Open the included test interface in your browser:

```
mapfish-print-browser.html
```

Or navigate directly to the file in your project directory and open it in your browser.


## Available Layouts

- **A4 Portrait**: Standard portrait orientation with legend
- **A4 Landscape**: Landscape orientation with legend
- **A4 Simple**: Basic layout without legend

