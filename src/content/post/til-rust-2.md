---
title: "TIL RUST #2"
description: "Running the main source file of a package and other files in src/bin"
publishDate: "2025-11-08"
tags: ["rust", "til", "cargo", "learning"]
coverImage:
  src: "https://pbs.twimg.com/media/G5N5RpMaEAAoMXv?format=jpg&name=medium"
  alt: "TIL RUST #2 Image"
---

# Running the main source file of a package and other files in src/bin

You should be somewhere inside your package's directory, which contains the Cargo.toml file, in order to run the package with Cargo. You do not need to be in the root itself; any subdirectory will work.

The same applies even to other source files (in src/bin), but a flag (--bin) must be used in conjunction with the regular cargo run command.

![Image](https://pbs.twimg.com/media/G5N5RpMaEAAoMXv?format=jpg&name=medium)
