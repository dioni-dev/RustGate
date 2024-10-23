
# RustGate

[![Build Status](https://img.shields.io/github/workflow/status/yourusername/rustgate/CI)](https://github.com/yourusername/rustgate/actions)
[![Latest Release](https://img.shields.io/github/v/release/yourusername/rustgate)](https://github.com/yourusername/rustgate/releases)
[![License](https://img.shields.io/github/license/yourusername/rustgate)](LICENSE)

## Overview

**RustGate** is a high-performance, secure **Ingress controller** for **Kubernetes** clusters, written entirely in **Rust**. Designed to provide a robust and fast proxy with enhanced security features, RustGate is ideal for routing traffic in modern cloud-native applications. With RustGate, you can ensure traffic management with low latency, TLS termination, and real-time monitoring of your services. 

### Key Features

- **High-performance Ingress for Kubernetes**: RustGate handles incoming traffic efficiently, ensuring low latency and high throughput for your Kubernetes services.
- **Secure by design**: Built with **Rust's memory safety** guarantees, RustGate ensures a secure, reliable environment for routing traffic.
- **HTTPS and TLS support**: Secure communication with support for HTTPS, including certificate management through integration with Cert-Manager.
- **Real-time traffic visualization**: RustGate includes a built-in **GUI** for monitoring traffic flow and viewing Ingress statistics directly in your web browser.
- **Flexible routing rules**: Fully compliant with Kubernetes Ingress specifications, supporting host-based and path-based routing.
- **Written in Rust**: Built from the ground up in Rust, leveraging the language’s performance and safety to handle high loads with minimal resource consumption.

## Table of Contents

- [Installation](#installation)
- [Getting Started](#getting-started)
- [Configuration](#configuration)
- [Monitoring and Visualization](#monitoring-and-visualization)
- [Contributing](#contributing)
- [License](#license)

## Installation

RustGate can be deployed in any Kubernetes cluster. Follow the steps below to install it using Helm or kubectl.

### Using Helm

```bash
helm repo add rustgate https://yourhelmrepo.com/charts
helm install rustgate rustgate/rustgate --namespace ingress-system
```

### Using kubectl

1. Clone the repository:

   ```bash
   git clone https://github.com/yourusername/rustgate.git
   ```

2. Apply the manifests:

   ```bash
   kubectl apply -f k8s-manifests/deployment.yaml
   ```

This will deploy RustGate into your Kubernetes cluster.

## Getting Started

Once RustGate is installed, it will begin managing **Ingress resources** in your cluster. To define an Ingress rule, create a YAML file like this:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
  annotations:
    kubernetes.io/ingress.class: "rustgate"
spec:
  rules:
  - host: example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: example-service
            port:
              number: 80
```

Apply the rule with `kubectl apply -f example-ingress.yaml`.

## Configuration

RustGate comes with a default configuration that should work for most use cases. However, you can customize it via a configuration file (`config.toml`) or environment variables.

Key configuration options include:

- **TLS/SSL**: Enable or disable TLS support, and configure certificate management.
- **Load balancing**: Choose between round-robin, least connections, or IP hash for balancing traffic across services.
- **Logging**: Adjust log levels to monitor traffic and debug issues.

For advanced configuration, refer to the [Configuration Guide](https://github.com/yourusername/rustgate/wiki/Configuration).

## Monitoring and Visualization

RustGate includes a built-in **GUI** accessible via a web interface at a specific port (default: `8080`). This interface allows you to:

- View real-time traffic flow.
- Monitor requests per second (RPS), latencies, and error rates.
- Visualize the current status of Ingress rules and routes.

### Accessing the GUI

Once deployed, access the dashboard by navigating to:

```
http://<rustgate-ip>:8080/gui
```

This will display the real-time traffic and Ingress management interface.

## Contributing

We welcome contributions from the community! If you'd like to report issues or contribute code, please visit the [Contributing Guide](https://github.com/yourusername/rustgate/blob/main/CONTRIBUTING.md) to get started.

### Development Setup

To set up the project locally:

1. Install Rust: [https://www.rust-lang.org/tools/install](https://www.rust-lang.org/tools/install)
2. Clone the repository:

   ```bash
   git clone https://github.com/yourusername/rustgate.git
   cd rustgate
   ```

3. Build and run the project:

   ```bash
   cargo run
   ```

### Running Tests

To run the test suite:

```bash
cargo test
```

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
