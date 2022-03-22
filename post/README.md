# Post MERMAID schemas

## Settings

Theme is **forest** in *Mermaid Configuration* section:

```json
{"theme":"forest"}
```

To obtain a PNG follow these steps:

1. Use the *Mermaid code* in the [Live Editor](https://mermaid-js.github.io/mermaid-live-editor).
2. Set the **forest** theme
3. Download the **SVG** image.
4. Open the file with **EDGE**.
5. Use the *Web capture* option to select the zone to keep as image.
6. Use Paint to save the clipboard to a **PNG** file.
7. Name the image file `FigureXX.png` where XX is the number with 0 padding on 2 positions.

:bulb: Point 3 to 6 can be replaced by a direct printscreen of the rendered schema if it fit a screen.

## Mermaid code for schemas

### Figure05

```mermaid
sequenceDiagram
    participant B as Blockchain
	participant I as Issuer
	participant H as Holder
    alt Verifiable credentials issuing
        H->>H: Generate RSA or EC key pair
        H->>I: Strong authentication of the Holder (MFA)
        H->>I: Provide Holder public key
        H->>I: Provide information needed to deliver the verifiable credentials
        I->>I: Verify the information of the Holder
		 I->>I: Generate verifiable credentials
        I->>I: Generate unique DID identifier and DID document
        Note right of I: DID document contain the Holder public key and Issuer public key
        Note right of I: DID document is signed with the Issuer private key
        Note right of I: DID document contain the signature of the verifiable credentials signed with the Issuer private key
        Note right of I: DID document is identified uniquely by the DID unique identifier
        I->>B: Store generated DID identifier and DID document
        Note right of I: DID document is not expected to contain sensitive private information, only proof cryptographic infos (signature)		
        I->>H: Return generated unique DID identifier and verifiable credentials
        H->>H: Store and link DID identifier and verifiable credentials with private key into the wallet
        Note right of H: A key pair is unique to a DID identifier and verifiable credentials
    end
```

### Figure06

```mermaid
sequenceDiagram
    participant B as Blockchain
	participant H as Holder
    participant V as Verifier
    alt Verifiable presentation validation
        H->>V: Provide a verifiable presentation of the verifiable credentials and DID identifier signed with the Holder private key
        H->>B: Search for the corresponding DID document based on the DID identifier provided
        V->>V: Verify the signature of the DID document using the Issuer public key contained into the DID document
        V->>V: Verify the signature of the verifiable presentation  provided using the Holder public key contained into the DID document
        V->>V: Verify the properties of the verifiable presentation related to the context of the Verifier
        V->>H: Grant access to the verifier system
    end
```

