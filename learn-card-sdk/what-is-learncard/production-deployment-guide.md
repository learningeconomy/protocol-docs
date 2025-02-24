---
description: Best practices for deploying LearnCard in production environments
---

# Production Deployment Guide

This guide provides comprehensive recommendations for deploying LearnCard SDK in production environments, with a focus on security, scalability, and maintainability.

## Key Management Best Practices

Proper key management is critical for production deployments of LearnCard. Your cryptographic keys are the foundation of your system's security.

### Seed Protection

Your seed phrase is the most sensitive piece of information in your LearnCard implementation. Never:
- Hard-code seeds in your application
- Store seeds in environment variables
- Commit seeds to source control
- Log seeds during application execution

Instead:
- Use a managed Key Management Service (KMS) like AWS KMS, Google Cloud KMS, or Azure Key Vault
- Implement proper access controls to your KMS
- Use Hardware Security Modules (HSMs) for highest security requirements
- Rotate keys periodically according to your security policies

```typescript
// Example using AWS KMS to retrieve a securely stored seed
import { KMS } from 'aws-sdk';
import { initLearnCard } from '@learncard/init';

async function getSecureSeed() {
  const kms = new KMS();
  const { Plaintext } = await kms.decrypt({
    CiphertextBlob: Buffer.from(process.env.ENCRYPTED_SEED, 'base64'),
    KeyId: process.env.KMS_KEY_ID
  }).promise();
  
  return Buffer.from(Plaintext).toString('hex');
}

async function initializeLearnCard() {
  const seed = await getSecureSeed();
  return initLearnCard({ seed });
}
```

## Architecture Patterns

### Serverless vs. Server-based Deployment

LearnCard can be deployed in various architectures:

**Serverless (AWS Lambda, Google Cloud Functions, etc.)**
- Pros: Auto-scaling, pay-per-use, lower operational overhead
- Cons: Cold starts impact performance, function duration limits
- Best for: Credential verification services, low-frequency issuing

**Server-based (Docker, Kubernetes, etc.)**
- Pros: Persistent connections, predictable performance, no cold starts
- Cons: Higher operational complexity, requires scaling management
- Best for: High-volume credential issuance, complex credential workflows

### Microservices Architecture

For large-scale applications, consider breaking down LearnCard functionality into dedicated microservices:

1. **Issuance Service**: Handles credential creation and signing
2. **Verification Service**: Validates credentials and presentations
3. **Storage Service**: Manages credential storage and retrieval
4. **DID Resolution Service**: Resolves DIDs and manages DID operations

This separation allows independent scaling and better resource allocation.

## Performance Optimization

### Caching Strategies

Implement caching for frequently accessed resources:

- **DID Document Caching**: Cache DID documents to reduce resolution time
- **Verification Results**: Cache verification results for frequently verified credentials
- **Template Caching**: Cache credential templates for rapid credential creation

Example Redis-based DID document caching:

```typescript
import { createClient } from 'redis';
import { initLearnCard } from '@learncard/init';

const redis = createClient();
await redis.connect();

const didPlugin = {
  name: 'cached-did-resolver',
  methods: {
    resolveDid: async (did) => {
      // Check cache first
      const cached = await redis.get(`did:${did}`);
      if (cached) return JSON.parse(cached);
      
      // If not in cache, resolve and store
      const didDocument = await originalResolveDid(did);
      await redis.set(`did:${did}`, JSON.stringify(didDocument), {
        EX: 3600 // Cache for 1 hour
      });
      
      return didDocument;
    }
  }
};

const learnCard = await initLearnCard({ 
  seed: process.env.SEED,
  plugins: [didPlugin]
});
```

### Connection Pooling

For database connections (if using external database storage):

- Use connection pooling to manage concurrent database access
- Configure appropriate pool sizes based on expected load
- Implement retry mechanisms for connection failures

## High Availability and Disaster Recovery

### Redundancy

- Deploy across multiple availability zones or regions
- Implement load balancing for server-based deployments
- Use managed database services with built-in replication

### Backup and Recovery

- Regularly backup critical data, including:
  - Credential indexes
  - DIDs and keys (securely)
  - Configuration data
- Test recovery procedures periodically
- Document recovery processes for operational staff

## Monitoring and Observability

### Key Metrics to Monitor

- Credential issuance rate and errors
- Verification success/failure rates
- Storage read/write operations
- API response times
- Error rates by endpoint/operation
- Resource utilization (CPU, memory, network)

### Logging Best Practices

- Use structured logging (JSON format) for easier parsing
- Include correlation IDs for tracking operations across services
- Log authentication and authorization events
- Never log sensitive information (keys, credentials, personal data)
- Implement log retention policies in compliance with regulations

Example logging configuration:

```typescript
import { initLearnCard } from '@learncard/init';
import { createLogger } from 'winston';

const logger = createLogger({
  level: 'info',
  format: combine(timestamp(), json()),
  defaultMeta: { service: 'learn-card-service' }
});

// Create a plugin that logs operations
const loggingPlugin = {
  name: 'operation-logger',
  methods: {
    issueCredential: async (credential, options, learnCard) => {
      const startTime = Date.now();
      try {
        const result = await learnCard.invoke.issueCredential(credential, options);
        logger.info('Credential issued', {
          operation: 'issueCredential',
          duration: Date.now() - startTime,
          credentialType: credential.type,
          success: true
        });
        return result;
      } catch (error) {
        logger.error('Credential issuance failed', {
          operation: 'issueCredential',
          duration: Date.now() - startTime,
          credentialType: credential.type,
          success: false,
          errorMessage: error.message
        });
        throw error;
      }
    }
  }
};
```

## Security Considerations

### Input Validation

Always validate inputs to your LearnCard API:
- Sanitize and validate all user-supplied data
- Implement schema validation for credential data
- Check for malformed DIDs and credential formats

### Rate Limiting

Implement rate limiting to prevent abuse:
- Limit credential issuance requests per API key/user
- Apply more restrictive limits for verification operations
- Use token bucket or similar algorithms for flexible rate limiting

### Audit Trails

Maintain comprehensive audit trails:
- Log all credential issuance with timestamps and issuer information
- Record verification attempts (successful and failed)
- Track access to stored credentials
- Ensure compliance with relevant regulations (GDPR, etc.)

## Upgrading and Versioning

### Semantic Versioning

Follow semantic versioning for your LearnCard implementation:
- MAJOR: Breaking changes to API
- MINOR: New features, non-breaking changes
- PATCH: Bug fixes and minor improvements

### Upgrade Strategy

- Test upgrades in staging environment before production
- Maintain comprehensive test suites to validate upgrades
- Document breaking changes and migration paths
- Consider running parallel systems during major upgrades

## Conclusion

A production-ready LearnCard deployment requires careful planning and implementation of security measures, performance optimizations, and operational practices. By following the guidelines in this document, you can build a robust, scalable, and secure credential management system using LearnCard SDK.

Remember that your specific requirements may vary based on your use case, regulatory environment, and organizational policies. Always adapt these recommendations to your particular context.