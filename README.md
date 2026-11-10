# IGLOS

[IGLOS](https://www.iglos.com) (Industrial Grade Linux Operating System) by Linutronix as a Margo app with a `native`
deployment profile, as proposed in [margo/specification-enhancements#109](https://github.com/margo/specification-enhancements/pull/109).
The device's WFM client hands the IGLOS SWUpdate image (`.swu`) to sw-update which places it into the inactive A/B slot and activates it.

## Release

Releases are pushed with `bart` by the [App release](.github/workflows/app_release.yml) workflow, either on a GitHub
release or by running it manually with a version.

The release tag must be the IGLOS image version, for example `13.7.1`. The tag is used as the Margo app version, and
[Margo push](.github/workflows/margo_push.yml) pins the component in [app/margo.yaml](app/margo.yaml) to it:

- `source` becomes `.../IGLOS_Tutorial_Web_App_<tag>.swu` on the public Linutronix Nextcloud share
- `version` becomes `"<tag>"`

The workflow fails if the image for the tag does not exist at that URL, because the device downloads it from there.

`bart validate` does not know the `native` deployment type yet, so validation is expected to fail.
