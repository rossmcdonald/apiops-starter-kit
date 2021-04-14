# Konnect APIOps Starter Kit

This repository can be used as a template for an end-to-end automation framework enabling an APIOps workflow. By following the instructions below, you will:

- Install `deck`, Kong's declarative configuration tool
- Use `deck` to capture the current state of your Konnect environment
- Use `deck` to declaratively make updates to your Konnect services - defining new services, applying policies, etc

## Prerequisites

Before getting started, you'll need to have the following items:

- [ ] A [Kong Konnect](https://konnect.konghq.com/) account.
- [ ] A Konnect Gateway runtime synced with your Konnect environment. If you don't yet have a Gateway available, see the Runtime Manager for your account [here](https://konnect.konghq.com/runtime-manager) for instructions on how to create one (using the "Configure Runtime" option).
- [ ] Access to a CLI with [decK](https://github.com/kong/deck) installed (installation instructions [here](https://github.com/kong/deck#installation)).

Once you have the items above, you're ready to get started.

## Configuring decK

To start, let's create a decK configuration which will automatically provide our Konnect credentials when running commands. Write the following contents to `~/.deck.yaml`:

```yaml
konnect-email: my-email@example.com
konnect-password: my-password123!
```

Once created, make sure the decK configuration is secure by running the following command:

```sh
chmod 0644 ~/.deck.yaml
```

To verify decK is properly configured, you can run the command:

```sh
deck konnect ping
```

If all went well, the output should look similar to the following.

```sh
$ deck konnect ping
Successfully Konnected as Your Name (Your Org)!
```

If you don't see a message similar to the above, then double check your configuration and credentials.

> The default deck configuration lives at `~/.deck.yaml`, however you can override it from the CLI with a `--config` command (for example, `deck --config my/deck/config.yaml`).

## Persisting the Initial Configuration

If you already have entities configured within Konnect, we'll want to persist them to a local state file so that we don't lose them on future updates. To dump the current configuration, run:

```sh
deck konnect dump
```

Once completed, you should now have a `konnect.yaml` in your local directory with the current state of your Konnect environment. For example:

```sh
$ head konnect.yaml 
_format_version: "0.1"
service_packages:
- name: Accounts Service
  description: This service provides features related to account management.
  versions:
  - version: v0.8.0
...
```

> If you don't have anything in Konnect yet, don't sweat it. Feel free to use the sample configuration within this repository (`konnect-sample.yaml`) as a starting point. You can rename it like so:
>
> ```
> cp konnect-sample.yaml konnect.yaml
> ```
> 
> Once renamed, you are ready to go.

