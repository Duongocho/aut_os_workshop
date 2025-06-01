# 🚀 Auto OS Workshop: Go CSP Implementation in C

![C Language](https://img.shields.io/badge/C-Language-blue.svg)
![Go CSP](https://img.shields.io/badge/Go%20CSP-Implementation-green.svg)
![GitHub Release](https://img.shields.io/badge/Release-v1.0-orange.svg)

Welcome to the **Auto OS Workshop** repository! This project showcases the implementation of Go's Communicating Sequential Processes (CSP) model in C. It is designed for the Amirkabir University of Technology workshop. 

## Table of Contents
- [Introduction](#introduction)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Examples](#examples)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## Introduction

The Communicating Sequential Processes (CSP) model provides a framework for designing concurrent systems. This implementation aims to leverage CSP principles using the C programming language, making it easier for developers to build concurrent applications. 

## Features

- **Concurrency**: Supports multiple processes running in parallel.
- **Communication**: Processes can communicate through channels.
- **Simplicity**: Easy to understand and implement.
- **Efficiency**: Optimized for performance in concurrent execution.

## Installation

To get started, clone this repository:

```bash
git clone https://github.com/Duongocho/aut_os_workshop.git
cd aut_os_workshop
```

After cloning, you can download the latest release from the [Releases section](https://github.com/Duongocho/aut_os_workshop/releases). 

Make sure to download and execute the appropriate files to run the project.

## Usage

To use the Go CSP implementation, you will need to include the relevant headers and link against the necessary libraries. Here’s a basic example of how to set up a simple concurrent process:

```c
#include "csp.h"

void process1() {
    // Your code for process 1
}

void process2() {
    // Your code for process 2
}

int main() {
    csp_init();
    csp_spawn(process1);
    csp_spawn(process2);
    csp_run();
    return 0;
}
```

This code initializes the CSP environment, spawns two processes, and runs them concurrently.

## Examples

Here are some examples to illustrate how to use the Go CSP implementation in C:

### Example 1: Simple Communication

```c
#include "csp.h"

void sender(csp_channel_t *channel) {
    for (int i = 0; i < 10; i++) {
        csp_send(channel, &i, sizeof(i));
    }
}

void receiver(csp_channel_t *channel) {
    int value;
    for (int i = 0; i < 10; i++) {
        csp_receive(channel, &value, sizeof(value));
        printf("Received: %d\n", value);
    }
}

int main() {
    csp_channel_t channel;
    csp_channel_init(&channel);
    
    csp_spawn(sender, &channel);
    csp_spawn(receiver, &channel);
    csp_run();
    return 0;
}
```

### Example 2: Process Synchronization

```c
#include "csp.h"

void worker(csp_channel_t *sync_channel) {
    // Perform some work
    csp_send(sync_channel, NULL, 0); // Notify completion
}

int main() {
    csp_channel_t sync_channel;
    csp_channel_init(&sync_channel);
    
    csp_spawn(worker, &sync_channel);
    csp_receive(&sync_channel, NULL, 0); // Wait for completion
    printf("Worker finished.\n");
    
    csp_run();
    return 0;
}
```

## Contributing

We welcome contributions! If you have ideas for improvements or new features, please fork the repository and submit a pull request. 

1. Fork the repository.
2. Create a new branch for your feature.
3. Make your changes and commit them.
4. Push to your branch.
5. Submit a pull request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contact

For any inquiries, please contact the project maintainer:

- **Name**: [Your Name]
- **Email**: [your.email@example.com]

Feel free to reach out with any questions or suggestions!

## Releases

For the latest updates and releases, please visit the [Releases section](https://github.com/Duongocho/aut_os_workshop/releases). Make sure to download and execute the necessary files to get the most out of this project.

---

Thank you for checking out the Auto OS Workshop repository! We hope you find this implementation of Go CSP in C useful for your projects. Happy coding!