---
rpip: <to be assigned>
title: <The RPIP title is a few words, not a complete sentence>
description: <Description is one full (short) sentence>
author: <a comma separated list of the author's or authors' name + GitHub username (in parenthesis), or name and email (in angle brackets).  Example, FirstName LastName (@GitHubUsername), FirstName LastName <foo@bar.com>, FirstName (@GitHubUsername) and GitHubUsername (@GitHubUsername)>
discussions-to: <URL>
status: Draft
type: <Protocol, Meta, or Informational>
category (*only required for Protocol ): <Core or RPRC>
created: <date created on, in ISO 8601 (yyyy-mm-dd) format>
requires (*optional): <RPIP number(s)>
---

`rpip-appeal_grant_result_GA022310.md`
 
Appeal of the rejection of the grant request for Rocket Pool University - GA022310

## Abstract

This RPIP is an appeal to reverse the "no" vote on Grant GA022310, Rocket Pool University (RPU). RPU is a framework for hosting Rocket Pool oriented courses along the lines of the now-defunct Ethereum Studymaster course. Courses can be created by anyone, currently in the form of specifically formatted json file(s). A user (i.e., a connected wallet), reads through the lessons in a course and takes a quiz after designated lessons within that course. The user has limited chances to pass each quiz. Passing all quizzes for a course is required to obtain the POAP or potentially other digital certification. RPU, as specified in GMC funding request GA022310, also includes a "Basics of Rocket Pool" course designed to give a mid-level overview of the protocol, not from an implementation perspective, but from an academic perspective. The heart of this appeal is that the stated reason for rejection was the belief that this project might overlap another (non-GMC funded) project, which indicates a misunderstanding or incomplete communication of the two projects.
  
## Motivation

This appeal of the GMC decision, a "no" with request to re-file in the next round, is for the following reasons:
1. The stated reason, that the project might be too similar to another group's project (which is NOT being funded by GMC), indicates a misunderstanding of the two projects.
2. GMC should not defer to another groups' potential projects.
3. GMC should encourage outreach and educational projects in earnest.
4. This appeal lowers the request amount, potentially making it more in line with GMC budget.

## Specification

 Grant request GA022310, Rocket Pool University, covers:

    Frontend, written in NextJS 13 with TypeScript and TailwindCSS
    Wallet sign-in via rainbowkit and wagmi
    Laravel Database for user course and quiz information storage
    A basic “Introduction to Rocket Pool” course
    POAP Delivery mechanism for course completion (might be manual at first)
  
The complete grant request, in its entirety, is available here: 
  https://dao.rocketpool.net/t/april-2023-gmc-call-for-grant-applications-deadline-is-april-15th/1638/12
  
## Rationale
  
Appeal Grounds Expanded

1. The stated reason, that the project is potentially too similar to another group's project (which is NOT being funded by GMC), indicates a misunderstanding of the two projects.

   The EVMaverick's project, https://therocketschool.xyz, is a potential video tutorial series on specific implementations of the Rocket Pool protocol. For example, "How to set up a node". This content is very valuable but has no overlap with Rocket Pool University. RPU could host a video tutorial series, but it is probably overkill and not the ideal format for such a presentation. 

Rocket Pool University courses can certainly contain images, videos and graphics, but it is a primarily text based reading/testing framework with certification (likely in the form of POAPs) for overall concepts within the Rocket Pool ecosystem. The website is a framework to easily allow classes to be created by anyone on any topic. For example, discord support certification or explanations of how to find and use various links and resources, i.e. information that might be useful to return to to reference in text based format.

As for content, the included and initial course, Basics of Rocket Pool, is not meant to replace the official documentation, it is an overview of the documentation; an easily digestible "quick start" version written from the ground up to give a different perspective on what parts are needed for novices to garner a quick but encompassing vision of the protocol. NOT, a quick understanding of how to set up a node or minipool. In many cases, it references the docs and via the quiz teaches students how to reference them themselves.

2. GMC should not defer to other group's potential projects.
 
   I believe the GMC should be proactive in the funding and encouragement of community projects and not reactive to other groups prospective projects. I am aware that Rocket Pool's EVMavericks are an influential subset of Rocket Pool and perhaps the GMC, so I understand that they are possibly an exception to this rule. Nevertheless, I feel it should be, in general, part of the mindset of the GMC to seekout more outreach anticipating success rather than limit outreach by questioning if it might not reach enough people or potentially mildly duplicate efforts.

3. GMC should encourage outreach and educational projects in earnest.
 
   It is important to offer several variants of education on the protocol, since people learn via many different methods. Expanding and encouraging alternatives is a tried and true teaching method in modern education. Furthermore, much of the language used in a large scale projects, like RP, tends to repeat obscure phrases and buzzwords that are confusing to newcomers and, all too often, much of the existing community. Different wordings and summaries can open up minds to concepts previously not fully grasped. This is something we should strive towards, not try to avoid.

   In addition, the GMC is sitting on unused funds. Knowing the GMC funds will be spent, encourages the community to create and innovate. If GMC grant funding seems unachievable, the opposite effect will prevail. In fact, this framework will allow others to easily put their content online for GMC funding without reinventing the wheel. 

4. This appeal lowers the request amount, potentially making it more in line with GMC budget.
 
   The original request was priced in line with what I would charge, in general, for this type of project. Having participated in many grant requests throughout the years, they are all different and unique beasts. Grants are odd in that you are asking someone to pay you for something they didn't ask for and if they did would likely not have requested it via the method you are proposing.

In light of this and because I want to do this project in the hopes it benefits the community (not just for the grant money). I am significantly lowering my proposal.

Task: Website Framework
Request: $5400 (120 RPL @$45)
Comment: Although this is a large amount of work, I also understand that it is not a critical feature for the protocol, thus rate is not what I would normally ask.

Task: Basics of Rocket Pool course
Request: $900 (20 RPL @ $45)
Comment: The course will consist of roughly seven lessons with subsections and seven quizzes of roughly ten questions each.

Total: $6300 (140 RPL @ $45)

## Backwards Compatibility
Not an issue for this RPIP

## Test Cases
No protocol change request

## Reference Implementation
Note that this is not in any way near completion. I would prefer not to have given this out, yet, but I feel it would not be fair to ask for a vommunity vote without giving a greater indication of what the project would look like:
https://rpu-git-main-drdoofusmdphddds-gmailcom.vercel.app/

## Security Considerations
This is not a protocol change request

## Copyright
Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
Copyright
