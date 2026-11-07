# DreadCabinet

> A powerful tool that brings order to your digital chaos, one file at a time!
> Organize, rename, and transform your notes or files based on date, subject, and other metadata—all within your own CLI applications.

## Features

- **Date-based organization** – Place files into folders by year, month, or day (or no structure at all).  
- **Flexible filename generation** – Include date, time, and a subject in filenames.  
- **Recursion** – Process all subdirectories (or just the top level) as you prefer.  
- **Timezone support** – Convert file timestamps or metadata to a specific timezone for naming.  
- **Extension filtering** – Restrict processing to certain file types.  
- **No destructive operations** – Original files remain untouched; DreadCabinet only creates copies in a new directory structure.
- **Concurrent processing** – Process multiple files in parallel for improved performance.

## Installation

```console
npm install @utilarium/dreadcabinet
```

*Or with other package managers:*

```console
# yarn
yarn add @utilarium/dreadcabinet
```

## Quick Start

DreadCabinet is a library designed to be integrated into your own CLI tools. Here's a basic example:

```javascript
import { Command } from 'commander';
import * as DreadCabinet from '@utilarium/dreadcabinet';

// Create a new instance with options
const instance = DreadCabinet.create({
  defaults: {
    timezone: 'America/New_York',
    extensions: ['md', 'txt'],
    outputStructure: 'month',
    outputDirectory: './dist',
  }
});

// Configure your command
const program = new Command();
await instance.configure(program);

// Parse arguments and process
program.parse(process.argv);
const cliArgs = program.opts();
const config = await instance.read(cliArgs);
const finalConfig = instance.applyDefaults(config);
await instance.validate(finalConfig);

// Use the operator to process files
const operator = await instance.operate(finalConfig);
await operator.process(async (file) => {
  // Your file processing logic here
});
```

Once integrated, users can process files with commands like:

```console
my-app \
  --input-directory . \
  --output-directory ./organized \
  --output-structure month \
  --extensions md
```

## Documentation

For complete documentation, including detailed configuration options, advanced usage examples, and integration guides, visit:

**[📖 DreadCabinet Documentation](https://tobrien.github.io/dreadcabinet/)**

### Quick Links

- [Getting Started Guide](https://tobrien.github.io/dreadcabinet/#getting-started)
- [CLI Options Reference](https://tobrien.github.io/dreadcabinet/#cli-options)
- [Configuration Files](https://tobrien.github.io/dreadcabinet/#configuration-files)
- [Advanced Usage](https://tobrien.github.io/dreadcabinet/#advanced-usage)
- [API Reference](https://tobrien.github.io/dreadcabinet/#api-reference)

## Contributing

We welcome contributions! Please see our [Contributing Guide](https://tobrien.github.io/dreadcabinet/#contributing) for details.

## License

[Apache-2.0](./LICENSE) © 2025 Tim O'Brien TEST
