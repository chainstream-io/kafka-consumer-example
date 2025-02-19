# Kafka Streams Consumer Examples

This repository provides example implementations of Kafka Streams consumers in multiple programming languages, designed for high-performance message processing.

## Implementations

- [Go Implementation](./consumer.go)

## Prerequisites

### Authentication
Contact our support team to obtain the following credentials:
```
const username = "<YOUR USERNAME>"
const password = "<YOUR PASSWORD>"
const topic = "<TOPIC>"  // e.g. "tron.broadcasted.transactions"
```

### Security Certificates
Required SSL certificates for secure connection:
- [Client Key (PEM)](./client.key.pem)
- [Client Certificate (PEM)](./client.cer.pem)
- [Server Certificate (PEM)](./server.cer.pem)

## Configuration Guidelines

### Critical Settings

1. **Auto Commit Control**
```properties
enable.auto.commit: false
```
Disables automatic commits to prevent consumer lag on restart. Note: This may result in message loss between restarts.

2. **Offset Management**
```properties
auto.offset.reset: latest
```
Configures consumer to start from the most recent messages.

3. **SSL Security**
```properties
ssl.endpoint.identification.algorithm: none
```
Enables connection to self-signed certificates.

4. **Consumer Group Configuration**
```properties
group.id: ${username}-mygroup
```
Group ID must be prefixed with your username.

## Performance Considerations

### Latency Analysis

Common causes of message latency:

1. **Consumer-side Bottlenecks**
   - Network bandwidth limitations
   - CPU constraints
   - Resource contention

2. **Consumer Group Lag**
   - Message backlog requiring catch-up
   - Mitigated by `enable.auto.commit: false` setting

### Performance Optimization Guidelines

For optimal performance, consider:

1. **Production Environment Requirements**
   - Implement multi-threading for parallel processing
   - Choose high-performance languages (e.g., Rust, Java, Go) for critical implementations
   - Minimize console logging in production

2. **Message Timing Considerations**
   - Transaction timestamps reflect creation time, not broadcast time
   - Expected delay between transaction creation and node broadcast

## Language-Specific Setup

### Go Setup
1. Initialize module:
```bash
go mod init kafka-consumer
```

2. Install dependencies:
```bash
go get github.com/confluentinc/confluent-kafka-go/kafka
```

3. Run consumer:
```bash
go run consumer.go
```