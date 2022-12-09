# Pass to Wallet
Resource: 

- [Building Your First Pass](https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/PassKit_PG/YourFirst.html#//apple_ref/doc/uid/TP40012195-CH2-SW1)
- [Node JS package for backend](https://www.npmjs.com/package/passkit-generator/v/2.0.8)

Design: 
- [Pass Design and Creation](https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/PassKit_PG/Creating.html#//apple_ref/doc/uid/TP40012195-CH4-SW1)


## Types of card/pass
- Boarding pass: transit systems such as train tickets, airline boarding passes, and other types of transit.
- Coupon: special offers, and other discounts.
- Event ticket: gain entry to an event like a concert, a movie, a play, or a sporting event.
- Generic: any pass that doesn’t fit into one of the other more specific styles for example, gym membership cards, coat-check claim tickets, and metro passes that carry a balance.
- Store card: loyalty cards, discount cards, points cards, and gift cards. 

Reference: https://tranzer.com/blogs/how-to-create-your-own-wallet-passes-pkpass/

## Creating pkpass

### 1)  Make a new directory in the Documents folder called <NAME>.pass. Using the .pass extension is a best practice, showing that the directory is a pass package.

### 2) Create the pass. Ensure that you have icon.png, icon@2x.png, thumbnail.png, thumbnail@2.png, **pass.json**

![Directory](https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/PassKit_PG/Art/directory_structure_2x.png)

### 3) Setting the Pass Type Identifier and Team ID

- In Certificates, Identifiers & Profiles, select Identifiers.
- Under Identifiers, select Pass Type IDs.
- Click the plus (+) button.
- Enter the description and pass type identifier, and click Submit.
- Select your registered pass identifier in list > Click on Create Certificate. (However, you need to generate Upload a Certificate Signing Request. (See 3.1)
- Download the cert

Find Team ID
- Double click the cert download which open up keychain
- Select the file (Pass Type ID: .....) > Get info
- Copy the Organisational Unit

- In your pass.json, ensure that it is correct:
```
{
    ...
    "passTypeIdentifier" : "your pass type identifier",
    "teamIdentifier" : "your Team ID",
    ...
}

```

##### 3.1) Certificate Signing Request

https://developer.apple.com/help/account/create-certificates/create-a-certificate-signing-request

- Launch Keychain Access located in /Applications/Utilities.
- Choose Keychain Access > Certificate Assistant > Request a Certificate from a Certificate Authority.
- In the Certificate Assistant dialog, enter an email address in the User Email Address field.
- In the Common Name field, enter a name for the key (for example, Gita Kumar Dev Key).
- Leave the CA Email Address field empty.
- Choose “Saved to disk,” then click Continue.


### 4) Generate the pkpass
1. Download this book’s companion file (from the developer downloads area), and locate the signpass project.
2. Open singpass
3. Click on project > Signing & Capabilities > Ensure that your team is selected.
4. Build the project
5. Dowload the build log file
6. Find the path ' /Users/sweekwang/Library/Developer/Xcode/DerivedData/signpass-gyuccukmgzupjidruwqhixskotty/Build/Products/Debug'
7. Copy the singpass to the `~/Documents` that contains your `.pass`
8. run `./signpass -p <name>.pass` to generate

Note:
- You can't add anything to the top half of the wallet, unless you are the card issuer (and have an agreement with Apple). For the bottom half, then there is an open API to create tickets, boarding passes, coupons, loyalty cards, etc. https://stackoverflow.com/questions/45708918/how-to-add-a-credit-debit-card-into-apple-wallet-from-the-ios-app.  which I believe is reserved for card issuers like banks and similar. apple-pay-provisioning@apple.com
