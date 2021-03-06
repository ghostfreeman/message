# Client / Server #

Message uses [XMPP][xmpp-core] to transport [Avro][avro-spec] data.
![Message Communication](static/diagram-client-server.png)


## Getting Started ##

You can watch a Message stream and send commands with the demo-client
to see how XMPP streams are structured.

First, run the server in verbose mode:

    :::sh
    ./bin/run -v

In another shell, activate the Message virtualenv and send commands
with the demo-client:

    :::sh
    source mdev/bin/activate
    ./db/examples/demo-client.py get-item '/'

As you send commands, you will see output like this in your server
shell:

    :::sh
    READ: '<iq type="get" id="UNIQUE-ID">...</iq>'
    REQUEST (get/UNIQUE-ID) 'COMMAND'
    RESULT (get/UNIQUE-ID) 'RESPONSE'
    WROTE: '<iq type="result" id="UNIQUE-ID">...</iq>'

The `READ` and `WROTE` lines are the XMPP stanzas received by the
server and sent in response.  The `REQUEST` line shows the `COMMAND`
decoded from the incoming stanza; `RESULT` shows the `RESPONSE` about
to be encoded and sent to the client after handling the `COMMAND`.
The `UNIQUE-ID` associates the four lines with each other.  This is
useful when the server is handling multiple requests at once.


## XMPP Clients ##

Using XMPP has a number of advantages.

  + **Security and Authentication**:
    XMPP supports TLS for stream security and extensible
    authentication mechanisms through SASL.

  + **Real-time, Bi-Directional**:
    By design, XMPP streams are persistent, real-time, and
    bi-directional.  Server-initited notifications are an important
    feature for Message.

  + **Available Client Libraries**:
    Since client libraries already exist for many programming
    languages, developers can quickly focus on issues specific to
    their framework.

  + **Works on the Web**:
    Web-based clients can connect directly to Message through BOSH.

### Connecting ###

### IQ Stanzas ###

### Send Commands ###

### Process Responses ###


## Avro Documents ##

Avro is a data serialization system that supports schema-based binary
or JSON representation.  Since it's designed with the expectation that
schema will change over time, it's ideal for Message.  The binary
representation allow it to be stored efficiently and JSON makes it
web-friendly.

### JSON Data ###

### Schema ###

### Binary Data ###

[xmpp-core]: http://xmpp.org/rfcs/rfc3920.html "XMPP: Core"
[avro-spec]: http://hadoop.apache.org/avro/docs/current/spec.html "Avro Specification"
