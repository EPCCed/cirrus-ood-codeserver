# Cirrus Open OnDemand - Code Server

## Overview

An [Open OnDemand](https://openondemand.org/) Batch Connect app that launches
[Code Server](https://coder.com/) as an interactive web-based session on OSC
HPC clusters. Code Server provides a full
[VS Code](https://code.visualstudio.com/) editing experience running on a
compute node and accessible through a browser.

This app uses the Batch Connect `basic` template with Slurm and supports
the Cirrus cluster. Jobs run on one node. Typically only a few cores are
required to support the server, running non-exclusively, but up to one whole
node in exclusive mode can be requested.

- **Forked from:** [OSC BC Code Server](https://github.com/OSC/bc_osc_codeserver)
- **Upstream project:** [Code Server](https://coder.com/) / [VS Code](https://code.visualstudio.com/)
- **Batch Connect template:** `basic`
- **Scheduler:** Slurm


## Requirements

### Compute Node Software

This Batch Connect app requires [Code Server](https://coder.com/) to be installed
on the EPPCFS file system. It is launched from [the template job script](template/script.sh.erb).

### Open OnDemand

- Tested to work with the latest version of Open OnDemand
- Slurm scheduler

## Configuration

### form.yml.erb attributes

| Attribute                      | Widget        | Description                                    | Default          |
|--------------------------------|---------------|------------------------------------------------|------------------|
| `cluster`                      | select        | Target cluster ID(s)                           | `cirrus`         |
| `auto_accounts`                | select        | Account to which job is charged                | top-level budget |
| `auto_queues`                  | select        | Partition on which to launch job               | `standard`       |
| `auto_qos`                     | select        | QoS to use for the job                         | `standard`       |
| `custom_walltime`              | string        | Maximum job wall time in HH:MM:SS format       | `01:00:00`       |
| `num_cores`                    | select        | Number of cores for job (1/2/4/8/16/32/72/144/288) | `2` |
| `working_dir`                  | path_selector | Working directory for the Code Server session  | `${HOME/home/epccfs}` |

## Known Limitations

- The authentication provided by code-server, used in the OOD server to code-server hop, is unencrypted

## Troubleshooting

### Connection timeout

Not encountered on Cirrus, but noted by OSC:
The app may need more time to start. Increase the connection timeout or check that the compute node can open the required port.

## Testing

<!-- TODO: Update with sites where this app has been deployed -->

## Contributing

For bugs or feature requests,
[open an issue](https://github.com/EPCCed/cirrus-ood-codeserver/issues).

## References

- [Code Server](https://coder.com/) -- the application launched by this app
- [VS Code](https://code.visualstudio.com/) -- the editor Code Server is based on
- [code-server GitHub releases](https://github.com/coder/code-server/releases)
  -- binary releases of Code Server
- [Open OnDemand](https://openondemand.org/) -- the HPC portal framework
- [OOD Batch Connect app development docs](https://osc.github.io/ood-documentation/latest/app-development.html)

## License

* Documentation, website content, and logo is licensed under
  [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/)
* Code is licensed under GPL-3.0 (See LICENSE.xt)

## Acknowledgments

This app is built on [Open OnDemand](https://openondemand.org/), developed and
maintained by the [Ohio Supercomputer Center (OSC)](https://www.osc.edu/).

Open OnDemand is supported by the National Science Foundation under awards
[NSF SI2-SSE-1534949](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1534949)
and [NSF CSSI-Frameworks-1835725](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1835725).

