# AI Bank App - Kubernetes Deployment

A production-grade **Spring Boot banking application** with integrated **AI capabilities** using Ollama, containerized with Docker, and orchestrated with Kubernetes.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Installation & Setup](#installation--setup)
- [Usage](#usage)
- [Deployment](#deployment)
- [Technology Stack](#technology-stack)
- [Security](#security)
- [License](#license)

---

## 🎯 Overview

**AI Bank App** is a modern banking web application that combines robust financial operations with AI-powered features. Built with Spring Boot 3.4.13, it provides secure user authentication, banking transactions, and integrates AI models via Ollama for intelligent features.

The application is production-ready with:
- ✅ Containerized deployment (Docker)
- ✅ Kubernetes orchestration support
- ✅ Security best practices (non-root user, Alpine base)
- ✅ Health checks and monitoring
- ✅ MySQL database integration
- ✅ AI model integration

---

## ✨ Features

### Banking Features
- 👤 User authentication and authorization with Spring Security
- 💳 Account management
- 💰 Transaction processing
- 📊 Balance inquiry
- 🔐 Encrypted sensitive data

### AI Features
- 🤖 Ollama AI integration
- 🧠 TinyLLaMA model support
- 📝 Intelligent assistance for banking operations

### DevSecOps
- 🛡️ CVE remediation (Tomcat, Jackson versions pinned)
- 🔍 Trivy security scanning
- 📈 Prometheus metrics and monitoring
- ✅ Health checks with actuator endpoints

---

## 🏗️ Architecture

