---
layout: default
title: Other References
permalink: /other/
---
# Addenda to the main paper

I sometimes run into other related references that would be useful if I ever update
[the paper](index.html). I don't want to forget that these are pertinent, but I
also don't want to try to merge uncleanly back into the paper. So I'll keep
them off to the side, on this page.

* In Apr 2021, the [Ruby language XML parser was
  updated](https://www.ruby-lang.org/en/news/2021/04/05/xml-round-trip-vulnerability-in-rexml-cve-2021-28965/)
  due to XML-specific round-trip vulnerabilities, which could cause
  applications using XML to perform insecure actions depending on the
  application context. This is analogous to the Mattermost issue mentioned
  below, but for Ruby language instead of Go language.
* Likewise in April 2021, the popular Wordpress Web content management system
  was found to be vulnerable to XML External Entity attack when running on PHP
  8 language, because PHP 8 added support for reading information about media
  files. Some media files support XML-based metadata, but PHP 8 did not read
  this XML information with safe parser settings, [leading to information about
  the Wordpress server being sent to an
  attacker](https://github.com/WordPress/wordpress-develop/security/advisories/GHSA-rv47-pc52-qrhh).
* In Dec 2020, [Mattermost posted about security vulnerabilities in SAML
  implementations across the modern Go
  ecosystem](https://mattermost.com/blog/coordinated-disclosure-go-xml-vulnerabilities/),
  due to the difficulty in parsing XML in a way that meets the security needs
  of SAML. As they put it:

  > The core issue is the same in all three [vulnerabilities]: maliciously
  > crafted XML markup mutates during round-trips through Go’s decoder and
  > encoder implementations. ... There are applications that absolutely require
  > semantic integrity in XML in order to be secure — a major example being
  > SAML.

  * As a result of months of work that left Go users still unable to securely use
  XML from the Go standard library, the author of a Go implementation of SAML
  [had this to say](https://news.ycombinator.com/item?id=25424267):

    > People need to stop using SAML. ... for reasons which are irrelevant to
    > modern implementations, XML [Digital Signature] prefers to stuff the
    > signature metadata back inside the XML document that was just signed.
    > ... Obviously this is a crazy approach to one of the most
    > security-critical parts of an application on the internet, and it breaks
    > all the time. Unfortunately people persist in using this fundamentally
    > broken protocol, so huge thank you to the team at Mattermost for their
    > research in this area.

* WorkOS posted a [thorough description of security issues in SAML](https://workos.com/blog/fun-with-saml-sso-vulnerabilities-and-footguns),
  much better written than [my documents](index.html) and which includes
  coverage of at least 4 separate major SAML security vulnerabilities that have
  been released since I wrote my paper. I predicted that there would be
  vulnerabilities in SAML deployments, but this article provides a very good
  description about how and why these keep happening. WorkOS is a company that
  provides single sign-on as a service so getting things like SAML and OpenID
  Connect right is their bread-and-butter, so they have good insight as to why
  SAML is so hard to get right.
* [https://ws-attacks.org/](https://ws-attacks.org/) has an extensive (but
  high-level) listing of many security attacks on the various Web Service
  (WS-\*) standards. Many (though not all) involve XML, and many of those
  involve things peculiar to XML.
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
* [@n0nst1ck](https://twitter.com/n0nst1ck), a security researcher at Stripe,
  posted a [very good
  article](https://www.stackallocated.com/blog/2020/saml-idp-no-shared-keys/)
  on why a SAML identity provider should use multiple signing keys for each
  service provider using SAML tokens generated by the identitiy provider.
  Although the article is not specific to XML, and notes that its advice
  applies also to other authentication protocols, it does reference the same
  history of XML processing issues that my own paper mentioned.
