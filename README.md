# immutable-doc-stamp
Immutable Document Stamp is a method for improvement of tampering resistance / protection for a multi-page paper document with one-page signatures. 

The protected contents are placed between the "protection anchors"

```
---START-OF-PROTECTED-CONTENTS--- 
```

and 

```
---END-OF-PROTECTED-CONTENTS---
```

Then the text, including the anchors is copied into a serializer that turns it into plain text or markdown. When the doucment is simple / has no tables it is enough to simply copy-paste the text to be protected into the doc-stamp-generator notebook (referenced below).

After that a checksum is computed and a document footer text is returned including the protected contents length and a hash.

If any of the document pages are tampered / altered without change in the hash this will be easy to detect if one re-applies serialization and recomputes the signature - all the data needed for that is already on paper.

There is a jupyter notebook in this repository that helps getting through the footer generation process.
