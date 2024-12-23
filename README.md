# Keycast

Secure remote signing and permissions for teams using Nostr.

## Overview

Keycast aims to make remote signing and secure key management easy for teams using Nostr. Previous solutions like [nsec.app](https://nsec.app/), [Knox](https://gitlab.com/soapbox-pub/knox), and [Amber](https://github.com/greenart7c3/Amber) are great for individuals, but Keycast is designed for teams. This means that you can collaboratively manage your keys and create policies and permissions to control who can sign and what they can sign.

Keycast is fully open source and will offer both a hosted version (if you don't want to have to manage your own deployment) and options for running your own sovereign instance via Docker, StartOS, or Umbrel.

## Features

- [x] NIP-98 HTTP Auth based web application and API authentication
- [x] Team management (create teams, manage stored keys, manage users, manage policies). Supports multiple teams per user.
- [x] Secure key management (row-level aes-256 encryption, file or aws kms backed key storage)
- [x] Permissions and policies (flexible, extensible permissions model)
- [ ] NIP-46 Remote signing for managed keys
- [ ] Docker based deployment
- [ ] StartOS service
- [ ] Umbrel app
- [ ] CLI for managing teams, keys, users, and policies

## Contributing

Contributions are welcome! Please fork or clone the repository and submit a PR with your changes. Small, well-documented changes are appreciated.

### The stack

The `api` subdirectory is a Rust application that uses SQLx for database interactions on a local SQLite database. We use `cargo watch` to run the API in watch mode, make sure to install that if you don't already have it.
- [Rust](https://www.rust-lang.org/)
- [SQLx](https://github.com/launchbadge/sqlx)
- [cargo-watch](https://github.com/watchexec/cargo-watch)

The `web` subdirectory contains a SvelteKit app that uses Bun for bundling and Tailwind for styling.
- [SvelteKit](https://kit.svelte.dev/)
- [Bun](https://bun.sh/)
- [Tailwind](https://tailwindcss.com/)

### Getting Started

1. Clone the repository and install workspace dependencies with `bun install`
2. Install the web app dependencies with `cd web && bun install`
3. Config is done with config.rs files. You shouldn't have to change anything to get started but you can modify the config.toml file to change the database url and migrations path.
4. Then, from the root directory, generate a master encryption key with `bun run key:generate`. This master key is used to encrypt and decrypt Nostr private keys in the database. These are only decrypted when used and remain encrypted at rest. In the future we hope to support other key storage methods, like AWS KMS.

### Running the dev server (API + Web)
1. You can now run the dev server with `bun run dev`. We use `concurrently` to run the API and web app in parallel. You'll see the web app start up at `https://localhost:5173` and the API will start up at `http://localhost:3000`. Both apps will output logs to the console and will hotreload on code changes.


### Managing the database

The database is a local SQLite database. There is a helper command to reset the database (drop, create, and run migrations). More can be added as needed.

- `bun run db:reset` - Reset the database (drop, create, and run migrations)

### Running the signing daemon
1. To actually process any signing requests you'll need to run the signing daemon. #TODO
2. You can also check the status of the signing daemon with #TODO

### Deployment




## License

[MIT](LICENSE)

## Contributors

<a align="center" href="https://github.com/erskingardner/keycast/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=erskingardner/keycast" />
</a>
