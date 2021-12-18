---
title: Potential design document formats
---

In my previous post I made an argument for the importance of technical writing in general, and the importance of design documents specifically.

Let’s talk about potential formats we can use for our design documents.

First of all, what is the objective, the outcome of this documentation process? It is to establish a high-level design for the software you are going to write and put it in the context of the problem you are trying to solve, the constraints you have, and the tradeoffs you are going to make.

What is the best medium for that?

I suggest that the best format is a written document that one can read in 10-30 minutes, complete with diagrams and data.

The audience for this document would be both the designers/engineers that can help you review it, as well as the implementing engineers.

When it comes to evaluating options, it is helpful to start with elimination first.

![](/assets/img/troika.png)

## Slides

Having spent a lot of my career in large enterprises, I anticipate the first question, “well, our whole company runs on presentations, why not use them?”

In my experience, the problem with slides is that they are not a ground-zero tool for exploring, documenting, and getting others up to speed on the design in all its nuance.

This is worth exploring a little deeper.

First, the information density for the slides is very poor compared to the written document. Simply put, the slides with a few bullets and large fonts cannot fit much information. You have to boil down your design and eliminate nuance.

Next, people read 3x times faster than they talk. Let me paint the extreme case - presenting something to an executive. Any exec by the nature of their job is super-skilled at acquiring context fast in any conversation they walk into. An exec is also impatient and has no qualms about squeezing the presenter for the info they want. As a result, the charted course of presentation has no chance of holding up. The exec would be jumping back and forth, trying to build the mental model they are after. This is a frustrating experience both for the author/presenter (“this is answered in the later slides!”) as well as the exec (“stop spoon feeding and get to the point!”).

There is a lot of effort that goes into the presentation aspect of the slides (images, formatting). All of these target the emotional impact. It is important for selling, but it is simply waste if what you are trying to do is to engage with the ideas on their merit.

The slides also imply the presenter, they rarely travel alone well. This introduces a lot of bias, making presentations with a speaker a very non-inclusive medium. A good presenter with a reality distortion field will sell you very effectively on an idea; but days later you would shake your head in disbelief, realizing that you remember nothing from their talk, and yet you were convinced. And vice versa, a poor presenter would turn off the audience from a good idea.

Presentations with a dynamic speaker definitely have their place—they motivate, they energize, they make things stick better. But this is not our goal here.

I have effectively used a presentation as a lens into the design document. A few slides can summarize the design, or a single scorecard can present it in a consistent format that you can talk to without losing your audience to other slides. All of these are lossy projections, they are useful, but they must have the underlying document in place to draw from.

## Pull Requests

Now that we have convinced ourselves that slides are not the way to go, let’s look at another extreme: pull requests (PRs). I want to use it as a bookend to frame the temporal aspect of the process. 

As engineers, a Pull Request is a natural place for reviewing others' work, especially coupled with the Github experience around it. I hope it is clear that this late in the implementation process a design review is a lot less effective. In most cases a reviewer will sigh, throw up their hands, quibble about a few stylistic inaccuracies and let the rest go. The code is already written, the time has passed to provide input on the design. And the comments in the PR are too fine-grained and tethered to individual details at source code line level to address the approach as a whole. Don’t do it. At the very least agree to talk through the implementation when picking up a story. But better yet, do the upfront design earlier when looking at the whole feature or epic or product roadmap.

Of course, a PR process is fine for authoring a design document, and its use will depend on what the team is familiar and comfortble with.

## Architecture Decision Records(ADRs)

What about Architecture Decision Records (ADRs)? They might be too tactical—after all, we are talking about one document per decision. One might be losing sight of the forest for the trees. If you decide to stick to ADRs, at least discuss them in a high-bandwidth setting first (e.g. architecture roundtable), do not just rely on pull requests (PRs) to shape the overall document, it would drag the process out for much longer.

![](/assets/img/typewriter-reading.png)

So this leaves us with design documents, although some might call them Request For Comments (RFCs), the name that establishes continuity with the well-known RFC process that governs the Internet.

Now that we have these popular alternatives out of the way, we’ll talk about the suggested format for design documents, some tips and tricks, and finally the process behind them.
