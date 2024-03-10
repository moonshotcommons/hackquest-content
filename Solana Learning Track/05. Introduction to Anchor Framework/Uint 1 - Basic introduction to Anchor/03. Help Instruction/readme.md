# Content

### Help Command

Print a list of all available commands: `anchor help`

```rust
anchor help

available commands:
  init      Initialize a workspace.
  build     Build the entire workspace.
  expand    Expand macros (wrapper for cargo expand).
  verify    Verify that on-chain bytecode matches locally built artifact. Run this command in the program subdirectory, i.e., the directory containing the program's Cargo.toml file.
  test      Run integration tests on the local network.
  new       Create a new program.
  idl       Commands for interacting with the Interface Definition Language (IDL).
  clean     Remove all build artifacts from the target directory except for the program keypair.
  deploy    Deploy each program in the workspace.
  migrate   Run deployment migration scripts.
  upgrade   Command for deploying, initializing the interface, and migrating everything in one go. Upgrade a single program. Configured wallet must have upgrade authority.
  cluster   Cluster commands.
  shell     Start a node shell with anchor client setup.
  run       Run a script defined by the current workspace's anchor.toml.
  login     Save an API token from the registry locally.
  publish   Publish a verified build to the anchor registry.
  keys      Keys commands.
  localnet  Localnet commands.
  account   Get and deserialize an account using the provided interface.
  help      Print this message or the help of the given subcommand.
```

Print help information for a given subcommand: `anchor help [subcommand]`. For example, if you want information about the `deploy` command, you can execute:

```rust
anchor help deploy
```

This will display usage, options, and examples related to the `deploy` command. Help information typically includes explanations on how to use the command correctly and detailed descriptions of available options. The help command is an essential tool for understanding and learning the Anchor framework as it provides detailed information about each command, helping you use them correctly for Solana program development and management.

### Difference Between `anchor init` and `anchor new`

Both commands are used to create Anchor projects, but they serve different purposes:

1. `anchor init`: Initializes a workspace. This command creates a workspace with a basic project structure and configuration files. You need to specify a workspace name, such as `anchor init my_workspace`.
2. `anchor new`: Creates a new program. This command is used to create a new Anchor program (smart contract), including the necessary directories and files. You need to specify a program name, such as `anchor new my_program`.

Generally, you would use `anchor init` to initialize a workspace first and then use `anchor new` to create one or more programs within that workspace.

### Purpose of the `anchor verify` Command

This command is used to verify whether the bytecode of a program deployed on-chain matches the locally built artifact. It is typically used after a developer deploys a program to the Solana blockchain to ensure that the on-chain contract is consistent with the code in the local development environment.

When using this command, you need to run it in the directory containing the  program, which includes the `Cargo.toml` file of the program. Executing `anchor verify` involves comparing the program ID of the on-chain contract with the locally compiled program ID and comparing the bytecode of the on-chain contract with the locally built artifact to ensure they match.

The verification process usually includes the following steps:

1. Check if the program ID of the on-chain contract matches the locally compiled program ID.
2. Compare the bytecode of the on-chain contract with the locally compiled artifact to ensure they match.

Through this command, developers can ensure that the program written in the local development environment is consistent with the contract deployed on the chain, reducing potential errors due to compilation or other environment issues.

### Purpose of the `anchor upgrade` Command

This command is used for a one-time upgrade of a program. Its purpose is to deploy the latest version of the program, initialize the Interface Definition Language (IDL), and integrate the process of executing all migrations. This command is typically used to upgrade a single program rather than the entire workspace. The command involves the following steps:

1. **Deploy the latest version of the program:** This means uploading the latest version of the program to the Solana blockchain network and creating a new instance of the program on-chain. This process includes deploying the new program binary file to the chain to replace the previously deployed program version.
2. **Initialize the Interface Definition Language (IDL):** The IDL is a language that describes the interface of a program, defining the data structures, methods, and events of the contract. The process of initializing the IDL involves deploying these interface definitions to the chain so that clients can interact with the program and correctly parse the contract's data structures and methods.
3. **Execute all necessary migration scripts:** Migration scripts are scripts executed during the upgrade or modification of a contract. They contain logic executed on-chain, such as updating storage structures or migrating data. The purpose of migration scripts is to ensure a smooth transition of on-chain contract state, making the new version of the contract compatible with the old version.
