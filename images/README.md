# Images and Screenshots

## Directory Structure

```
images/
├── screenshots/
│   ├── pt/          # Portuguese interface screenshots
│   └── en/          # English interface screenshots
├── diagrams/         # Technical diagrams (mermaid exports)
└── README.md        # This file
```

## Screenshots Needed

### Priority 1 - Essential (Already Referenced in Docs)
- [ ] `dashboard-overview.png` - Visão geral do dashboard (introduction.mdx)
- [ ] `whatsapp-connect-overview.png` - Tela inicial de conexão (conectar-whatsapp.mdx)
- [ ] `whatsapp-qr-code.png` - QR Code para escaneamento (conectar-whatsapp.mdx)
- [ ] `agent-config-tabs.png` - Interface com abas de configuração (configurar-agente.mdx)
- [ ] `agent-test-chat.png` - Chat de teste do agente (quickstart.mdx)
- [ ] `knowledge-base-tabs.png` - Base de conhecimento com métodos (adicionar-conhecimento.mdx)
- [ ] `flow-example-whatsapp.png` - Flow no celular (criar-flows.mdx)
- [ ] `flow-builder-interface.png` - Construtor de flows (criar-flows.mdx)
- [ ] `conversations-interface.png` - Tela de conversas 3 colunas (gerenciar-conversas.mdx)

### Priority 2 - Important
- [ ] `integrations-list.png` - Lista de integrações disponíveis
- [ ] `ai-tools-listing.png` - Listagem de ferramentas
- [ ] `lead-management.png` - Gestão de leads
- [ ] `flow-submission-details.png` - Detalhes de submissão de flow
- [ ] `agent-modules-tools.png` - Aba de módulos e ferramentas

### Priority 3 - Nice to Have
- [ ] `analytics-dashboard.png` - Dashboard de analytics
- [ ] `team-management.png` - Gestão de equipe
- [ ] `workspace-settings.png` - Configurações do workspace
- [ ] `mobile-responsive-views.png` - Visões mobile
- [ ] `knowledge-base-documents.png` - Lista de documentos
- [ ] `conversation-handoff.png` - Transferência para humano

## Screenshot Guidelines

### Technical Specifications
- **Format:** PNG (lossless)
- **Resolution:** 1920x1080 or higher
- **DPI:** 72 (web standard)
- **Max file size:** 500 KB (compress if needed)

### Content Guidelines
- Use demo/example data
- Hide sensitive information (API keys, emails, phone numbers)
- Use consistent theme (light mode as default)
- Clean UI (no browser dev tools, no notifications)
- Show relevant state (e.g., connected channel, active agent)

### Naming Convention

```
[section]-[feature]-[language].png

Examples:
- dashboard-overview-pt.png
- whatsapp-connect-qr-en.png
- agent-config-tabs-pt.png
- flow-builder-preview-en.png
```

## Capturing Screenshots

### Recommended Tools
- **macOS:** Cmd+Shift+4 (native)
- **Windows:** Win+Shift+S (Snipping Tool)
- **Linux:** Flameshot, GNOME Screenshot
- **Browser:** Full Page Screen Capture extension

### Best Practices
1. Use incognito/private mode for clean UI
2. Set browser zoom to 100%
3. Disable browser extensions that show in UI
4. Use consistent window size
5. Capture at actual size (don't scale afterwards)

## Processing Screenshots

### Compression
Use tools like:
- TinyPNG: https://tinypng.com
- ImageOptim (macOS)
- pngquant (CLI)

### Annotations
For tutorial screenshots, use:
- Arrows to highlight key areas
- Numbers for step-by-step guides
- Boxes to focus attention
- Keep annotations minimal and clear

## Diagrams

### Mermaid Diagrams
- Export from mermaid.live
- Save as PNG with transparent background
- Use in documentation with light background

### Architecture Diagrams
- Use consistent color scheme
- Match documentation brand colors
- Keep text readable at normal size
- Export at 2x for retina displays

## Usage in Documentation

Reference screenshots in MDX:

```mdx
<img
  src="/images/screenshots/pt/dashboard-overview-pt.png"
  alt="Dashboard Overview"
  className="rounded-lg border border-gray-200"
/>
```

For comparison (before/after, PT/EN):

```mdx
<Tabs>
  <Tab title="Português">
    <img src="/images/screenshots/pt/feature-pt.png" alt="Feature PT" />
  </Tab>
  <Tab title="English">
    <img src="/images/screenshots/en/feature-en.png" alt="Feature EN" />
  </Tab>
</Tabs>
```

## Status

- ✅ Directory structure created
- ⏳ Screenshots pending capture
- ⏳ Diagrams pending export

## Contact

For questions about screenshots:
- Email: hello@integrabot.ai
- Include this file location in your message
