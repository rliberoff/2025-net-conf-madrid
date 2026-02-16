# .NET 💖 Artificial Intelligence <br> A session from the .NET Conf Madrid 2025

## Table of Contents / Tabla de contenidos

- [English](#english)
  - [What you’ll learn](#what-youll-learn)
  - [Key building blocks](#key-building-blocks)
  - [Unified API across providers](#unified-api-across-providers)
  - [Middleware & observability](#middleware--observability)
  - [Multimodal by design](#multimodal-by-design)
  - [Agentic systems & ecosystem](#agentic-systems--ecosystem)
  - [MCP (Model Context Protocol)](#mcp-model-context-protocol)
  - [Links](#links)

- [Español](#español)
  - [Qué aprenderás](#qué-aprenderás)
  - [Piezas clave](#piezas-clave)
  - [API unificada entre proveedores](#api-unificada-entre-proveedores)
  - [Middlewares y observabilidad](#middlewares-y-observabilidad)
  - [Multimodal por diseño](#multimodal-por-diseño)
  - [Sistemas agénticos y ecosistema](#sistemas-agénticos-y-ecosistema)
  - [MCP (Model Context Protocol)](#mcp-model-context-protocol-1)
  - [Enlaces](#enlaces)

---

## English

### What you'll learn

- How **.NET AI libraries** provide a consistent developer surface for GenAI apps (chat, embeddings, vector stores). 
- Why a **unified API** helps you switch models/providers without rewriting your app.
- How to keep **telemetry and middleware patterns** you already know (OpenTelemetry, Aspire, Application Insights).
- How **multimodal inputs/outputs** are represented in a practical way.
- Where **agentic systems** fit: Azure AI Foundry + Agent Framework + tools (search, functions, workflows).

### Key building blocks

- **Microsoft.Extensions.AI**: common abstractions and primitives for AI scenarios.
- **Microsoft.Extensions.VectorData**: vector data operations and abstractions.
- **AI Templates**: out-of-the-box guidance and scaffolding.
- **Agent Framework**: multi-agent workflows and orchestration.
- **Model evaluation**: scoring/evaluations across dimensions.

### Unified API across providers

The session highlights using a single set of abstractions to talk to different providers (local or cloud), keeping your app code largely stable.

**Example (conceptual)**

```csharp
// Provider A (local): e.g., Ollama
var uri = new Uri("http://localhost:11434");
var client = new OllamaApiClient(uri) { SelectedModel = "mistral:latest" };

await foreach (var chunk in client.GenerateAsync("How are you today?"))
    Console.Write(chunk.Response);
```

```csharp
// Provider B (cloud): e.g., OpenAI-compatible
var client = new OpenAIChatClient("gpt-4o-mini", Environment.GetEnvironmentVariable("OPENAI_API_KEY"));
var response = await client.GetResponseAsync("How are you today?");
Console.WriteLine(response.Message?.Content?.FirstOrDefault()?.Text);
```

> The goal is **portability**: model/provider changes should be configuration-driven, not code-driven.

### Middleware & observability

A key message: AI calls shouldn’t be a “black box”. Instrumentation aligns with the ASP.NET Core mindset:

- Hook AI clients into familiar **middleware-style pipelines**.
- Emit **OpenTelemetry** events and export to **Application Insights**, or view them in **.NET Aspire** dashboards.

### Multimodal by design

Modern GenAI isn’t text-only. The session describes a simple approach:

- An **AIContent** hierarchy for typed content.
- **DataContent** as the workhorse type for media (audio/video/images): essentially bytes + media type.

### Agentic systems & ecosystem

The talk connects .NET app development with “agentic” architectures:

- **Azure AI Foundry** as the ecosystem (models, agents, tools, safety/governance).
- **Microsoft Agent Framework** for multi-agent orchestration.
- Typical tools: **Azure AI Search**, Bing grounding, **Functions**, **Logic Apps**, storage, key vault, channels (e.g., Bot Service).

### MCP (Model Context Protocol)

- Microsoft (with Anthropic) is building an **official MCP SDK for C#**.
- It aims to **faithfully implement the MCP spec**, enabling interoperability with MCP servers.
- Preview versions evolve quickly—expect occasional breaking changes.

### Links

- Session author: https://www.codertectura.com/
- YouTube: https://www.youtube.com/@codertectura
- MCP C# SDK code: https://aka.ms/mcp-cs-sdk
- MCP C# SDK docs: https://modelcontextprotocol.github.io/csharp-sdk

---

## Español

### Qué aprenderás

- Cómo las **librerías de IA para .NET** ofrecen una superficie común para apps GenAI (chat, embeddings, vector stores).
- Por qué una **API unificada** permite cambiar modelos/proveedores sin reescribir la aplicación.
- Cómo conservar patrones conocidos de **middlewares y telemetría** (OpenTelemetry, Aspire, Application Insights).
- Cómo representar de forma práctica **entradas/salidas multimodales**.
- Dónde encajan los **sistemas agénticos**: Azure AI Foundry + Agent Framework + herramientas (búsqueda, funciones, workflows).

### Piezas clave

- **Microsoft.Extensions.AI**: abstracciones y bloques básicos para escenarios de IA.
- **Microsoft.Extensions.VectorData**: operaciones y abstracciones para datos vectoriales.
- **AI Templates**: plantillas y guía “out-of-the-box”.
- **Agent Framework**: orquestación y flujos multi-agente.
- **Model evaluation**: evaluación y scoring en varias dimensiones.

### API unificada entre proveedores

Se enfatiza una única capa de abstracción para hablar con distintos proveedores (local o cloud), manteniendo el código estable.

**Ejemplo (conceptual)**

```csharp
// Proveedor A (local): p.ej., Ollama
var uri = new Uri("http://localhost:11434");
var client = new OllamaApiClient(uri) { SelectedModel = "mistral:latest" };

await foreach (var chunk in client.GenerateAsync("How are you today?"))
    Console.Write(chunk.Response);
```

```csharp
// Proveedor B (cloud): p.ej., compatible OpenAI
var client = new OpenAIChatClient("gpt-4o-mini", Environment.GetEnvironmentVariable("OPENAI_API_KEY"));
var response = await client.GetResponseAsync("How are you today?");
Console.WriteLine(response.Message?.Content?.FirstOrDefault()?.Text);
```

> Objetivo: **portabilidad**. El cambio de modelo/proveedor debe ser por configuración, no por cambios de código.

### Middlewares y observabilidad

Idea central: las llamadas a IA no deben ser “caja negra”. La instrumentación se alinea con ASP.NET Core:

- Integrar clientes de IA con pipelines estilo **middleware**.
- Emitir eventos **OpenTelemetry** y exportarlos a **Application Insights**, o visualizarlos en paneles de **.NET Aspire**.

### Multimodal por diseño

La GenAI moderna no es solo texto. Se propone un enfoque simple:

- Jerarquía **AIContent** para contenido tipado.
- **DataContent** como tipo principal para medios (audio/vídeo/imagen): bytes + tipo de medio.

### Sistemas agénticos y ecosistema

Se conecta el desarrollo en .NET con arquitecturas agénticas:

- **Azure AI Foundry** como ecosistema (modelos, agentes, herramientas, safety/gobernanza).
- **Microsoft Agent Framework** para orquestación multi-agente.
- Herramientas típicas: **Azure AI Search**, grounding con Bing, **Functions**, **Logic Apps**, storage, key vault, canales (p.ej., Bot Service).

### MCP (Model Context Protocol)

- Microsoft (junto a Anthropic) está creando un **SDK MCP “oficial” para C#**.
- Busca implementar fielmente la **especificación MCP**, habilitando interoperabilidad con servidores MCP.
- Las versiones preview evolucionan rápido; puede haber cambios rompientes.

### Enlaces

- Autor de la sesión: https://www.codertectura.com/
- YouTube: https://www.youtube.com/@codertectura
- Código SDK MCP C#: https://aka.ms/mcp-cs-sdk
- Docs SDK MCP C#: https://modelcontextprotocol.github.io/csharp-sdk

---

### Disclaimer / Aviso

[EN] This README is a summarized interpretation of the AI sessions from the [Global .NET Conf 2025](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oXtIlvq1tuORUtZqVG-HdCt), and is provided “_as-is_”.

[ES] Este README es una interpretación resumida de las sesiones de IA de la [Global .NET Conf 2025](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oXtIlvq1tuORUtZqVG-HdCt) y se proporciona “_tal cual_”.
