# architecture-decomposition-apache_spark-aws_redshift-ec2-s3-SpringBoot
Solutions Design for a Document Processing System using AWS and Apache components. 

# Problem Statement
Decomposition / Solution Architecture Diagram

Our customers often seek our assistance in decomposing large-scale
systems into a set of specific components within a solution
architecture that is consistent with a stated set of requirements and
solution approach.

# System Context

The customer has requested a scalable solution for document
submission, persistence, metadata extraction, categorization, and
search.  The solution will be hosted in Amazon Web Services, and users
will interact with it using either new "nano-apps" developed for their
use, or by extending existing enterprise applications to directly use
microservices provided by the solution.

# Actors

*Document Providers*. Provide documents to the system.  Document
 providers number in the hundreds and are globally distributed.

*Extraction / Enrichment Team*.  Team focused on metadata extraction
 and enrichment for each provided document.  Uses a variety of tools
 and methods to extract metadata and keywords from, extract graphics
 and images from, classify, categorize, geolocate, summarize, and
 otherwise enrich provided documents.  This team continuously improves
 the metadata created from each document, pushing each successive
 release into production.  Once released, their methods are intended to
 run automatically over all new and previously provided documents.

*Document Consumers*.  Search for provided documents using extracted /
 enriched metadata to find potential documents of interest.  Request
 delivery of provided documents.

# Requirements

1. Ability for Document Providers to submit up to 1000 documents per
   hour, across all data providers.  Documents are heavy payload,
   averaging around 50 Gigabytes each.

2. Ability for Extraction / Enrichment team to upgrade extraction /
   enrichment methods on a weekly basis.

3. Ability for Document Consumers to search for provided documents
   using extracted / enriched metadata.  There are around 100,000
   Document Consumers distributed globally. who may undertake up to
   5,000 concurrent searches.

4. Ability to deliver Documents requested by Document Consumers.
   Document consumers request delivery of around 20,000 documents per
   day in aggregate.

5. Security is critical, but tackling would topple this exercise so we
   will keep it out of scope.


# Solution Approach

- Microservices layer atop underlying AWS services

- New "Nano-Applications", used by Document Providers and Document
  Consumers, consume microservices

- Existing Enterprise Applications consume microservices

- Consistent way for Extraction / Enrichment team to package and
  deploy releases of their methods
