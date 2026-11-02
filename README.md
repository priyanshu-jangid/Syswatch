# SysWatch
### A Modular Linux Resource Monitor Using Direct `/proc` Filesystem Sampling

<p align="center">
  <strong>A lightweight, real-time Linux system monitoring application built with C++20 and ncurses.</strong>
</p>

---

## 1. Project Overview

**SysWatch** is a terminal-based Linux system monitoring application designed to provide real-time information about system performance and resource utilization.

The application collects and displays information about CPU usage, memory consumption, disk activity, network traffic, running processes, GPU statistics, and other system-level information.

The main objective of SysWatch is to provide a lightweight alternative to traditional graphical system monitoring applications by using Linux system interfaces and presenting the collected information through an interactive terminal dashboard.

SysWatch is developed using C++20 and the ncurses library. It uses Linux interfaces such as the `/proc` filesystem and `/sys` filesystem to collect system information without requiring a separate monitoring server.

## 2. Key Features

SysWatch provides several system monitoring capabilities.

- **CPU Monitoring:** Displays CPU utilization, temperature, frequency, and individual core statistics.
- **Memory Monitoring:** Shows RAM usage, available memory, buffers, cache, and swap information.
- **GPU Monitoring:** Displays GPU utilization, temperature, clock frequency, power consumption, and VRAM information where supported.
- **Disk Monitoring:** Tracks disk space, device-level I/O activity, and utilization.
- **Network Monitoring:** Displays network interface traffic, including received and transmitted data.
- **Process Monitoring:** Lists running processes and allows sorting based on CPU, memory, GPU, and process ID.
- **Port Monitoring:** Identifies listening network ports and associated processes.
- **System Services:** Displays the status of systemd services.
- **Database Monitoring:** Provides information about supported database services.
- **Web Server Monitoring:** Displays information about supported web server processes.
- **Cron Monitoring:** Provides information about scheduled cron jobs.
- **Activity History:** Displays historical resource utilization through terminal-based graphs.

Some monitoring capabilities depend on the availability of the corresponding Linux utilities, hardware interfaces, and system permissions.

## 3. Dashboard Modes

SysWatch provides three different dashboard modes.

### 3.1 Default Mode

The default dashboard provides an overview of the system's current resource utilization.

It includes:
- CPU utilization and temperature.
- RAM and memory statistics.
- GPU information.
- Disk usage and activity.
- Network traffic.
- System activity history.
- Top running processes.

### 3.2 Zen Mode

Zen Mode provides a consolidated monitoring interface that displays important system information in a simplified layout.

It includes process information, network ports, system services, database information, cron jobs, and other monitoring details.

Press `z` to switch to Zen Mode.

### 3.3 Pro Mode

Pro Mode provides a more detailed monitoring interface for users who want additional system-level information.

It includes:
- Individual CPU core statistics.
- Detailed memory breakdown.
- Kernel and file descriptor statistics.
- GPU information.
- Network connections.
- Disk I/O statistics.
- Database and web server information.
- System services and scheduled tasks.

Press `P` to switch to Pro Mode.

## 4. Technology Stack

| Technology | Purpose |
|---|---|
| C++20 | Core application development |
| ncurses | Terminal-based user interface |
| CMake | Build configuration and compilation |
| Linux `/proc` | System and process information |
| Linux `/sys` | Hardware and device information |
| systemd | System service information |
| Git | Version control |

## 5. Project Structure

The project follows a modular structure in which different system monitoring functionalities are organized into separate components.

```text
Syswatch/
│
├── include/
│   ├── hmon/
│   └── metrics/
│
├── src/
│   ├── core/
│   │
│   ├── plugins/
│   │   ├── cpu/
│   │   ├── gpu/
│   │   ├── system/
│   │   ├── process/
│   │   ├── ports/
│   │   ├── systemd/
│   │   ├── database/
│   │   ├── webserver/
│   │   └── cron/
│   │
│   └── main.cpp
│
├── CMakeLists.txt
├── README.md
├── LICENSE
└── .gitignore
```

**Main components:**

- `src/main.cpp`: Contains the main application and dashboard implementation.
- `src/core/`: Handles plugin management and application-level functionality.
- `src/plugins/`: Contains individual system monitoring modules.
- `include/`: Contains shared headers, interfaces, and metric definitions.
- `CMakeLists.txt`: Defines the build configuration and dependencies.

## 6. Installation and Requirements

SysWatch is designed for Linux-based operating systems.

### System Requirements

| Requirement | Minimum |
|---|---|
| Operating System | Linux |
| C++ Compiler | GCC or Clang with C++20 support |
| CMake | 3.16 or newer |
| ncurses | Development library |
| Git | Recommended |

### Installing Dependencies

For Ubuntu and Debian-based distributions, install the required packages:

```bash
sudo apt update

sudo apt install -y \
    build-essential \
    cmake \
    libncurses-dev \
    git
```

