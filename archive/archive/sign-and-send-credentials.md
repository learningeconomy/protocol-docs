# Sign & Send Credentials

### High-Level Overview

1. [**Install**](broken-reference) [@learncard/init package](broken-reference) from pnpm, yarn, or npm into your project.
2. [**Construct**](../../sdks/learncard-core/construction.md): create a new LearnCard [from a random seed](broken-reference), with [imported key material](broken-reference), [connected to a VC-API](../../sdks/official-plugins/vc-api.md), or [connected to a Web3 wallet](broken-reference).
3. [**Sign Credential**](broken-reference): [construct a credential ](create-new-credentials.md)and issue the credential by signing it. Or, setup your own [LearnCard Bridge](learncard-bridge.md) to sign the credential with VC-API.
4. [**Send Credential**](../../how-to-guides/implement-flows/chapi/using-learncard-to-interact-with-a-chapi-wallet.md#storing-a-presentation-with-chapi): there are many ways to send a credential, but we primarily recommend [CHAPI](../../how-to-guides/implement-flows/chapi/cheat-sheets/issuers.md) at the moment.

The easiest way to start sending credentials, is to follow the docs for CHAPI:

{% content-ref url="../../how-to-guides/implement-flows/chapi/" %}
[chapi](../../how-to-guides/implement-flows/chapi/)
{% endcontent-ref %}
