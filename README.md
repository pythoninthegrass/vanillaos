# pythoninthegrass' opinionated vib image

## Use my custom image

### But why tho?

Some quality of life packages are pre-installed:

* `ptyxis`: container-aware terminal
  * Nicer alternative to Blackbox IMHO
* `docker`: OG container runtime
  * For those who need/want to use Docker over Podman
  * Podman is still available and the `vso shell` container image is Podman-based
* `vim`: to start flame wars
* `ansible`: configuration management
* `bat`: cat clone with wings
* `build-essential`: build tools
* A number of [other packages](recipe.yml#L40-L74) primarily for development

The ethos of immmutable OSes like Vanilla OS is to run everything in containers or Flatpaks, this is a happy medium that enables an easier transition for those who are used to running things on the host.

It also speeds up the initial onboarding since less packages need to be layered via `abroot` post-install.

### Quickstart

Point ABRoot to pythoninthegrass' custom image to use it.

* Open a terminal and run `vso shell`
  * Default with `Blackbox`, only necessary over SSH or another terminal
* Edit the configuration file with the command: `abroot config-editor`
* Change the "name" entry from something like `vanilla-os/desktop` to `pythoninthegrass/vanillaos`
* Now, run `abroot upgrade` to switch to the custom image

**Exhibit A**:

```json
{
  "registry": "ghcr.io",
  "registryService": "registry.ghcr.io",
  "registryAPIVersion": "v2",
  "name": "pythoninthegrass/vanillaos",
  "tag": "main",
}
```

## Other quality of life items

### Homebrew

Install [Homebrew](https://docs.vanillaos.org/handbook/en/install-homebrew). Then add `brew` to the `PATH` and `shellenv` to `.bash_aliases` (sourced by default in `~/.bashrc`).

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
touch ~/.bash_aliases
echo 'export PATH="/home/linuxbrew/.linuxbrew/bin:$PATH"' >> ~/.bash_aliases
(echo; echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"') >> ~/.bash_aliases
source ~/.bashrc
```

### Distrobox

Install [Distrobox](https://docs.vanillaos.org/handbook/en/install-distrobox) et al.

```bash
curl -s https://raw.githubusercontent.com/89luca89/distrobox/main/install | sh -s -- --next --prefix ~/.local
```

Add `distrobox`'s `bin` directory to the `PATH` to `.bash_aliases`.

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bash_aliases
source ~/.bashrc
```

Create a `distrobox` configuration file in `~/.config/distrobox/distrobox.conf` with the following content:

```ini
container_always_pull="1"
container_generate_entry=0
container_manager="docker"
container_image_default="registry.fedoraproject.org/fedora-toolbox:latest"
container_name_default="distrobox-default"
container_user_custom_home="$HOME/.config/distrobox/home"
# container_init_hook="~/.local/distrobox/a_custom_default_init_hook.sh"
# container_pre_init_hook="~/a_custom_default_pre_init_hook.sh"
non_interactive="1"
skip_workdir="0"
```

Pull an image and use the container:

```bash
distrobox create --name ubuntu-lts --image ubuntu:latest
distrobox enter --name ubuntu-lts
cat /etc/os-release
exit
distrobox stop ubuntu-lts
```

## Further Reading

> [!TIP]
> It is suggested to check the [Vib documentation](https://docs.vanillaos.org/collections/vib) to know more about the recipe format, structure of modules and the supported fields.

* [Vib images](https://github.com/Vanilla-OS/Vib)
* [Official Vanilla OS images](https://images.vanillaos.org)
* [How to add docker into my custom Vanilla OS image? : r/vanillaos](https://www.reddit.com/r/vanillaos/comments/1em7ke6/how_to_add_docker_into_my_custom_vanilla_os_image/)
* [How to create a good developer environment : r/vanillaos](https://www.reddit.com/r/vanillaos/comments/1dhslfe/how_to_create_a_good_developer_environment/)
* [Christian Hergert / ptyxis · GitLab](https://gitlab.gnome.org/chergert/ptyxis)
