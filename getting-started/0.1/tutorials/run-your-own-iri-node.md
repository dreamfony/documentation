# Run your own IRI node

**Nodes are the core of an IOTA network. Clients must send their transactions to nodes to have them validated and attached to the Tangle. Without nodes, IOTA networks wouldn't exist. No one would be able to send transactions because there would be no way of recording who sent what to whom.**

By running your own IRI node, you have the following benefits:
* You have your own direct access to a ledger on an IOTA network instead of having to connect to someone else's node
* You help the IOTA network to become more distributed by adding to the number of ledgers and validating other users' transactions

In this tutorial, you're going to run your own IRI node in a [Docker](https://www.docker.com/) container.

The IRI Docker container is suitable for the following operating systems:
* Linux
* MacOSX
* Windows

If you're using a Linux operating system, add `sudo` before all the commands in the following tasks.

## Prerequisites

To complete this tutorial, you need the following:

* Access to a command prompt
* An Internet connection

## Run an IRI node

1. [Install Docker](https://docs.docker.com/install/#supported-platforms). If you're running a version of Mac or Windows that's older than the system requirements, install the [Docker toolbox](https://docs.docker.com/toolbox/overview/) instead.

2. Make sure that Docker is installed

    ```bash
    docker run hello-world
    ```

    You should see some Docker information like the following:

    ```
    Unable to find image 'hello-world:latest' locally
    latest: Pulling from library/hello-world
    1b930d010525: Pull complete
    Digest: sha256:2557e3c07ed1e38f26e389462d03ed943586f744621577a99efb77324b0fe535
    Status: Downloaded newer image for hello-world:latest

    Hello from Docker!
    This message shows that your installation appears to be working correctly.

    To generate this message, Docker took the following steps:
    1. The Docker client contacted the Docker daemon.
    2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
        (amd64)
    3. The Docker daemon created a new container from that image which runs the
        executable that produces the output you are currently reading.
    4. The Docker daemon streamed that output to the Docker client, which sent it
        to your terminal.

    To try something more ambitious, you can run an Ubuntu container with:
    docker run -it ubuntu bash

    Share images, automate workflows, and more with a free Docker ID:
    https://hub.docker.com/

    For more examples and ideas, visit:
    https://docs.docker.com/get-started/
    ```

3. Download the pre-built Docker container

    ```bash
    docker pull iotaledger/iri:latest
    ```

4. Run the IRI

    ```bash
    docker run --name iri iotaledger/iri:latest --remote -p 14265
    ```
    
    Your IRI node is now running and you can interact with it through the [IRI API](root://node-software/0.1/iri/references/api-reference.md) at the following URL:
    http://localhost.com:14265

5. Use cURL to send a request to the [`getNodeInfo` endpoint](root://node-software/0.1/iri/references/api-reference.md#getNodeInfo)
    ```bash
    curl http://localhost:14265 -X POST -H 'Content-Type: application/json' -H 'X-IOTA-API-Version: 1' -d '{"command": "getNodeInfo"}'
    ```

    You should see something like the following in the output:
    ```json
    {
    "appName": "IRI",
    "appVersion": "1.7.0-RELEASE",
    "jreAvailableProcessors": 8,
    "jreFreeMemory": 2115085674,
    "jreVersion": "1.8.0_191",
    "jreMaxMemory": 20997734400,
    "jreTotalMemory": 4860129502,
    "latestMilestone": "CUOENIPTRCNECMVOXSWKOONGZJICAPH9FIG9F9KYXF9VYXFUKTNDCCLLWRZNUHZIGLJZFWPOVCIZA9999",
    "latestMilestoneIndex": 1050373,
    "latestSolidSubtangleMilestone": "CUOENIPTRCNECMVOXSWKOONGZJICAPH9FIG9F9KYXF9VYXFUKTNDCCLLWRZNUHZIGLJZFWPOVCIZA9999",
    "latestSolidSubtangleMilestoneIndex": 1050373,
    "milestoneStartIndex": -1,
    "lastSnapshottedMilestoneIndex": 1039138,
    "neighbors":0,
    "packetsQueueSize":0,
    "time":1548407444641,
    "tips":0,
    "transactionsToRequest":0,
    "features":["snapshotPruning","dnsRefresher","tipSolidification"],
    "coordinatorAddress": "EQSAUZXULTTYZCLNJNTXQTQHOMOFZERHTCGTXOLTVAHKSA9OGAZDEKECURBRIXIJWNPFCQIOVFVVXJVD9",
    "duration": 0
    }
    ```

You'll notice in the output that the value of the `neighbors` field is 0. This means that your node is not connected to an IOTA network. To do so, you need to connect to [neighbors](root://node-software/0.1/iri/concepts/neighbor-iri-node.md).

For help connecting to neighbors, go to the #help or #nodesharing channel on our [Discord](https://discord.iota.org).

## Next steps

[Read more in-depth guides about running a node](root://node-software/0.1/iri/introduction/overview.md).

[Send your first data transaction](../tutorials/send-a-zero-value-transaction-with-nodejs.md) to a node that's connected to the Devnet network.
