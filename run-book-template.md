# Run Book / System Operation Manual

## Service or system overview

**Service or system name:** 

### Business overview

> What business need is met by this service or system? What expectations do we have about availability and performance?

_(e.g. Provides reliable automated reconciliation of logistics transactions from the previous 24 hours)_

### Technical overview

> What kind of system is this? Web-connected order processing? Back-end batch system? Internal HTTP-based API? ETL control system?

_(e.g. Internal API for order reconciliation based on Ruby and RabbitMQ, deployed in Docker containers on Kubernetes)_

### Service owner

> Which team owns and runs this service or system?

_(e.g. The *Sneaky Sharks* team (Bangalore) develops and runs this service: sneaky.sharks@company.com / *#sneaky-sharks* on Slack / Extension 9265)_

### Contributing applications, daemons, services, middleware

> Which distinct software applications, daemons, services, etc. make up the service or system? What external dependencies does it have?

_(e.g. Ruby app + RabbitMQ for source messages + PostgreSQL for reconciled transactions)_

## Security and access control

### Password and PII security

> What kind of security is in place for passwords and Personally Identifiable Information (PII)? Are the passwords hashed with a strong hash function and salted?

_(e.g. Passwords are hashed with a 10-character salt and SHA265)_

## System configuration

### Configuration management

> How is configuration managed for the system?

_(e.g. CloudInit bootstraps the installation of Puppet - Puppet then drives all system and application level configuration except for the XYZ service which is configured via `App.config` files in Subversion)_

### Secrets management

> How are configuration secrets managed?

_(e.g. Secrets are managed with Hashicorp Vault with 3 shards for the master key)_

## System backup and restore

### Backup requirements

> Which parts of the system need to be backed up?

_(e.g. Only the CoreTransactions database in PostgreSQL and the Puppet master database need to be backed up)_

### Backup procedures

> How does backup happen? Is service affected? Should the system be [partially] shut down first?

_(e.g. Backup happens from the read replica - live service is not affected)_

### Restore procedures

> How does restore happen? Is service affected? Should the system be [partially] shut down first?

_(e.g. The Booking service must be switched off before Restore happens otherwise transactions will be lost)_

## Monitoring and alerting

### Metrics

> What significant metrics will be generated?

_(e.g. Usual VM stats (CPU, disk, threads, etc.) + around 200 application technical metrics + around 400 user-level metrics)_

### Health checks

> How is the health of dependencies (components and systems) assessed? How does the system report its own health?

## Operational tasks

### Deployment

> How is the software deployed? How does roll-back happen?

_(e.g. We use GoCD to coordinate deployments, triggering a Chef run pulling RPMs from the internal yum repo)_

### Troubleshooting

> How should troubleshooting happen? What tools are available?

_(e.g. Use a combination of the `/health` endpoint checks and the `abc-*.sh` scripts for diagnosing typical problems)_

