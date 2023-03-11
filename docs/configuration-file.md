---
layout: default
title: Configuration file
nav_order: 2
---

# Configuration file
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

---

## Configure File Integrity Monitor

To customize your installation and monitor custom folders, you may want to edit the config.yml file. Such file is pretty straightforward below you have an example configuration:

```
node: "FIM"
events:
  destination: both
  file: C:\ProgramData\fim\events.json
  max_file_checksum: 64
  endpoint:
    address: "https://10.0.0.227:9200"
    insecure: true
    credentials:
      user: "admin"
      password: "admin"

audit:
  # Only available in Linux with Audit daemon installed
  - path: /tmp/dir
    ignore: [".txt"]
    labels: ["audit"]

monitor:
  # Windows version
  - path: C:\tmp\test.txt
    ignore: [.log, .test]
    labels: ["tmp", "windows"]
  # Linux/Unix version
  - path: /tmp/dir
    ignore: [.txt]
    labels: ["tmp", "linux"]

log:
  file: fim.log
  level: info
```

We will describe each field and sub-field.

# Parameters
## node

String
{: .label }

Define the event producer's name.

This parameter will come on each event produced by the process.

---

- ## events

    Section
    {: .label .label-green }

    Handle event output parameters.

    - ### destination

    String
    {: .label }

    - ### file

    String
    {: .label }

    - ### endpoint

        Section
        {: .label .label-green }

        - #### address

        String
        {: .label }

        - #### insecure

        Boolean
        {: .label .label-purple }

        - #### credentials

            Section
            {: .label .label-green }

            - ##### user

            String
            {: .label }

            - ##### password

            String
            {: .label }

---

- ## audit

    Section
    {: .label .label-green }

    - ### path

        String
        {: .label }

        - #### ignore

        Array
        {: .label .label-yellow }
        String
        {: .label}

        - #### labels

        Array
        {: .label .label-yellow }
        String
        {: .label}

---

- ## monitor

    Section
    {: .label .label-green }

    - ### path

        String
        {: .label }

        - #### ignore

        Array
        {: .label .label-yellow }
        String
        {: .label}

        - #### labels

        Array
        {: .label .label-yellow }
        String
        {: .label}

---

- ## log

    Section
    {: .label .label-green }

    - ### file

    String
    {: .label }

    - ### level

    String
    {: .label }


- `node`, [String] to define host/app custom name.
- `events`, [Section] to handle file system events output.
  - `destination`, [String] that defines the destination of the events, options [file, network, both], default 'file'.
  - `file`, [Path/String] where the events will be stored.
  - `endpoint`, [Section] to define network parameters. 
    - `address`, [String] that defines the IP/DNS of indexer software [ElasticSearch/OpenSearch].
    - `insecure`, [Boolean] set the trust of HTTPS self signed certificates at the endpoint.
    - `credentials`, [Section] that defines the credentials to access to the endpoint. 
      - `user`, [String] that defines username of indexer software.
      - `password`, [String] that defines password of indexer software.
- `monitor`, [Section] that keeps a list of files/directories. Add as many lines as you require.
  - `path`, [Path/String] That defines the directory or file to monitor, it's recursive.
    - `ignore`, [List/Array] that allows you to ignore files that match the given string inside its name. Available formats Array or List.
    - `labels`, [Array] that allows to define custom labels on each event produced in the defined directory.
- `audit`, [Section] that keeps a list of files/directories. Add as many lines as you require. This section will use audit daemon engine with enhanced information.
  - `path`, [Path/String] That defines the directory or file to monitor, it's recursive.
    - `ignore`, [List/Array] that allows you to ignore files that match the given string inside its name. Available formats Array or List.
    - `labels`, [Array] that allows to define custom labels on each event produced in the defined directory.
- `log`, [Section] keeps configuration of software logging output
  - `file`, [Path/String] to the output logs.
  - `level`, [String] level of verbosity, currently supported [debug, info, error, warning].


{: .note }
> `ignore` formats:
> ```
>   - path: /tmp/dir
>     ignore: [.txt, .tmp]
> ```
> Or
> ```
>   - path: /tmp/dir
>     ignore:
>       - .txt
>       - .tmp
> ```

{: .note }
> `labels` formats:
> ```
>   - path: /tmp/dir
>     labels: ["temp", "linux"]
> ```
> Or
> ```
>   - path: /tmp/dir
>     labels:
>       - temp
>       - linux
> ```