For NVIDIA GPU monitoring, `nvidia-smi` must be available through the appropriate NVIDIA driver utilities.

### Verify Installation

Check the installed compiler:

```bash
g++ --version
```

Check CMake:

```bash
cmake --version
```

## 7. Environment Variable Setup

SysWatch does not require a `.env` file or any mandatory environment variables for normal operation.

The application obtains system information directly from Linux interfaces and available system utilities.

Therefore:

- No API keys are required.
- No database credentials need to be configured for basic monitoring.
- No external monitoring server is required.
- No sensitive configuration values need to be added to the repository.

Optional monitoring capabilities may depend on locally installed utilities and appropriate system permissions.

## 8. Building the Project Locally

Follow these steps to compile SysWatch on your Linux machine.

### Step 1: Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/syswatch.git
```

Navigate into the project directory:

```bash
cd syswatch
```

### Step 2: Configure the Project

Generate the CMake build configuration:

```bash
cmake -S . -B build
```

### Step 3: Compile the Application

Build the project using all available CPU cores:

```bash
cmake --build build -j$(nproc)
```

After successful compilation, the executable will be generated inside the `build` directory.

### Step 4: Run the Application

```bash
./build/hmon
```

The terminal-based monitoring dashboard should now appear.

> **Note:** The current CMake target generates an executable named `hmon`. This will be changed to `syswatch` as part of the executable renaming.

## 9. Command-Line Options

SysWatch supports several command-line arguments for customizing its execution.

| Command | Description |
|---|---|
| `-h`, `--help` | Display help information |
| `-v`, `--version` | Display application version |
| `-r`, `--refresh` | Set refresh interval in seconds |
| `-t`, `--top` | Set the number of processes displayed |
| `--no-gpu` | Disable GPU monitoring |
| `--no-history` | Disable activity history graphs |
| `--zen` | Start directly in Zen Mode |
| `--pid` | Lock focus on a particular process ID |
| `--no-color` | Disable terminal colors |

Examples:

Start the application with a custom refresh interval:

```bash
./build/hmon --refresh 2
```

Display more processes:

```bash
./build/hmon --top 15
```

Start directly in Zen Mode:

```bash
./build/hmon --zen
```

Disable GPU monitoring:

```bash
./build/hmon --no-gpu
```

## 10. Keyboard Controls

The application supports keyboard-based navigation.

| Key | Function |
|---|---|
| `q` | Quit the application |
| `?` | Display help overlay |
| `z` | Toggle Zen Mode |
| `P` | Toggle Pro Mode |
| `s` | Change process sorting |
| `j` / `k` | Navigate process list |
| `↑` / `↓` | Navigate process list |
| `1`–`9` | Select process row |
| `l` | Lock selected process ID |
| `u` | Unlock process ID |
| `r` | Force refresh |
| `+` | Increase refresh speed |
| `-` | Decrease refresh speed |
| `Tab` | Change focus in Zen Mode |

## 11. System Monitoring and Data Sources

SysWatch uses Linux system interfaces to retrieve information about system performance.

| Monitoring Component | Data Source |
|---|---|
| CPU Utilization | `/proc/stat` |
| CPU Temperature | `/sys/class/thermal/` |
| CPU Frequency | `/sys/devices/system/cpu/` |
| Memory Usage | `/proc/meminfo` |
| Network Traffic | `/proc/net/dev` |
| Disk Space | `statvfs()` |
| Disk I/O | `/sys/block/` |
| NVIDIA GPU | `nvidia-smi` |
| AMD/Intel GPU | `/sys/class/drm/` and hwmon |
| Network Ports | `/proc/net/tcp` and `/proc/net/tcp6` |
| System Services | `systemctl` |
| Process Information | `/proc/` process entries |

Some metrics are calculated by comparing successive readings rather than reading a single instantaneous value. This is particularly relevant to CPU utilization and disk/network throughput.

## 12. Troubleshooting

### CMake Configuration Error

If the build directory contains an outdated CMake cache, remove it and configure the project again:

```bash
rm -rf build

cmake -S . -B build
```

### ncurses Dependency Missing

Install the development library:

```bash
sudo apt install libncurses-dev
```

### Permission Issues

Some hardware and system-level information may require additional permissions. Run the application using your normal user account first and grant additional permissions only when necessary.

### GPU Information Unavailable

GPU monitoring depends on hardware support and installed drivers. For NVIDIA devices, verify that `nvidia-smi` works:

```bash
nvidia-smi
```

## 13. Future Improvements

Potential improvements to SysWatch include:

- Additional hardware monitoring support.
- Improved historical performance analysis.
- More detailed process-level statistics.
- Configurable dashboard layouts.
- Additional Linux distribution compatibility.
- Improved performance and resource efficiency.

## 14. License

This project includes an MIT License. Refer to the `LICENSE` file in the repository for the complete license terms.

---

**SysWatch – A Modular Linux Resource Monitor Using Direct `/proc` Filesystem Sampling**

Built with C++20 for Linux system monitoring.