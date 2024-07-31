---
created: 2024-07-31T12:57:33.361Z
updated: 2024-07-31T12:57:33.361Z
---
https://github.com/sequinstream/sequin

> Sequin is an open source message stream built on Postgres. It's like Kafka, but its Postgres foundation gives you more flexibility with less operational overhead.

> Sequin runs as a stateless Docker container in front of any Postgres database. It comes with a CLI, HTTP interface, and the ability to pull changes from any Postgres table into a stream.

> Sequin is a message stream, not just a queue. Like Kafka, Sequin persists messages according to a retention policy you specify. You can setup **consumers** to process a filtered subset of messages in the stream. Sequin delivers messages to consumers exactly once within a visibility timeout.

> With a stream instead of a queue, Sequin provides features like message replay and consumer rewind. Consumers can "join" the stream at any time and play through the history of messages. You can fan out to many individual services with exactly once delivery to each. Message history also helps with debugging and troubleshooting.

written in [[elixir]] and [[go]]