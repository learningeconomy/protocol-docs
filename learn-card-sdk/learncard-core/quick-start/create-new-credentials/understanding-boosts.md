# Understanding Boosts

### What is a Boost?

A Boost is LearnCard's enhanced version of a standard Verifiable Credential (VC). It extends the Open Badges v3 and W3C Verifiable Credentials standards by adding useful features for credential display, management, and governance while maintaining full compatibility with standard credential verifiers.

Think of a Boost as a "VC+" - all the standard credential fields you expect, plus additional capabilities that make credentials more useful and manageable in real-world applications.

### Why Use Boosts?

Boosts solve several common challenges when working with credentials:

1. **Display Control**: Customize how credentials appear in wallets and viewers
2. **Governance**: Define and enforce rules about who can issue what credentials
3. **Network Validation**: Get network-level verification that a credential was issued following proper procedures
4. **Attachments**: Include additional files and resources with credentials

### Types of Boosts

#### Basic Boost

The simplest form of a boost adds display options to a standard credential:

```javascript
{
  type: ["VerifiableCredential", "OpenBadgeCredential", "BoostCredential"],
  // Standard VC fields...
  display: {
    backgroundColor: "#353E64",
    backgroundImage: "https://example.com/background.jpg",
    displayType: "badge" // or "certificate"
  }
}
```

#### ID Boost

Special type for creating digital IDs with custom styling:

```javascript
{
  type: ["VerifiableCredential", "OpenBadgeCredential", "BoostCredential", "BoostID"],
  // ... standard fields
  boostID: {
    IDIssuerName: "Organization Name",
    accentColor: "#FF0000",
    backgroundImage: "https://example.com/id-background.jpg",
    dimBackgroundImage: true,
    fontColor: "#FFFFFF",
    issuerThumbnail: "https://example.com/logo.png",
    showIssuerThumbnail: true
  }
}
```

### Network Certification

When a Boost is issued through the LearnCard Network, it gets wrapped in a CertifiedBoostCredential:

```javascript
{
  type: ["VerifiableCredential", "CertifiedBoostCredential"],
  issuer: "did:web:network.learncard.com",
  boostCredential: {
    // Your original boost here
  },
  boostId: "lc:network:example.com/boost:123"
}
```

This wrapper:

* Validates the issuer's authority to send the boost
* Provides a unique network identifier
* Adds a network-level signature
* Maintains the original peer-to-peer signatures

### Common Fields Reference

#### Display Options

```javascript
display: {
  backgroundColor: string,    // CSS color
  backgroundImage: string,    // URL
  displayType: "badge" | "certificate"
}
```

#### Attachments

```javascript
attachments: [{
  title: string,            // Attachment name
  type: string,            // MIME type
  url: string              // Resource URL
}]
```

### Tips for Developers

1. **Start Simple**: Begin with a basic boost and add features as needed
2. **Use Display Types**:
   * `badge` for compact achievements
   * `certificate` for formal credentials
3. **Network Integration**:
   * Test boost structures locally first
   * Validate all required fields before network submission
   * Handle both the original boost and certified wrapper in your application
4. **Verification**:
   * Boosts remain standard VCs - use any VC verifier
   * Access network-specific features through LearnCard APIs
   * Check both boost and network signatures when full verification is needed

Remember: Every boost is a valid VC, but not every VC is a boost. The extra features are optional and can be added incrementally as your application's needs grow.
