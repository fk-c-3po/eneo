<div align="center">

<img src="docs/assets/Eneo-logo-svg.svg" alt="Eneo Logo" width="400"/> 

# Eneo

**Democratic AI Platform for the Public Sector**

[![License: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-blue.svg)](https://www.gnu.org/licenses/agpl-3.0)
[![Made for: Public Sector](https://img.shields.io/badge/Made%20for-Public%20Sector-green)](https://github.com/sundsvallai/eneo)
[![Contributions Welcome](https://img.shields.io/badge/Contributions-Welcome-brightgreen.svg)](#contributing)
[![Contributors](https://img.shields.io/github/contributors/sundsvallai/eneo)](https://github.com/sundsvallai/eneo/graphs/contributors)

[Getting Started](#-getting-started) • [Features](#-features) • [Documentation](#-documentation) • [Architecture](#️-architecture) • [Contributing](#-contributing)

</div>

---

## 🏛️ What is Eneo?

Eneo is an open-source AI platform specifically designed for Swedish public sector organizations to deploy and manage AI assistants while maintaining complete control over data, security, and algorithms. Originally developed by Sundsvall Municipality and Ånge Municipality, Eneo embodies the principle that **"Generative AI must not be a technology for the few, but a technology for everyone."**

### Why Eneo?

- **🏛️ Public Sector First**: Built specifically for municipal and government organizations with their unique needs and constraints
- **🔒 Data Sovereignty**: Complete control over your data and AI infrastructure - no data leaves your environment
- **🌐 Model Agnostic**: Support for multiple AI providers (OpenAI, Anthropic, Azure, local models) without vendor lock-in
- **🤝 Democratic AI**: Open governance through user association of public sector organizations
- **📋 Compliance Ready**: Built-in support for GDPR and EU AI Act with audit trails and security classifications
- **🔓 Fully Open Source**: AGPL v3 licensed for maximum transparency and community ownership

---

## ✨ Features

### 🤖 AI Assistant Management
- Create and customize AI assistants for specific organizational needs
- Support for multiple AI providers (OpenAI, Anthropic, Azure, local models)
- System prompts and behavior customization
- Assistant-specific API access for integrations

### 🏢 Collaborative Spaces
- **Shared Workspaces**: Team collaboration within organizations
- **Role-based Access**: Admin, Editor, Viewer roles with granular permissions
- **Cross-organizational Sharing**: (**TBA** - planned feature)
- **Production Management**: Mark assistants as published for broader visibility

### 📚 Knowledge Management
- **Document Processing**: PDF, Word, PowerPoint, Excel (CSV) etc with intelligent chunking
- **Web Crawling**: Automated content extraction from websites (Scrapy library)
- **Vector Search**: Semantic search using PostgreSQL with pgvector
- **Real-time Processing**: Background task system for file processing

### ⚡ Real-time Capabilities
- **Streaming Chat**: Server-Sent Events for real-time AI responses
- **WebSocket Updates**: Live status updates for background tasks
- **Background Processing**: Async document processing and web crawling with the worker service

### 🌍 Multi-language Support
- Swedish (base locale) and English interface with type-safe translations
- Seamless language switching without URL changes - language preference stored in cookies
- Live language switching without page reload
- Cookie-based locale persistence

---

## 🚀 Getting Started

Choose your path based on your needs:

### 🏛️ **For Municipal Organizations**
**Want to evaluate Eneo for your organization?**

**📋 Option 1: Learn & Evaluate**
- 📖 **[See Use Cases & Features](#-use-cases)** - Understand what Eneo can do
- 📞 **[Contact Us](mailto:digitalisering@sundsvall.se)** - Get guidance from other municipalities
- 💬 **[Community Issues](https://github.com/sundsvallai/eneo/issues)** - Ask questions and report issues

**🚀 Option 2: Quick Production Deployment**
```bash
# Option A: Clone repository
git clone https://github.com/sundsvallai/eneo.git
cd eneo/docs/deployment

# Option B: Download files only
mkdir eneo-deployment && cd eneo-deployment
curl -O https://raw.githubusercontent.com/sundsvallai/eneo/main/docs/deployment/docker-compose.yml
curl -O https://raw.githubusercontent.com/sundsvallai/eneo/main/docs/deployment/env_backend.template
curl -O https://raw.githubusercontent.com/sundsvallai/eneo/main/docs/deployment/env_frontend.template
curl -O https://raw.githubusercontent.com/sundsvallai/eneo/main/docs/deployment/env_db.template

# Configure and deploy
cp env_backend.template env_backend.env
cp env_frontend.template env_frontend.env  
cp env_db.template env_db.env
# Edit configuration files with your settings, then:
docker network create proxy_tier && docker compose up -d
```

**🌐 Access Your Deployment:**
- **Platform**: https://your-domain.com
- **API Documentation**: https://your-domain.com/docs
- **Default Login**: `user@example.com` / `Password1!`

> 🔐 **Security**: Change default password and update all `your-domain.com` placeholders!

📖 **[Full Production Guide](docs/DEPLOYMENT.md)** for complete deployment instructions

### 🔧 **For Developers**
**Want to contribute or customize Eneo?**

**🎯 Choose Your Development Path:**

**🐳 DevContainer (Recommended for beginners)**
- ✅ Pre-configured environment with all dependencies
- ✅ Consistent across all machines
- 🔧 **Prerequisites:** Docker Desktop + VS Code + Dev Containers extension

```bash
git clone https://github.com/sundsvallai/eneo
cd eneo && code .
# Click "Reopen in Container" when prompted
# If no prompt: Ctrl+Shift+P → "Dev Containers: Reopen in Container"
```

**💻 Manual Setup (For experienced developers)**
- ⚡ Full control over your environment  
- 🔧 Requires: Python ≥3.10, Docker, Node ≥v20, pnpm 8.9.0
- 📺 Need 3 terminals for full functionality

```bash
git clone https://github.com/sundsvallai/eneo
cd eneo
# Setup backend, frontend, and worker (see detailed guide below)
```

**🌐 Access Your Development Environment:**
- **Platform**: http://localhost:3000
- **API Documentation**: http://localhost:8123/docs  
- **Default Login**: `user@example.com` / `Password1!`

> ⚠️ **Note:** File uploads and web scraping require the worker service

📖 **[Complete Development Guide](docs/INSTALLATION.md)** - Detailed setup instructions  
🤝 **[Contributing Guide](docs/CONTRIBUTING.md)** - Coding standards and workflow

---

### 🖼️ Platform Overview

<div align="center">
<img src="docs/assets/eneo_startpage.png" alt="Eneo Personal Assistant Interface" width="800"/>
<p><em>Personal AI Assistant with customizable models and real-time chat interface</em></p>
</div>

<div align="center">
<img src="docs/assets/eneo_space.png" alt="Eneo Collaborative Spaces" width="800"/>
<p><em>Collaborative spaces for team-based AI development and deployment</em></p>
</div>

### ⚡ **Quick Production Deployment Details**

**Prerequisites:** Docker, Docker Compose, AI provider API key

**Security Requirements:**
- Generate unique JWT_SECRET: `openssl rand -hex 32`
- Replace all default passwords immediately
- Update `your-domain.com` in configuration files

**Access Points:**
- **Platform**: https://your-domain.com
- **API Documentation**: https://your-domain.com/docs  
- **Default Login**: `user@example.com` / `Password1!`

> 🔐 **Important**: Change default credentials immediately after first login!

---

## 🏗️ Architecture

Eneo follows a modern microservices architecture with clean separation of concerns:

<details>
<summary>🔍 Click to view architecture diagram</summary>
<img src="docs/assets/eneo_architecture.png" alt="Eneo Architecture Diagram" width=800/>

</details>

### Technology Stack

- **Frontend**: SvelteKit with TypeScript, Tailwind CSS
- **Backend**: FastAPI (Python 3.11+) with SQLAlchemy
- **Database**: PostgreSQL 13 with pgvector extension
- **Cache/Queue**: Redis with ARQ task processing
- **Deployment**: Docker Compose with Traefik reverse proxy
- **AI Integration**: Multi-provider support (OpenAI, Anthropic, Azure, etc.)

---

## 📚 Documentation

| Document | Purpose |
|----------|---------|
| **[Installation Guide](docs/INSTALLATION.md)** | Development environment setup |
| **[Deployment Guide](docs/DEPLOYMENT.md)** | Production deployment |
| **[Architecture Guide](docs/ARCHITECTURE.md)** | Technical architecture overview |
| **[Contributing Guide](docs/CONTRIBUTING.md)** | Development workflow |
| **[Troubleshooting](docs/TROUBLESHOOTING.md)** | Common issues and solutions |
| **[Security Guide](docs/SECURITY.md)** | Security practices |

### API Documentation
- **Development**: http://localhost:8123/docs
- **Production**: https://your-domain.com/docs
- **OpenAPI Schema**: Auto-generated from FastAPI
- **Type Safety**: Full TypeScript types for frontend integration

---

## 🔧 Contributing

Eneo is developed by the Swedish public sector for the global community. Contributions are welcome from municipalities, organizations, and individuals who share our vision of democratic AI.

> 📋 **Important**: Before contributing, review our [Contribution Standards](docs/CONTRIBUTING.md#-contribution-standards-and-requirements) to ensure your PR aligns with platform goals.

### Quick Contribution Guide

1. **Fork** the repository
2. **Create** a feature branch
3. **Follow** coding standards (see [Contributing Guide](docs/CONTRIBUTING.md))
4. **Write tests** for new functionality
5. **Submit** a pull request

### Development Standards
- **Python**: PEP 8, type hints, comprehensive testing
- **TypeScript**: ESLint configuration, strict type checking
- **Architecture**: Domain-driven design patterns
- **Testing**: Unit and integration test coverage

For detailed guidelines, see our [Contributing Guide](docs/CONTRIBUTING.md).

---

## 🤝 Community & Governance

### Democratic Control
Eneo is governed by a user association of public sector organizations, ensuring that development priorities align with public interest rather than commercial goals.

### User Association
- **Digital Collaboration**: Join our collaboration space for municipalities
- **Knowledge Sharing**: Share experiences and best practices
- **Collective Development**: Influence platform direction through democratic participation

**Contact**: `digitalisering@sundsvall.se` for collaboration space access (public sector organizations only)

### Open Source Commitment
- **License**: AGPL v3 ensures all improvements remain open
- **No Vendor Lock-in**: Use any AI provider or deployment method
- **Community Driven**: Decisions made collectively by user association

---

## 📈 Use Cases

### Municipal Applications
- **Citizen Services**: AI assistants for municipal websites
- **Internal Operations**: Administrative support and automation
- **Cross-municipal Collaboration**: Share AI applications between municipalities
- **Compliance Management**: Built-in GDPR and AI Act compliance tools

### Enterprise Applications
- **Knowledge Management**: Organizational knowledge bases with AI search
- **Customer Support**: AI-powered assistance with internal data
- **Document Processing**: Automated analysis and summarization
- **Integration Platform**: Connect with existing enterprise systems

---

## 🔒 Security & Compliance

- **Data Protection**: GDPR-compliant by design
- **EU AI Act Ready**: Built-in compliance features
- **Audit Trails**: Comprehensive logging and tracking
- **Security Classifications**: Data sensitivity handling
- **Access Control**: Role-based permissions and multi-tenancy

---

## 🆘 Support & Help

**Get Help:**
- **🐛 Bug Reports**: [GitHub Issues](https://github.com/sundsvallai/eneo/issues)
- **💬 Community Discussion**: [GitHub Discussions](https://github.com/sundsvallai/eneo/discussions)  
- **📖 Documentation**: [docs/](docs/) folder for comprehensive guides
- **📧 Municipal Collaboration**: digitalisering@sundsvall.se (public sector organizations)

**Response Times:**
- **Community**: Best effort response via GitHub
- **Municipal Partners**: Priority support for public sector organizations

---

## 🙏 Acknowledgments

Eneo builds on the success of [Open ePlatform](https://www.openeplatform.org/), another Swedish municipal open-source project used by 200+ municipalities since 2010.

**Original Development**: Sundsvall Municipality & Ånge Municipality, Sweden 🇸🇪

**Inspiration**: Learning from Open ePlatform's success in creating sustainable municipal collaboration

**Acknowledgment**: We extend our thanks to InooLabs AB (Now Intric AB) for their foundational contributions to Intric (now Eneo).

---

## 📜 License

```
Eneo - Democratic AI Platform for the Public Sector
Copyright (C) 2023-2025 Sundsvall Municipality & Ånge Municipality

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as published
by the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU Affero General Public License for more details.
```

See [LICENSE](LICENSE) for the complete AGPL v3 license text.

---

<div align="center">

**Made with ❤️ by the Swedish Public Sector for the Global Community**

*Empowering democratic access to AI technology*

[🌐 Project Website](#) • [📧 Contact](mailto:digitalisering@sundsvall.se) • [💬 Community](https://github.com/sundsvallai/eneo/issues)

</div>
