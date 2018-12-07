#Verfiable Credentials Data-Model Explainer
***by Tzviya Siegman, Wiley with a great deal of cribbing from Manu Sporny, Digital Bazaar***

***NOTE***: "Verifiable Claims" are now known as "Verifiable Credentials".
The W3C Verifiable Claims Working Group's experience with using the term
"Verifiable Claims" demonstrated that it led to confusion in the marketplace.
The group has since found consensus in shifting to use the term
"Verifiable Credentials", which contain "Claims".

## Introduction
It is currently difficult to transmit credentials such as driver's licenses,
proofs of age, education qualifications, and healthcare data, via the
Internet in a way that is verifiable yet protects individual privacy.

Starting in 2013, the [W3C Credentials Community Group](https://w3c-ccg.github.io/) started to
work in earnest on solutions in this space followed shortly thereafter by the
[Rebooting Web of Trust Community](http://www.weboftrust.info/)
and W3C Verifiable Claims Working Group](https://www.w3.org/2017/vc/).
These groups, composed of 150+ individuals and organizations, are currently
focused on the creation, storage, transmission, and verification of digital
credentials via the Internet.

## Goals
The mission of the Verifiable Claims Working Group is to make expressing, exchanging, and verifying claims easier and more secure on the Web. The data-model outlines core data model concepts, such as claims, credentials, and presentations, that form the foundation of this specification. 

## Non-goals
The VCWG is not defining protocols or APIs. The model is identifier agnostic.

## Getting Started

The Verifiable Credentials ecosystem is composed of four primary roles:

* The ***Issuer***, who issues verifiable credentials about a specific
  ***Subject***.
* The ***Holder*** stores credentials on behalf of a ***Subject***.
  ***Holders*** are typically also the ***Subject*** of a credential.
* The ***Verifier*** requests a ***profile*** of the ***Subject***. A
  ***profile*** contains a specific set of credentials. The ***verifier***
  verifies that the credentials provided in the profile are fit-for-purpose.
* The ***Identifier Registry*** is a mechanism that is used to issue
  identifiers for ***Subjects***.

A visual depiction of the ecosystem above is shown below:

<a href="https://w3c.github.io/vc-data-model/">
  <img src="https://rawgithub.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2018/master/topics-and-advance-readings/verifiable-credentials-primer-diagrams/ecosystem.svg" width="100%" height="400">
</a>

### Claims, Credentials, and Profiles

The ecosystem roles exchange data that enables the realization of the previously
mentioned use cases. The data that is exchanged differs based on the roles
participating, but is fundamentally composed of Claims, Credentials, and
Profiles.

A claim is statement about a subject, expressed as a subject-property-value relationship:

<a href="https://w3c.github.io/vc-data-model/">
  <img src="https://rawgithub.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2018/master/topics-and-advance-readings/verifiable-credentials-primer-diagrams/claim-simple.svg" width="50%">
</a>

### Proofs
The cryptographic mechanism used to prove that the information in a verifiable credential or a verifiable presentation has not been tampered with is called a proof. There are many types of cryptographic proofs including, but not limited to, digital signatures, zero-knowledge proofs, proofs of work, and proofs of stake. In general, when verifying proofs implementations MUST ensure that:

* The proof is available in the form of a known proof suite.
* All required proof suite properties are present.
* The proof suite verification agorithm, when applied to the data, results in an acceptable proof.

The data model does not detail proof mechanisms. 

## Use Cases
The VCWG has created an [Use Case](https://w3c.github.io/vc-use-cases/) Document, including focal use cases that demonstrate complicated scenarios and the full encoding. 

Some simple use cases: 
* A student presents a government-issued identity to verify who she is when presenting herself for a standardized test
* An airline offers loyal customers upgrades to first-class via digital coupons. Coupons are issued as verifiable credentials.
* The Board of Physicians maintains its list of board-certified physicians in a credentials repository, enabling them to assert that a physician is certified or revoke certification as needed. This information can be verified as physicians apply for positions or by patients as they seek information about the doctors they are considering.

## Code Samples
What does a Verifiable Credential look like?

There are many pieces of information that MAY be included in a Verifiable Credential. There are numerous examples of credentials in the spec.

Here is an example of usage of the ID property in a credential, using the DID scheme:
```
{
  "@context": [
    "https://w3.org/2018/credentials/v1",
    "https://example.org/motorlicense/v1"
  ],
  "id": "http://dmv.example.gov/credentials/3732",
  "type": ["VerifiableCredential", "ProofOfAgeCredential"],
  "issuer": "https://dmv.example.gov/issuers/14",
  "issuanceDate": "2010-01-01T19:73:24Z",
  "claim": {
    "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
    "ageOver": 21
  },
  <span class="highlight">"credentialSchema": {
    "id": "https://example.org/motorlicense/proof-of-age.json",
    "type": "JsonSchemaValidator2018"
  }</span>,
  "proof": { ... }
}
```

## Tricky Design Choices
* JOSE vs JWT - see [Issue 93](https://github.com/w3c/vc-data-model/issues/93)
(what else should go here?)

## References and Acknowledgements
Thanks to Manu Sporny for writing most of this in previous formats. Much of the text came from [Motivation for Verifiable Claims Working Group Charter]http://w3c.github.io/webpayments-ig/VCTF/charter/charter-motivation.html, [Verifiable Claims Working Group Primer](http://w3c.github.io/webpayments-ig/VCTF/primer/), and [A Verifiable Credentials Primer](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/verifiable-credentials-primer.md).
