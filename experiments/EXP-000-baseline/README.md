# EXP-000 — Hardware & Environment Baseline

## ID

`EXP-000-baseline`

## Date

2026-09-22

## Question

What is the reproducible baseline state of the hardware and software environment that will be used for the AI Agent Lab?

## Hypothesis

The laboratory can establish a useful, reproducible starting point by recording the laptop's hardware identity, software versions, available storage, and idle resource state before installing or configuring any AI-specific software.

This experiment is expected to document the environment, not to establish inference performance or make architecture decisions.

## Hardware

### Repository baseline — already known

These values are recorded from the repository's initial hardware baseline and should be verified against the actual machine where possible:

| Component | Baseline value | Status |
|---|---|---|
| CPU | Intel Core i7-12650H | Known from repository baseline |
| GPU | NVIDIA RTX 4060 Laptop GPU | Known from repository baseline |
| VRAM | 8 GB | Known from repository baseline |
| RAM | 32 GB | Known from repository baseline |
| Storage | 2 TB | Known from repository baseline |
| Operating system | Windows 11 | Known from repository baseline |

### Actual machine measurements

Complete this section from the measurement procedure below. Do not infer exact values from the repository baseline.

| Component | Measured value | Measurement date/time | Command or source |
|---|---|---|---|
| CPU model | _Pending measurement_ | _Pending_ | _Pending_ |
| GPU name | _Pending measurement_ | _Pending_ | `nvidia-smi` |
| GPU memory total | _Pending measurement_ | _Pending_ | `nvidia-smi` |
| Installed RAM | _Pending measurement_ | _Pending_ | PowerShell system information |
| Storage capacity and free space | _Pending measurement_ | _Pending_ | `Get-Volume` |

## Software

### Repository baseline — already known

| Software or platform | Baseline value | Status |
|---|---|---|
| Operating system family | Windows 11 | Known from repository baseline |
| Windows version/build | Not specified | Must be measured on the actual machine |
| NVIDIA driver version | Not specified | Must be measured on the actual machine |
| CUDA version reported by the NVIDIA driver | Not specified | Must be measured on the actual machine |
| Python version | Not specified | Must be measured on the actual machine |
| Git version | Not specified | Must be measured on the actual machine |
| PowerShell version | Not specified | Must be measured on the actual machine |

### Actual machine measurements

| Software or platform | Measured value | Measurement date/time | Command or source |
|---|---|---|---|
| Windows product/version/build | _Pending measurement_ | _Pending_ | `Get-ComputerInfo` |
| NVIDIA driver version | _Pending measurement_ | _Pending_ | `nvidia-smi` |
| CUDA version reported by NVIDIA driver | _Pending measurement_ | _Pending_ | `nvidia-smi` |
| Python version | _Pending measurement_ | _Pending_ | `python --version` |
| Git version | _Pending measurement_ | _Pending_ | `git --version` |
| PowerShell version | _Pending measurement_ | _Pending_ | `$PSVersionTable` |

No local LLM runtime, model, inference server, CUDA Toolkit, AI-specific Python package, container runtime, WSL2 distribution, database, MCP server, agent, RAG system, or cloud infrastructure is part of this experiment.

## Model

None. No model is installed, selected, loaded, or evaluated as part of EXP-000.

## Configuration

- Machine role: normal personal laptop and laboratory machine.
- Operating state: normal Windows 11 desktop environment with no AI experiment running.
- Measurement state: allow the machine to settle at idle before collecting resource measurements.
- Network state: record whether the machine is connected to the network, but do not expose or start any service.
- Power state: record whether the laptop is on AC power or battery and, if relevant, the selected Windows power mode.
- AI-specific configuration: none.
- Permanent system changes: none.

Experiments may later use substantial CPU, GPU, VRAM, RAM, power, and thermal capacity when intentionally running. EXP-000 does not impose artificial resource limits and does not configure the laptop as a continuously running server.

## Variables

### Recorded variables

