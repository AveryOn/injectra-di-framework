# Injectra

Injectra is a small dependency injection framework for Node.js and TypeScript.

The package is in early development. The public API is not stable yet.

## Installation

```bash
npm install injectra
```

## Requirements

Injectra currently targets Node.js 24 or higher.

```json
{
  "engines": {
    "node": ">=24.0.0"
  }
}
```

## Usage

Injectra is published as an ESM package.

```ts
import { INJECTRA_VERSION } from 'injectra'

console.log(INJECTRA_VERSION)
```

## Current public API

At the moment, the package exposes only a minimal public entrypoint:

```ts
INJECTRA_VERSION
```

Future versions will provide the main dependency injection API:

```ts
import { Container, Injectable, Inject, Module } from 'injectra'
```

## TypeScript

The package includes TypeScript declarations.

No additional type packages are required.

## Decorator metadata

Injectra depends on `reflect-metadata`.

The package imports it from the public entrypoint, so users do not need to import it manually for the current API.

Future decorator-based APIs may require TypeScript decorator options in the consumer project:

```json
{
  "compilerOptions": {
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true
  }
}
```

## Package format

Injectra is distributed as an ESM package.

```ts
import { INJECTRA_VERSION } from 'injectra'
```

CommonJS `require()` is not supported yet.

## License

MIT
