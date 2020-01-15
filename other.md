---
layout: default
title: Other References
permalink: /other/
---

I sometimes run into other related references that would be useful if I ever update the
paper (so don't want to forget), but don't want to try to merge uncleanly back into
the paper. So I'll keep them off to the side, on this page.

* https://ws-attacks.org/ has an extensive (but high-level) listing of many
  security attacks on the various Web Service (WS-\*) standards. Many (though
  not all) involve XML, and many of those involve things peculiar to XML.
* Amazon Web Services's EC2 and S3 services [were attacked on their SOAP
  endpoints](https://www.nds.ruhr-uni-bochum.de/media/nds/veroeffentlichungen/2011/10/22/AmazonSignatureWrapping.pdf)
  in a 2011 paper by using XML ecosystem mis-features to forge valid signatures
  for SOAP-based requests. That may be one reason why SOAP support was removed
  just a few years later by AWS, even after the bug was fixed (and had to be
  fixed again). The paper notes that [XML Signature
  Wrapping](https://www.ws-attacks.org/XML_Signature_Wrapping) attacks were
  known since 2005, so the fact that a 'hyperscale' cloud provider's own
  services were made vulnerable to a well-known attack underscores how
  difficult it is to use XML (and the wider XML ecosystem) to underpin security
  guarantees.
    * In addition, AWS was employing XML schema validation (a common security
      improvement essential for use with XML)--the problem was the SOAP
      specification schema is over-broad, and more stringent schemas are not
      generically suitable for interoperability with other SOAP users.
* The XML-based WS-Security standard [was reviewed](https://eprint.iacr.org/2019/779.pdf) with a powerful
  symbolic model checker called Tamarin, detecting a previously-unknown flaw in
  the mutual authentication specific that was once used to protect SOAP
  requests. Although the flaw is not itself due to XML peculiarity, the paper
  notes almost as an afterthough that WS-Security has suffered "... a number of
  implementation flaws, *primarily due to the complexities of XML parsing and
  canonicalisation*" (emphasis mine).
