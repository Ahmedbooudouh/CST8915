# CST-8915 Lab4

## 1. CST-8915 Lab4 recording link: 
https://youtu.be/ioVPYHekj0M?si=DFMXqf7E9TsJgdWL

## 2. Reflection Questions

Image vs. Container

A Docker image is a read-only blueprint. A Docker container is a running instance created from that image. You can start many containers from the same image.

Layered architecture efficiency

Images are built from layers (one layer per change). Docker reuses unchanged layers across images and containers, so downloads and builds are faster and use less disk and network. If only one layer changes, Docker only rebuilds or pulls that layer.

Writable layer per container

Each container gets its own writable layer on top of the image so it can write logs, temp files, or config changes without modifying the base image. This keeps containers isolated: your changes in one container don't affect others that use the same image.

Why use Docker Compose

Docker Compose lets you define and run multi-container apps with one file and one command. It handles networks, volumes, dependencies, and scaling in a clear, repeatable way. This is simpler and less error-prone than starting each container by hand.