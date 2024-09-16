# pythoninthegrass' opinionated vib image

## Use my custom image

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

## Further Reading

> [!TIP]
> It is suggested to check the [Vib documentation](https://docs.vanillaos.org/collections/vib) to know more about the recipe format, structure of modules and the supported fields.

* [Vib images](https://github.com/Vanilla-OS/Vib)
* [Official Vanilla OS images](https://images.vanillaos.org)