- Windows version and build.
- NVIDIA driver version.
- CUDA version reported by the NVIDIA driver, if `nvidia-smi` reports one.
- Python version.
- Git version.
- PowerShell version.
- Available storage on the relevant volume(s).
- CPU utilization at idle.
- GPU utilization at idle.
- GPU temperature at idle.
- GPU VRAM usage at idle.
- System RAM usage at idle.

### Context variables

Record these alongside the measurements because they can affect idle values:

- Measurement date and local time.
- AC power or battery state.
- Windows power mode, if available.
- Whether ordinary user applications were open.
- Whether Windows Update, antivirus scanning, backups, games, or other unusually active processes were running.
- Number of repeated samples and the sampling interval.

## Procedure

1. Confirm that no AI experiment, local model server, benchmark, game, or other intentionally resource-intensive workload is running.
2. Do not install software or change system configuration for this experiment.
3. Close unusually heavy applications while preserving the normal desktop environment. Record any ordinary applications intentionally left open.
4. Connect AC power or record that the machine is running on battery. Record the Windows power mode if available.
5. Let the machine remain undisturbed for approximately five minutes so transient startup activity can settle.
6. Open PowerShell and run the safe, read-only commands listed below.
7. For idle utilization and temperature values, collect at least three samples where practical. Record the sample time, interval, and whether the value is a point-in-time reading or an average.
8. Copy the command output into the Results section or retain it as an experiment artifact, together with the exact date and time it was collected.
9. If a command is unavailable, record that fact and the error rather than substituting an unverified value.
10. After measurement, leave the laptop in its normal usable state. Do not enable a persistent service or make a permanent system modification.

### Safe PowerShell measurement commands

These commands query local state and do not install or modify software.

#### Windows version and build

```powershell
Get-ComputerInfo | Select-Object WindowsProductName, WindowsVersion, OsBuildNumber
```

Optional additional system identity:

```powershell
Get-CimInstance Win32_OperatingSystem | Select-Object Caption, Version, BuildNumber, LastBootUpTime
```

#### NVIDIA driver, GPU, and CUDA reporting

```powershell
nvidia-smi
```

Preferred structured GPU query, where available:

```powershell
nvidia-smi --query-gpu=name,driver_version,memory.total,memory.used,temperature.gpu,utilization.gpu,power.draw --format=csv
```

The CUDA version shown by `nvidia-smi` is the CUDA compatibility/runtime version reported by the installed NVIDIA driver. It is not evidence that the CUDA Toolkit is installed.

#### Python, Git, and PowerShell versions

```powershell
python --version
```

```powershell
git --version
```

```powershell
$PSVersionTable | Select-Object PSVersion, PSEdition, OS, Platform
```

#### Available storage

For all mounted file-system volumes:

```powershell
Get-Volume | Select-Object DriveLetter, FileSystemLabel, FileSystem, Size, SizeRemaining, HealthStatus
```

For the system volume specifically:

```powershell
Get-Volume -DriveLetter C | Select-Object DriveLetter, Size, SizeRemaining, HealthStatus
```

#### CPU utilization at idle

This collects five one-second samples of total processor utilization:

```powershell
Get-Counter '\Processor(_Total)\% Processor Time' -SampleInterval 1 -MaxSamples 5
```

#### RAM usage at idle

```powershell
Get-CimInstance Win32_OperatingSystem | Select-Object @{Name='TotalRAM_GB';Expression={[math]::Round($_.TotalVisibleMemorySize / 1MB, 2)}}, @{Name='FreeRAM_GB';Expression={[math]::Round($_.FreePhysicalMemory / 1MB, 2)}}, @{Name='UsedRAM_GB';Expression={[math]::Round(($_.TotalVisibleMemorySize - $_.FreePhysicalMemory) / 1MB, 2)}}, @{Name='UsedRAM_Percent';Expression={[math]::Round((($_.TotalVisibleMemorySize - $_.FreePhysicalMemory) / $_.TotalVisibleMemorySize) * 100, 2)}}
```

#### GPU utilization, temperature, and VRAM at idle

The structured NVIDIA query above records GPU utilization, temperature, total memory, and used memory in one read-only command. Run it at least three times, approximately one second apart, if a single point-in-time sample is not sufficient:

