# CX Plugins

A collection of Claude plugins for customer experience teams. Each plugin provides decision frameworks and skills that help CX leaders optimize their support operations.

## Available Plugins

| Plugin | Description | Skills |
|--------|-------------|--------|
| [fin-optimization](./fin-optimization/) | Decision frameworks for optimizing Intercom Fin AI agent | `content-advisor`, `procedure-advisor` |

## Installation

Each plugin is a self-contained directory. To use a plugin:

1. Clone this repo (or download the plugin folder you want)
2. Copy the plugin directory into your project
3. The skills inside will be available to Claude when working in that project

```bash
# Clone the full marketplace
git clone https://github.com/YOUR_USERNAME/cx-plugins.git

# Or copy a single plugin into your project
cp -R cx-plugins/fin-optimization /path/to/your/project/
```

## Plugin Format

Each plugin follows this structure:

```
plugin-name/
├── README.md                  # What the plugin does and how to use it
├── .claude-plugin/
│   └── plugin.json            # Plugin metadata (name, version, description)
└── skills/
    └── skill-name/
        ├── SKILL.md            # Skill instructions and behavior
        └── references/         # Supporting knowledge files
```

## Contributing

To add a new plugin, create a directory at the root of this repo following the plugin format above. Each plugin should include a README explaining its purpose and usage.
