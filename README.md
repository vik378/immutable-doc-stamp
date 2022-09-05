# immutable-doc-stamp
Immutable Document Stamp is a method for improvement of tampering resistance / protection for a multi-page paper document with one-page signatures. 

# Background

Even though there are electronic signatures out there paper print-and-sign documents still have legal value however do lack means for protection from tampering.

While signing a multi-page document, unless it is signed on every page - there is a risk of unapproved change to unsigned pages - when somebody prints a page that looks and feels the same but has slightly different contents and so makes it looked like you signed up for something that you actually have never seen before.

To reduce such risk / make such a tampering / forgery attack significantly more difficult one could add an electronic checksum on every single page of the to-be signed (printed-and-signed) document. The last page (with signatures) then may feature the same checksum + a QR code to facilitate checksum transfer for contents validation.

As documents sometimes feature a lot of formatting this method will work best with plain text or markdown serializations. The checksum stamp shall indicate what serialization method and checksum algorithm were used.

# How the method works

The protected contents are placed between the "protection anchors" in the original editor (word / gdocs / plain text / HTML).

```
---START-OF-PROTECTED-CONTENTS--- 
```

and 

```
---END-OF-PROTECTED-CONTENTS---
```

Then the text, including the anchors is copied into a serializer (for example the Jupyter notebook referenced below) that turns it into plain text or markdown. When the document has no complex formatting it is enough to simply copy-paste the plain text.

After that a checksum is computed and a document footer text is returned including the protected contents length and a hash.

The resulting footer text may look like the below:

```
Contents of this document are check-summed using method described in https://github.com/vik378/immutable-doc-stamp.
Protected text hash is 0fc514ece4eed3ca1a8fe4eba59b1764;
text serialization method is: plain-text; hashing algorithm: md5; length of serialized text: 630 characters
```

This text then should be copied back to the original text editor and inserted into its footer, so that it is shown on every protected page and the page with the signatures.

After that the document can be printed and signed. That may be followed by hash validation. The protected text may be independently OCR-ed from the printed / scanned document. Then the protected text could be extracted and placed back in the notebook. The footer compute process may then re-run and a difference in resulting hash may indicate tampering. One more thing to watch out is content length indicated in the signature - significant mismatch there may indicate that wrong serialization method is used for validation. For example, in plain-text copy-paste list decoration is stripped out so no numbers are pasted in front of the list items.

The [doc-stamp-generator.ipynb](doc-stamp-generator.ipynb) notebook is there to facilitate the footer generation and checking process. You may run it locally with Python 3 or [vscode](https://code.visualstudio.com/).