```powershell
1..3 | ForEach-Object { Get-Date -Format 'yyyy-MM-dd HH:mm:ss'; nvidia-smi --query-gpu=name,driver_version,memory.total,memory.used,temperature.gpu,utilization.gpu,power.draw --format=csv; Start-Sleep -Seconds 1 }
```

## Measurements

### Measurement record

Populate the table after running the procedure. Use exact values and units from command output; do not replace missing data with estimates.

| Measurement | Value | Unit | Sample count/interval | Date/time | Source |
|---|---:|---|---|---|---|
| Windows version/build | _Pending_ | — | 1 | _Pending_ | PowerShell |
| NVIDIA driver version | _Pending_ | — | 1 | _Pending_ | `nvidia-smi` |
| CUDA version reported by driver | _Pending_ | — | 1 | _Pending_ | `nvidia-smi` |
| Python version | _Pending_ | — | 1 | _Pending_ | PowerShell |
| Git version | _Pending_ | — | 1 | _Pending_ | PowerShell |
| PowerShell version | _Pending_ | — | 1 | _Pending_ | PowerShell |
| Available storage | _Pending_ | GB/TB free | 1 | _Pending_ | `Get-Volume` |
| CPU utilization at idle | _Pending_ | % | _Pending_ | _Pending_ | `Get-Counter` |
| GPU utilization at idle | _Pending_ | % | _Pending_ | _Pending_ | `nvidia-smi` |
| GPU temperature at idle | _Pending_ | °C | _Pending_ | _Pending_ | `nvidia-smi` |
| GPU VRAM usage at idle | _Pending_ | MiB/GB | _Pending_ | _Pending_ | `nvidia-smi` |
| RAM usage at idle | _Pending_ | GB/% | _Pending_ | _Pending_ | PowerShell |

## Results

Pending measurement on the actual machine.

The initial repository-known hardware baseline is:

- Intel Core i7-12650H CPU.
- NVIDIA RTX 4060 Laptop GPU with 8 GB VRAM.
- 32 GB RAM.
- 2 TB storage.
- Windows 11.

Exact operating-system build, driver, CUDA reporting, tool versions, available storage, and idle resource values must be filled from the measured command output. No result should be marked confirmed solely because it appears in the repository baseline.

## Interpretation

EXP-000 establishes the reference environment against which later experiments can report changes and resource use. It distinguishes repository-provided hardware information from values measured on the actual machine and preserves the conditions under which the baseline was collected.

This is not a performance benchmark. It does not measure tokens per second, latency, model quality, sustained thermals, or workload behavior. Idle measurements are only a reference point and should not be interpreted as maximum available capacity or as evidence of suitability for a particular model.

## Limitations

- Idle utilization varies with Windows services, updates, antivirus activity, background applications, thermal state, and power mode.
- A point-in-time GPU temperature or utilization reading does not characterize sustained workload behavior.
- `nvidia-smi` reports information exposed by the NVIDIA driver; its CUDA field does not prove that the CUDA Toolkit is installed.
- Reported storage depends on partitioning, filesystem formatting, reserved space, and which volume is measured.
- The repository baseline may not match the current physical laptop exactly until each component is measured.
- No measurement here establishes model compatibility, inference speed, quality, power draw under load, or upgrade requirements.
- The experiment intentionally does not evaluate Windows versus WSL2 or any local LLM runtime.

## Conclusion

EXP-000 will provide a reproducible hardware and software starting point before introducing local AI infrastructure. It records the current personal-laptop environment without installing dependencies, starting services, imposing artificial resource limits, or making permanent system changes.

The experiment is complete only after the pending measurements are collected, dated, and recorded with their command sources. Until then, the repository-known hardware values are provisional context rather than a fully measured baseline.

## Next experiment

The next experiment should be proposed only after this record is measured and reviewed. It may investigate a local inference setup, but it must separately define its runtime, model, configuration, workload, resource measurements, and rollback procedure.

EXP-000 does not:

- select an LLM runtime;
- select a model;
- decide between Windows and WSL2;
- determine whether a hardware upgrade is necessary;
- configure a model server or persistent AI service;
- establish a 24/7 homelab/server design.

Those decisions belong to later, separately recorded experiments.
