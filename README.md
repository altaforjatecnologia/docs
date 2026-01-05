# Integrabot Documentation

Official documentation for Integrabot - AI-powered WhatsApp automation platform.

## 📚 Documentation Structure

This documentation is available in:
- 🇧🇷 **Portuguese** (`/pt/`) - Complete documentation
- 🇺🇸 **English** (`/en/`) - Main pages (full translation in progress)

## 🚀 Quick Links

- **Live Documentation:** https://docs.integrabot.ai
- **App:** https://app.integrabot.ai
- **Support:** hello@integrabot.ai

## 📖 Content Overview

### Getting Started
- Introduction to Integrabot
- Quick start guide (5 minutes)
- WhatsApp connection guide

### User Guides
- Configure AI Agent
- Add knowledge to agent
- Create WhatsApp Flows
- Manage conversations
- AI Tools and integrations

### Concepts
- How AI works (RAG, LLM, etc)
- Knowledge base architecture
- WhatsApp Flows technical details
- Integrations overview

### Reference
- Flow components API
- Tool types reference
- Glossary

## 🌐 Translation Status

| Section | Portuguese | English |
|---------|-----------|---------|
| Introduction | ✅ Complete | ✅ Complete |
| Quick Start | ✅ Complete | ✅ Complete |
| User Guides | ✅ Complete | 🔄 In Progress |
| Concepts | ✅ Complete | 🔄 In Progress |
| Reference | ✅ Complete | 🔄 In Progress |

## 🛠️ Built With

- **Platform:** [Mintlify](https://mintlify.com)
- **Deployment:** Automatic on push to `main`
- **Theme:** Light (custom colors)
- **Components:** Cards, Accordions, Tabs, Steps, Code blocks

## 🎨 Design System

### Colors
- Primary: `#34322d` (text-primary)
- Background: `#f8f8f7` (background-main)
- Light: `#6b6963`
- Typography: Libre Baskerville (headings), System fonts (body)

### Components
- CardGroup for feature highlights
- Steps for tutorials
- Accordions for expandable content
- Tabs for alternative options
- Info/Warning/Tip callouts

## 📝 Contributing

To update documentation:

1. Edit `.mdx` files in `/pt` or `/en`
2. Update `mint.json` if adding new pages
3. Commit and push to `main` branch
4. Mintlify deploys automatically

### File Structure
```
integrabot-docs/
├── mint.json           # Main configuration
├── pt/                 # Portuguese docs
│   ├── introduction.mdx
│   ├── quickstart.mdx
│   ├── guias/          # User guides
│   ├── conceitos/      # Concepts
│   └── referencia/     # Reference
├── en/                 # English docs (same structure)
├── images/             # Screenshots and diagrams
└── logo/              # Brand assets
```

## 🔧 Local Development

To preview locally:

```bash
# Install Mintlify CLI
npm install -g mintlify

# Run dev server
mintlify dev

# Access at http://localhost:3000
```

## 📸 Screenshots

Screenshots are organized in:
- `images/screenshots/pt/` - Portuguese UI
- `images/screenshots/en/` - English UI

## 🤝 Support

- **Email:** hello@integrabot.ai
- **Discord:** Coming soon
- **GitHub:** Issues for documentation bugs/suggestions

---

**Last Updated:** January 2025  
**Version:** 2.0  
**Status:** Active Development
