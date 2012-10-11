---
layout: default
title: Requirements and Expectations
permalink: RequirementsAndExpectations
category: Agile
description: How to differentiate between a requirement and an expectation.
summary: Software development activity comes from many different sources.  Some of these activities are necessary to deploy the system.  Some of them are not.  Additionally, users of the system and even people developing the system have expectations that may or may not match with these requirements.  This article discusses the difference between a requirement and an expectation.
---
## Sources of Development Effort

Software development activity comes from four sources:

* Requirements necessary to deploy a system
* Expectations of the user using the software
* Expectations of the development team itself
* Requirements that are not currently necessary to deploy a system

### Necessary Requirements

With any development effort,
there is a subset of requirements which are absolutely necessary
in order to deploy the system.  In a commercial sofware enterprise,
this means that if any of the requirements are not met, then the
software can not be sold.  In a custom or internal software development
effort, it means that if any of the requirements are not met, then
the system will not be deployed.

Determining the absolute minimum set of requirements necessary
to sell (or deploy) a system should be the first priority of any
project management team.  Not all requirements are absolutely
necessary.  Even if a requirement is highly desirable, or if it
has a high return on investment, it should not be classed as
absolutely necessary unless the system can not be deployed without
it.

It should also be noted that whether or not a requirement is necessary
for deployment will change over time.  Our understanding of the situation
is rarely complete, so we may discover new information over time.  The
business environment also changes over time.  Windows of opportunity
open and close.  Finally, as the system matures, new demands are
made of it.

### User Expectations

Given any set of requirements, there will be a number
of user expectations for those requirements.  Meeting the requirements
without meeting the user expectations will result in the user
being surprised or displeased.  For example, there may be a requirement
for a word processor to read a certain file format.  There may
be an additional user expectation that this type of file can be
read in a short period of time.

A user expectation is not always a necessary requirement.  It may
be possible to sell or deploy the system without meeting the user's
expectations.  However, it is a quality issue.  Software that meets 
all of the user's expectations will be considered to be high quality.
As the user encounters issues that do not meet expectations, the
perception of quality drops.  Even if the user later becomes used
to the operation of the software, the perception of low quality can
persist.

Usually, it is not possible to determine user expectations fully
without allowing the user to use the system.  Some expectations
can be guessed ahead of time, but others can only be discovered
by using the system and observing other users of the system.
If a high quality system is desired, time must be allocated to
discover these expectations after the necessary requirements have
been implemented (or partially implemented).

### Developer Expectations

In addition to user expectations, members of the development team 
(including program management) may have expectations of the software.
This usually comes in the form of new and innovative functionality
that the user will not yet imagine.  Because others do not expect
this functionality, it is obviously not a necessary requirement.
It is just as obviously not a user expectation.  However, it can
be an important market differentiator for a product.

When considering developer expectations, it is important not to
confuse them with user expectations.  Development teams are
often isolated from real users and can have a distorted view
of what a normal user expects.  If at all possible, when deciding
if an expectation is a user expectation or not, it is best to
consult an actual user.

Another danger with developer expectations is the tendency to
choose them in favour of user expectations.  It is extremely tempting
to believe that through our expertise as developers we know better
than the user what they will want.  This is rarely the case.
If a developer expectation conflicts with a user expectation it
is usually better to choose the user expectation unless extensive
user useability testing is done.  As stated above, failure to meet
user expectations will be considered as poor quality, even if the
user eventually gets used to the developer's choice.

In some circumstances, a development group will prioritize a
developer expectation over a necessary requirement.  This will
result in the failure of the project, as the system will not
be deployable.  No matter how desirable a feature seems, or how
much members of the development and program management team
wish for a feature, if it conflicts with a necessary requirement
it must not be implemented.

