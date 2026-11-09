# OPM Flow Ubuntu 26.04 canary

Daily (04:00 UTC) and manual GitHub Action that installs OPM Flow from
`ppa:opm/ppa` in an `ubuntu:26.04` container. It runs twice: with the apt
default, and with `APT::Architecture-Variants "amd64v3"` enabled.

Each run reports `flow --version`, the package version, and whether the `amd64`
or `amd64v3` variant was installed in the job summary. The job fails if the
version is older than `EXPECTED_OPM_VERSION` (currently 2026.04).

Known cause of failures: the PPA only provides plain `amd64`. With the
`amd64v3` variant enabled, apt prefers the Ubuntu archive's `amd64v3` build
(2025.10) over the PPA's newer version.
