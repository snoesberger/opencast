Firewall
========

Opencast relies on a lot of network communication and although not strictly necessary,
it usually makes sense to configure a firewall for additional protection

This describes a lot of the communication happening between servers in the most common use cases.
In certain set-ups and with certain types of integrations, these may deviate slightly.

General rules are:

- Users communicate with Opencast via HTTP(S)
- Capture agents communicate with Opencast via HTTP(S)
- Opencast nodes communicate among each other via HTTP(S)
- Often OpenSearch runs on the admin node since this node communicates with these services exclusively
- All servers should get access to the storage infrastructure
- All Opencast nodes need database access

A visual representation of the communication within a three-node cluster will look like this:

```mermaid
graph LR

  subgraph Internet
    user(User)
  end

  subgraph Opencast
    direction LR
    oc1(Opencast Admin)
    oc2(Opencast Worker)
    oc3(Opencast Presentation)
  end

  subgraph Data
    db(Database)
    os(OpenSearch)
    storage(Storage)
  end

  subgraph Recorder
    ca(Capture Agent)
  end

  user -->|80, 443| oc1
  user -->|80, 443| oc3
  oc1 <-->|80, 443| oc2
  oc2 <-->|80, 443| oc3
  oc3 <-->|80, 443| oc1
  oc1 -->|e.g. 3306| db
  oc2 -->|e.g. 3306| db
  oc3 -->|e.g. 3306| db
  oc1 -->|9200| os
  oc3 -->|9200| os
  oc1 --- storage
  oc2 --- storage
  oc3 --- storage
  ca -->|80, 443| oc1
```

Notes:

- The numbers in the diagram describe TCP ports
- If you use a database other than MariaDB, the port may differ


Suggested Firewall Configurations
---------------------------------

Note that none of these instructions take additional services like SSH into account.
They are focused just on what Opencast needs for communication.


### Simple

For a very simple configuration catching most of the important attack vectors, implement the following firewall rules:

1. Allow HTTP and HTTPS to all Opencast nodes from the outside
2. Allow all TCP communication within the cluster


### Complex

If you want a more complex, stricter set of rules:

1. Allow external HTTP and HTTPS communication to admin, presentation and possibly ingest
2. Allow all Opencast nodes to access the database
3. Allow the admin and presentation nodes to access OpenSearch
4. Allow all nodes access to the storage infrastructure
