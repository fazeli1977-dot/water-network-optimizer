# Water Network Optimizer

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue?logo=python)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

Python toolkit for sizing pressurized water pipes and calculating frictional head loss with the Hazen-Williams equation.

Developer: Alireza Sani · [alirezafazeli@live.com](mailto:alirezafazeli@live.com)

## Features

- Hazen-Williams head loss and velocity for each pipe
- Discrete diameter selection inside a velocity band, 0.6 m/s to 2.5 m/s by default
- CSV export of the sizing schedule
- A command-line entry point and an importable package

## Formulation

Frictional head loss in SI units:

```text
h_f = 10.67 * L * Q^1.852 / (C^1.852 * D^4.87)
```

- `h_f` is head loss in metres
- `L` is pipe length in metres
- `Q` is discharge in cubic metres per second
- `C` is the Hazen-Williams coefficient
- `D` is the internal diameter in metres

## Setup

```bash
git clone https://github.com/fazeli1977-dot/water-network-optimizer.git
cd water-network-optimizer
python -m venv .venv
source .venv/bin/activate
python -m pip install -e .
```

On Windows PowerShell, activate the environment with `.\.venv\Scripts\Activate.ps1`.

## Run

```bash
python -m water_network_optimizer examples/sample_network.json --csv outputs/sizing_results.csv
```

`--min-v` and `--max-v` change the allowable velocity band. The command prints total network length and total head loss, and writes the sizing table to the CSV path.

## Scope & Engineering Assumptions

- **Steady-State Hazen-Williams Sizing:** Computes frictional head loss and selects discrete commercial pipe diameters within a target velocity band (`0.6-2.5 m/s` by default).
- **Not a Full Looped Solver:** Intended for preliminary pipe sizing and head-loss screening on defined pipe segments/flows, rather than full looped-network pressure balancing (e.g., EPANET) or transient/water-hammer analysis.
- **Minor Losses & Fittings:** Local/fitting losses and elevation/pump-curve hydraulics are outside the current scope unless accounted for externally.

## Tests

```bash
python -m pytest -q
```

## Project structure

```text
src/water_network_optimizer/
├── hydraulics.py
├── optimizer.py
├── io.py
└── cli.py
examples/sample_network.json
tests/
```

## Related work

- [water-sampling-app](https://github.com/fazeli1977-dot/water-sampling-app)
- [ClimateLens](https://github.com/fazeli1977-dot/ClimateLens)
- [SAR-MotionLens](https://github.com/fazeli1977-dot/SAR-MotionLens)

## License

MIT License. See [LICENSE](LICENSE).

## Author

Alireza Sani — [fazeli1977-dot](https://github.com/fazeli1977-dot)

