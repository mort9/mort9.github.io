---
title: Mort9 Posts
author: Mortie Torabi 
---

# Fundamentals of Software Testing

## Basic Concepts and Definitions

- **Testability**: How easy can a software be tested?
  
  - **Operability**: The better if works the more efficiently it can be tested
    - *Bugs* add overhead of *analysis and reporting* to testing
    - Bugs might even *block execution of tests*
  - **Observability**: What you see is what you test
    - Distinct output is generated for each test
    - System state and variables should be visible during execution
    - *Incorrect output* is easily identified
    - Internal errors are detected through self-testing and automatically reported
    - source code is accessible
  - **Controllability**: The better we can control the software, the more testing can be automated and optimized
    - All possible *outputs* can be generated through some combination of inputs
    - All *code is executable* through some combination of input
    - *Software and hardware states* can be controlled directly by the test engineer
  - **Decomposability**: By controlling the scope of testing, we can more quickly isolate problems and perform smarter retesting
    - Software is built from *independent modules*
    - Modules can be *tested independently*
  - **Simplicity**: The less there is to test, the more quickly we can test it
    - **Functional Simplicity**: no extra features beyond requirements
    - **Structural Simplicity**: partition architecture to minimize the propagation of faults
    - **Code Simplicity**: A coding standard is followed for ease of inspection and maintenance
  - **Stability**: The fewer the changes, the fewer the disruption to testing
    - Charges to software are *infrequent* and controlled
    - Changes to software *do not invalidate existing tests*
  - **Understandability**: The more information we have, the smarter we will test
    - The *design* is well understood
    - *Dependencies* among components are well understood
  - Good technical *documentation*

### Model Based Testing

Is an application of model-based design for designing and optionally also executing artifacts to perform **software testing** or **system testing**. Models can be used to represent the desired behavior of a System Under Test (SUT), or to represent testing strategies and a test environment.

![image-20210214180739888](C:\Users\mortie\AppData\Roaming\Typora\typora-user-images\image-20210214180739888.png)
