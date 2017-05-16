# Taleo Enterprise Edition (TEE)

## FAQ
*Why are there more candidates in TEE than in mySupply?*

Not all candidates will be uploaded. IF the candidate does not meet the requirements stated here they will not be found in mysupply. This can sometimes be a lrge percentage (think 50% not 5%) See the filters described later in this document.

*Why does a query in TEE not prodcue the same candidates as in myCandidates?*

In general we do not recommend conparing search results form TEE to search results in myCandidates. If you are trying to compare results please try to limit such searhcing to matching an email address for a candidate. The differences can be for several reasons. The primary differnce is that the filters applied in our search interface may not match those in TEE. Another reaosn is that the data in myCandidates reflects the most recent candidate and the client may have had newer data for a particuylar candidate form another source.

## Integration Overview
Taleo offers a set of APIs utelized by myCandidates known commonly as the "Bulk APIs" but technically referred to as the Integration Mangement Service.

The TEE integration works by sending a query to the taleo server. The server then builds a document consisting of all of the "entitites" that match the query. The integration then requests this document by pages, and then traverses the document page, creating a cnadidate form each row in the document. The candidate is then sent to the mysupply uplaod API.
- query is sent
- document is built
- document is retrieved a page at a time
- each row in the page is turned into a candidate
- the candidate is uploaded to mysupply

## Technical Detials
The endpoints used by the integration are:
- GetMessageByKey
- SubmitLargeDocument
- GetLargDocumentByKey

The Taleo equeries used are fairly complex but have the effect of only importing candidates:
- must have an attachment
- attachment must be marked as type RESUME, or have the word “resume” or “CV” in the title
 
Further, mysupply requires for all candidates:
- The document must be at least 100 characters long
- An email must either be on the candidate or successfully parsed from the resume
- Some resumes will fail to parse in which case the candidate is rejected.


## Needs for a New Fulfillment
In order to access the IMS APIs mysupply needs an account created with the following "rights":

- User type = Integration
- User permissions:
  - Allow this user to perform integration tasks
  - Allow batch export
  - Allow batch import
