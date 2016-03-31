---
title: SLIM Use Cases
abbrev: slim-use-cases
docname: draft-ietf-slim-use-cases-latest
date: 2016
category:

ipr: 
area: ART
workgroup: SLIM
keyword: Note
keyword: SLIM
keyword: language


stand_alone: no
pi: 

author:
  -
    ins: N. Rooney
    name: Natasha Rooney
    organization: GSMA
    email: nrooney@gsma.com
    uri: https://gsma.com

informative:
  RFC4566: https://datatracker.ietf.org/doc/rfc4566/

  SLIM:
  	target: https://datatracker.ietf.org/wg/slim/charter/

  NEGOTIATING-HUMAN-LANG:
  	target: https://datatracker.ietf.org/doc/draft-ietf-slim-negotiating-human-language/

--- abstract

Use cases for selection of language for internet media.

	      
--- middle
# Introduction

The SLIM Working Group [SLIM] is developing standards for language selection for non-real-time and real-time communications. There are a number of relevant use cases which could benefit from this functionality including emergency service real-time communications and customer service. This document details the use cases for SLIM and gives some indication of necessary requirements. For each use case a 'Solution' is provided, indicating the implementability of the use case based on "Negotiating Human Language in Real-Time Communications" [NEGOTIATING-HUMAN-LANG].
			
# Use Cases

Use cases are listed below:
			
## Single two-way language
					
The simplest use case. One language and modality both ways in media described in SDP [RFC4566] as audio or video or text. Straightforward. Works for spoken, written and signed languages. An example is when a user makes a voice call and the preferred language of that user is specified in SDP, allowing the answerer to make decisions based on that specification.
				
- Solution: Possible
				
## Alternatives in the same modality

Two or more language alternatives in the same modality. Two or more languages both ways in media described in SDP as audio or video or text, but only in one modality. Straightforward. Works for spoken, written and signed languages. The answering part selects. There is a relative preference expressed by the order, and the answering part can try to fulfill that in the best way. An example is a user who makes a voice call and prefers French as their first language and German as their second, and the answerer selects to speak German as no French speaking abilites are available. 
				
- Solution: Possible
				
## Fairly equal alternatives in different modalities.

Two or more modality alternatives. Two or more languages in different modalities both ways in media described in SDP as audio or video or text. An example is a person with hearing abilities who is also competent in sign language declares both spoken and sign language competence in audio and video. This is fairly straightforward, as long as there is no strong difference in preference for these alternatives. The indication of sign language competence is needed to avoid invoking relay services in calls with deaf sign language users only indicating sign language.
				
- Solution: Possible
				
## Last resort indication

One language in the different modalities. Allows the user to indicate one last resort language when no other is available. For example, a hearing user has text capability but want to use that as last resort. (With current specifications, there is no way to describe preference level between modalities and no way to describe absolute preference.)

- Solution: An answering service will have no guidance to which is the preferred modality and may select to use the modality that is the callers last resort even if the preferred alternative is available.

Another practical case can be a sign language user with a small mobile terminal that has some inconvenient means for texting, but sign language will be strongly preferred. In order to not miss any calls, the indication of text as last resort would be desirable.

- Solution: need coding of an absolute preference: hi, med, lo together with the tag.
				
## Directional capabilities in different modalities

Two or more language alternatives in the different modalities. For example, a hard-of-hearing user strongly prefers to talk and receive text back. Spoken language input is appreciated. This can be indicated by spoken language two-ways in audio, and reception of language in text. (There is no current solution that says that the text path is important. The answering part may see it as an alternative.)

- Solution: Need for preference indication per modality

### Fail gracefully?

There currently are methods to indicate that the call shall fail if a language is not met, but that may be too drastic for some users including the one in the above scenario (Section 2.5). It may be important to be able to connect and just say something, or use residual hearing to get something back when the voice is familiar.

- Possible solution: coding of an absolute preference together with the tag could solve this case if used together with the directional indications. For example:

`preference: hi, med, lo` 

Another solution would be to indicate required grouping of media, however this raises the complexity level.

## Combination of modalities

Similar to Section 2.5, two or more language alternatives in the different modalities. A person who is deaf-blind may have highest preference for signing to the answerer and then receiving text in return. This requires the indication of sign language output in video and text reception in text, using the current directional attributes. An answering party may seek suitable modalities for each direction and find the only possible combination.
	
- Solution: Need for preference indication per modality

## Person with speech disabilities who prefer speech-to-speech service

One specific language for one specific modality with a speech-speech engine. A person who may find that others have some difficulty in understanding what they are trying to say may be used to have support of a speech-to-speech relay service that aids clear speech when needed for the understanding. Typically, only calls with close friends and family might be possible without the relay service.

This user would indicate preference for receiving spoken language in audio. Text output can be indicated but this user might want to use this method as a last resort. (There is no current coding for vague or unarticulated speech or other needs for a speech-to-speech service.)

A possibility could be to indicate no preference for spoken language out, a coding of proposed assisting service and an indication of text output on a low absolute level.
	
- Solution: Need of service indication, and absolute level of preference indication.

## Person with speech disabilities who prefer to type and hear

Two or more language alternatives for multiple modalities. A person who speaks in a way that may be hard to understand, may be used to using text for output and listen to spoken language for input. This user would indicate preference for receiving spoken language in audio. Text output modality can be indicated.

If the answering party has text and audio capabilities, there is a match. If only voice capabilities exist there is a need to invoke a text relay service.

- Solution: Need of service indication, and absolute level of preference indication.

## All Possibilities

Mutiple languages and multiple modalities. For example: a tele-sales center calls out and wants to offer all kinds of possibilities so that the answering party can select. A tele-sales center has competence in multiple spoken languages and can invoke relay services rapidly if needed. So, it indicates in the call setup competence in a number of spoken languages in audio, a number of sign languages in video and a number of written languages in text. This would allow, as a further example, a deaf-blind person who prefers to sign out and get text back answers with only these capabilities. The center can detect that and act accordingly, this could work in the following methods:

- Solution Alternative 1: The center calls without SDP. A deafblind user includes its SDP offer and the center sees what is needed to fulfill the call. 
- Solution Alternative 2: The center calls out with only the spoken language capabilities indicated that the caller can handle.

The person with deaf and / or sight disabilities who answers, or terminal or service provider detects the difference compared to the capabilities of the answering party, and adds a suitable relay service. (This does not use all the offerings of the callers competence to pull in extra services, but is maybe a more realistic case for what usually happens in practice. )

- Solution: Possible in the same way as cases in Section 1.8.

# Final Comments

The use cases identified here try to cover all cases of when users wish to make text, voice or video communication using the language of set of languages in which they are able to speak, write or sign and for which the receivers are also able to communicate. Some of these use cases go even further to allow give some users the ability to select multiple and different languages based on their abilities and needs.

To fulfill all the use cases the currently specified directionality will be needed, as well as an indication of absolute preference. An indication of suitable service and its spoken language is needed for the speech-to-speech case, but can be useful for other cases as well. There is no clear need for explicit grouping of modalities seem to be needed. 

Subsequent work in the Selection of Language for Internet Media Working Group [SLIM] will work on Internet Drafts to support these use cases. 

# Security Considerations

Indications of user preferred language may give indications as to their nationality, background and abilities. It may also give indication to any possible disabilities and some existing and ongoing health issues.

# IANA Considerations

This document has no IANA actions. 


--- back

# Acknowledgments

Gunnar Hellstrom's experience and knowledge in this area provided a great deal of these use cases. Thanks also goes to Randall Gellens and Brian Rosen. 

