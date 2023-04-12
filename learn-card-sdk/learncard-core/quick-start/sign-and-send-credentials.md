# Sign & Send Credentials

### High-Level Overview

1. [**Install**](./#install-the-library) [learn-card-core package](./#install-the-library) from pnpm, yarn, or npm into your project.
2. [**Construct**](../construction/): create a new LearnCard [from a random seed](../construction/initlearncard.md#example-usage), with [imported key material](../construction/learncardfromseed.md), [connected to a VC-API](../plugins/official-plugins/vc-api.md), or [connected to a Web3 wallet](../../../learncard-services/metamask-snap.md).
3. [**Sign Credential**](./#issue-credentials): [construct a credential ](create-new-credentials.md)and issue the credential by signing it. Or, setup your own [LearnCard Bridge](../../learncard-bridge.md) to sign the credential with VC-API.
4. [**Send Credential**](../chapi/using-learncard-to-interact-with-a-chapi-wallet.md#storing-a-presentation-with-chapi): there are many ways to send a credential, but we primarily recommend [CHAPI](../chapi/cheat-sheets/issuers.md) at the moment.

The easiest way to start sending credentials, is to follow the docs for CHAPI:

{% content-ref url="../chapi/" %}
[chapi](../chapi/)
{% endcontent-ref %}
