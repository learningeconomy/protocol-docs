# LearnCard Bridge

**LearnCard Bridge** is a suite of tools with a simple CLI for deploying a serverless execution environment for LearnCard Core exposed over an HTTP API.&#x20;

The LearnCard Bridge implements the [**W3C CCG VC-API**](https://w3c-ccg.github.io/vc-api/) **specification.**&#x20;

{% hint style="success" %}
The **LearnCard SDK,** including **LearnCard Bridge**, **** is in early beta as we work toward full public release in Q4 2022.&#x20;

We are **currently accepting requests to join the early access cohort!** Please fill out [this short Typeform to request access,](https://r18y4ggjlxv.typeform.com/to/Ou8DYi4s) and we will follow-up with you as soon as possible to get you setup.&#x20;
{% endhint %}

### Quick Start&#x20;

To deploy your own LearnCard Bridge&#x20;

* Clone the [LearnBridge Repo](https://github.com/learningeconomy/LearnCard/tree/main/packages/learn-card-bridge-http)
* Set up [AWS CLI](https://aws.amazon.com/cli/)
* Add a .env file exporting a wallet seed (e.g. `WALLET_SEED=aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa`)
* Run `pnpm serverless-deploy`

### Connect a LearnCard Wallet

Once you have a deployed LearnCard Bridge VC-API, check out the [VC-API plugin](learncard-core/plugins/official-plugins/vc-api.md) for connecting it to your LearnCard agents:

{% content-ref url="learncard-core/plugins/official-plugins/vc-api.md" %}
[vc-api.md](learncard-core/plugins/official-plugins/vc-api.md)
{% endcontent-ref %}

LearnCard Bridge exposes a DID discovery endpoint at `/did`, so you do not need to specify the Issuer DID when instantiating a connected LearnCard agent.
