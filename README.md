# IP Address Analysis Toolkit

A comprehensive suite of Python utilities for network analysis, IP address processing, and proxy management. This toolkit provides professional-grade tools for network administrators, security professionals, and developers working with IP networks and proxy services.

## Table of Contents

- [Project Overview](#project-overview)
- [Components](#components)
  - [IP Address Analyzer](#1-ip-address-analyzer)
  - [Proxy Scanner Application](#2-proxy-scanner-application)
- [Installation and Requirements](#installation-and-requirements)
- [Usage Instructions](#usage-instructions)
- [Technical Specifications](#technical-specifications)
- [Architecture and Design](#architecture-and-design)
- [API Reference](#api-reference)
- [License](#license)

## Project Overview

This repository contains two main components: a batch IP address analysis tool and a graphical proxy scanner application. Both tools are designed for network analysis and security testing purposes, providing both command-line and graphical user interfaces for different use cases.

## Components

### 1. IP Address Analyzer

**File:** `ip_address_checker.py`

A comprehensive IP address analysis library that processes IP addresses from input files and provides detailed network information.

#### Core Functions

- **IP Validation** (`is_valid_ip_address`): Validates IP address format and octet ranges according to RFC standards
- **Binary Conversion** (`bin_ip_address`): Converts decimal IP addresses to 8-bit binary representation with proper padding
- **Class Identification** (`class_ip_address`): Determines IP address class (A, B, C, D, E) based on first octet values
- **Private/Public Classification** (`private_ip_address`): Identifies private IP addresses (RFC 1918) vs public addresses
- **Subnet Mask Calculation** (`default_mask`): Provides default subnet masks based on IP class
- **Binary Mask Generation** (`bin_default_mask`): Converts subnet masks to binary format
- **Network ID Extraction** (`net_id`): Calculates network identifier using bitwise AND operations
- **Network/Host Template** (`net_id_host_id`): Generates visual template showing network (N) and host (H) portions

#### Supported IP Ranges

- **Class A**: 1.0.0.0 - 126.255.255.255
- **Class B**: 128.0.0.0 - 191.255.255.255  
- **Class C**: 192.0.0.0 - 223.255.255.255
- **Class D** (Multicast): 224.0.0.0 - 239.255.255.255
- **Class E** (Experimental): 240.0.0.0 - 255.255.255.255

#### Private Address Ranges

- 10.0.0.0/8 (10.0.0.0 - 10.255.255.255)
- 172.16.0.0/12 (172.16.0.0 - 172.31.255.255)
- 192.168.0.0/16 (192.168.0.0 - 192.168.255.255)

### 2. Proxy Scanner Application

**Files:** `scan_proxy_ip.py`, `data.py`

A multi-threaded graphical application for scanning and validating proxy servers from multiple public sources.

#### Features

- **Multi-Source Aggregation**: Collects proxies from 50+ public repositories and lists
- **Protocol Support**: HTTP, HTTPS, SOCKS4, and SOCKS5 proxy validation
- **Multi-Threaded Verification**: Concurrent proxy testing with configurable worker threads
- **Real-Time Results**: Live updating interface with progress reporting
- **Customizable Parameters**: Adjustable timeout settings and target URLs
- **FreeProxy Integration**: Additional proxy discovery using the FreeProxy library

#### Proxy Sources

The application aggregates proxies from categorized sources:

- **General Proxies**: 10 sources including anonymous and mixed proxies
- **HTTP Proxies**: 30 specialized HTTP proxy sources
- **HTTPS Proxies**: 20 SSL-enabled proxy sources
- **SOCKS5 Proxies**: 30 SOCKS5 protocol sources
- **SOCKS4 Proxies**: 10 SOCKS4 protocol sources

## Installation and Requirements

### Prerequisites

- Python 3.8 or higher
- pip package manager

### Dependencies

```bash
# Core dependencies
pip install requests

# For proxy scanner only
pip install tkinter fake-useragent free-proxy

# Optional: for enhanced performance
pip install fp
```

### Installation Steps

1. **Clone the Repository**
   ```bash
   git clone https://github.com/yourusername/ip-analysis-toolkit.git
   cd ip-analysis-toolkit
   ```

2. **Set Up Virtual Environment** (Recommended)
   ```bash
   python -m venv venv
   source venv/bin/activate  # Linux/MacOS
   venv\Scripts\activate     # Windows
   ```

3. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   ```

## Usage Instructions

### IP Address Analyzer

**Command Line Usage:**
```bash
python ip_address_checker.py
```

The analyzer automatically processes IP addresses from `ip_address.txt` and outputs comprehensive analysis including:
- Binary representations
- IP class identification
- Private/public classification
- Default subnet masks
- Network ID calculations

**Input File Format:**
Create `ip_address.txt` with one IP address per line:
```
192.168.1.1
8.8.8.8
10.0.0.1
```

### Proxy Scanner Application

**Graphical Interface:**
```bash
python scan_proxy_ip.py
```

**Application Workflow:**
1. Launch the application
2. Configure timeout parameters (default: 2-5 seconds)
3. Set target URL for validation (default: www.youtube.com)
4. Click "Start Proxy Check" to begin scanning
5. Monitor real-time progress in the output window

**Configuration Options:**
- **Minimum Timeout**: Lower bound for connection attempts (seconds)
- **Maximum Timeout**: Upper bound for connection attempts (seconds)  
- **Validation URL**: Target for proxy connectivity testing

## Technical Specifications

### IP Address Validation

- **Format Compliance**: RFC 791 standards
- **Octet Validation**: 0-255 range per octet
- **Length Validation**: 7-15 character length constraints
- **Structure Enforcement**: Exactly 4 octets separated by periods

### Binary Conversion

- **8-bit Padding**: Ensures consistent 8-character binary representation
- **Dot Separation**: Maintains IP address structure in binary format
- **Error Handling**: Comprehensive exception management for invalid inputs

### Proxy Validation

- **Concurrent Processing**: Up to 20 simultaneous verification threads
- **Protocol Compliance**: Proper header and proxy configuration for each protocol type
- **Source Redundancy**: Multiple fallback sources for reliability
- **Performance Optimization**: Configurable worker threads and timeouts

## Architecture and Design

### IP Analyzer Architecture

```
Input File → IP Validation → Classification → Analysis → Output
    ↓           ↓              ↓              ↓         ↓
 ip_address.txt → Format Check → Class Detection → Multiple Analyses → Console Report
```

### Proxy Scanner Architecture

```
Multiple Sources → Aggregation → Multi-threaded Validation → Results Display
      ↓               ↓                  ↓                     ↓
 50+ URL Lists → Proxy Collection → Concurrent Testing → GUI Presentation
```

### Key Design Patterns

- **Factory Pattern**: Proxy source management and protocol handling
- **Strategy Pattern**: Multiple validation methods for different proxy types
- **Observer Pattern**: Real-time GUI updates during scanning process
- **Thread Pool Pattern**: Efficient resource management for concurrent operations

## API Reference

### IP Address Analyzer Functions

```python
def is_valid_ip_address(ip_address: str) -> bool:
    """
    Validate IP address format and structure.
    
    Args:
        ip_address: String representation of IP address
        
    Returns:
        Boolean indicating validity
    """

def bin_ip_address(ip_address: str) -> str:
    """
    Convert IP address to binary representation.
    
    Args:
        ip_address: Valid IP address string
        
    Returns:
        8-bit binary representation with dot separation
    """

def class_ip_address(ip_address: str) -> str:
    """
    Determine IP address class.
    
    Args:
        ip_address: Valid IP address string
        
    Returns:
        Single character representing class (A, B, C, D, E)
    """
```

### Proxy Scanner Functions

```python
def proxy_sources(proxy_urls: list) -> list:
    """
    Aggregate and validate proxies from multiple sources.
    
    Args:
        proxy_urls: List of source URLs
        
    Returns:
        List of validated working proxies
    """

def check_single_proxy(proxy_url: str, test_url: str, timeout: int) -> str:
    """
    Validate individual proxy server.
    
    Args:
        proxy_url: Proxy server address
        test_url: Target for connectivity test
        timeout: Connection timeout in seconds
        
    Returns:
        Working proxy URL or None
    """
```

## License

This project is licensed under the MIT License. See the `LICENSE.md` file for complete terms and conditions.

**Copyright Notice:**  
Copyright (c) 2025 WARATECS. Permission is granted for free use, modification, and distribution with appropriate attribution.

## Disclaimer

This toolkit is intended for legitimate network analysis, security testing, and educational purposes only. Users are responsible for complying with all applicable laws and terms of service when using these tools. The developers assume no liability for misuse or damages resulting from the use of this software.

**Important Notes:**
- Always obtain proper authorization before scanning networks
- Respect rate limits and terms of service for proxy sources
- Use private IP ranges only in appropriate environments
- Ensure compliance with local regulations regarding network scanning
