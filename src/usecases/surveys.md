# Atomic Data for Surveys

Surveys and Questionnaires haven't been evolving that much over the past few years.
However, Atomic Data has a couple of unique characteristics that would make it especially suitable for surveys.
It could help make surveys easier to **fill in**, easier to **analyze**, easier to **create**, and more **privacy friendly**.

- **Pre-filled form fields**. which can save the respondent a lot of time.
- **Privacy friendly, yet highly personalized invites** as a researcher, send profile descriptions to servers, and let the servers tell if the question is relevant.
- **Question standardization** which helps researchers to re-use (validated) questions, which saves time for the researcher

## Privacy friendly invites

Currently, a researcher needs to either build their own panel, or use a service that has a lot of respondents.
Sometimes, researchers will need a very specific target audience, like a specific age group, nationality, gender, or owners of specific types of devices.
Targeting these individuals is generally done by having a large database of personal information from many individuals.
But there is another way of doing this.
Instead of asking for the users data, and storing it centralized, we could send queries to decentralized personal data stores.
There queries basically contain the targeting information and an invitation.
The query is executed on the personal data store, and if the result is interesting to the user, it is shown in a feed / a notification is sent to the user.
The user simply opens their application, and only sees invitations that are highly relevant, without sharing _any_ information with the researcher.

The Atomic Data specification solves at least part of this problem.
[Paths](../core/paths.md) are used to describe the queries that researchers make.
[Atomic Server](https://github.com/joepio/atomic/blob/master/server/README.md) can be used as the personal online data store.

However, we still need to specify the process of sending a request to an individual (probably by introducing an [inbox](https://github.com/ontola/atomic-data/issues/28))

## Question Standardization

We can think of Questions as Resources that have a URL, and can be shared.
Sharing questions like that can make it easier to use the same questions across surveys, which in turn can make it easier to interpret data.
Some fields (e.g. medical) have highly standardized questions, which have been validated by studies.
These Question resources should contain information about:

- The **question** itself and its translations
- The **datatype** of the response (e.g. `date`, `string`, `enum`), denoted by the [Property](https://atomicdata.dev/classes/Property) of the response.
- The **path of the data**, relative to the user. For example, a user's `birthdate` can be found by going to `/ profile birthdate`

[Atomic Schema](../schema/intro.md) and [Atomic Paths](../core/paths.md) can be of value here.

## Pre-filled form fields

If a user
