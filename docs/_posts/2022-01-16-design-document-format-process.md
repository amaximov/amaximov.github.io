---
title: Design document format and process
---

Below are some of my experiences writing, editing, and reviewing design documents.

I am resisting the temptation to present the complete format here, since it is culture- and org-specific.

As a recap, the design doc documents the high level implementation strategy and key design decisions with emphasis on the trade-offs that were considered during those decisions.

![](/assets/img/thinker.png)

# Document sections

## Size

As mentioned in the previous posts, keep the document size to 5-10 pages max. Basically, anything you can read through in 10-30 minutes.

If there is more content than that, introduce another document that captures larger context and then break out smaller designs into separate design documents. Nobody will read a 200 page paper.

## Metadata

It is useful to keep track of large changes as well as the authors upfront. Yes, most editors these days have history, but you need semantic history, not a flurry of editing information.

Other metadata might be more useful in larger companies, where you have multiple orgs and teams. Consider externalizing it to make it easier to organize and track documents:
* the status of the document (accepted/proposed/obsoleted by)
* RACI matrix—who has been consulted, who is accountable for the decision, who has authored the document, who has been informed
* the lifecycle—when was it published, when was it accepted

## What and why

In my experience, when it comes to format, the biggest levers that tend to be missed are the “what” and “why” sections, since shaping the problem upfront often contains most of the answer. Avoid the temptation to jump straight to the tools/tech selection, since this is what we gravitate towards as engineers.

Tease out the requirements and ground them. They have to be stated upfront. It should not be a tech choice first that you stretch the problem over. Your design needs to be grounded in numbers, both current and expected. Anecdotally, I have seen so many “real-time” stream processing system designs that turned out to be a once-a-day batch for a few hundred clients.

Embrace constraints as much as possible, they will define the shape of the design early on, they will reduce the possible options. In large established companies the universe of possible options alone could be the longest pole in your design process tent. Everyone would drag in their pet solution, or some other tangentially relevant option, and ask you to consider it.

## Non-goals / out of scope

Put this upfront and keep refining, since it will focus any conversation early on. Call out the things explicitly out of scope. This will allow you to avoid spinning out into irrelevant side conversations. Keep stuffing things into this section over time, whenever a side conversation rears its head.

## Options and recommendations

This is the meat of the document, where you present the design you recommend as well as the options you have considered and rejected.

You want to capture the decision process that led to your recommendation, and the challenge is to show the alternatives you have considered without spending too much time on them. Sometimes it is helpful to put the recommended option upfront and tuck everything else below it.

It is important to bring up alternatives considered, since it will cut down on future conversations when inevitably (which is also even more so in larger orgs) someone would bring up, “what about X?” This is where you pin stuff down to make sure it does not creep back into focus and take up your time and attention.

## FAQ

Keep it at the end and keep populating it as you make the rounds, presenting your document. You do not want to re-open the same conversations over and over again, so pin things here.

## Open questions

Keep updating this section, both as a reminder as well as the things you might have to address later when you go into implementation.

## Idea graveyard

This might overlap with the options & recommendations section above, but sometimes I factor it out into its own section, especially if possible options are really far-flung and I need to keep pinning them down. Of course, choose a different term (icebox, parking lot, etc) if graveyard offends the org’s sensibilities.

## Diagrams

Diagrams - use them, they really help. Stick to context diagrams and architecturally significant aspects. Do not treat it as an implementation manual. You do not know the details well enough now (and if you do, then you probably do not need the design document in the first place), so stick to things that will establish guardrails and direction.

Diagrams are not the easiest thing to author. They require a visual skill and ability to simplify and organize that takes time to develop. Some people never get there.

While it might be tempting to use tools that lay out diagrams automatically for you (e.g. Python’s Diagrams), consider what you are trying to convey. It is not just the building blocks, but their relationship to each other. It is the concepts that map into the design. For more complex designs the way you lay things out and how you present them is what makes all the difference. The way you group, color, organize things is what makes the meaning come across. This is part of presentation design, not the mechanical layout of constituent pieces.

A well-done diagram becomes a reusable thinking tool for the roundtable discussion, something a wall of text cannot do.

# Process

![](/assets/img/process.png)

Now let’s talk about the process.

First of all, you will not get it right from the start. Manage expectations—you will need to iterate and refine both the format as well as the process. You will also need to establish the discipline to stick to the bar for quality that you have set.

## Authors

The document is written by a team, with perhaps a single person responsible for consistency and final formatting. Peer review even at this stage is key. Do not go too far writing, editing, organizing before getting feedback.

## Review

Use in-person discussion throughout the process if you can. It is high-bandwidth communication that can really advance the argument in minutes, otherwise the feedback cycles could stretch into weeks, with massive rewriting.

The remote work setup makes the feedback cycle harder. You have to be more deliberate to ensure it happens.

## Time
I hesitate to put the time on the process, since depending on the importance and complexity of the decision, it could be anywhere from an hour or two to several weeks. What is important though is converging on the decision and moving forward. Do not let the design process drag out. After all, what you ship is the software, not the design document.

## Decision making

Feed the document into your decision making process, whatever it is. In smaller orgs it might be just a meeting. In larger orgs it might be as formal as the [GSD wheel](https://www.radicalcandor.com/culture-of-listening/) or [SPADE](https://review.firstround.com/square-defangs-difficult-decisions-with-this-system-heres-how).

In any case, do not skip the important stages of the process: get feedback on the proposed design, make people feel heard, make a decision within a timebox, commit to it, publicize the decision, learn upon execution.

In larger orgs it does pay off to introduce a formal process to make sure everyone interested knows how things are happening and when. It will go a long way to reduce FUD and help people feel included and legitimize the approach. As it turns out mapping the process itself in a large org could take weeks, and is surprisingly involved. Consider sticking just to the broad brush strokes with outcome gates in between.

## When not to write a design doc

Design doc could be an overhead, it is an extra step, so invest in it judiciously.

I still think you should write things down, both as a tool to think through a problem as well as for posterity, but you could do it in a more lightweight manner—in your agile story description or even in the code comments.

If you do not need to get people on the same page, if you know the problem and solution space well, if the scope or the impact of the implementation is insignificant, then perhaps you should skip it altogether.

## Reviewers’ engagement

During the document reviews I often struggled with the engagement of the audience. It is a challenge for a group to walk in cold into a design discussion and get up to speed quickly enough to participate.

It is important to create an atmosphere of deeply engaged participants that are actively working, not just present for the sake of being considered a part of some coveted committee. 

Consider adding a list of reviewers to the document to help with accountability. Try sending the document out beforehand, try making people read the document at the beginning of the meeting in silence. There is no silver bullet—but you do need engaged participants that recognize it as their job.


