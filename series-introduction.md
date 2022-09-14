# Hello again Internet!

Over the last couple years, I've missed being able to help others by sharing my experiences!

I've put up a poll and it looks like most folks are looking for a combination of video (WHY?) and blog so lets give this a shot!

I'm going to go through the most popular publicly available API repositories starting with Postman and review and redesign what I find in a RESTful (for real) manner.

## Disclaimer Town

Before I say one thing about any API I find, I want to make one thing perfectly clear: every API I will redesign is the result of a tremendous amount of work for a substantial group of people. None of this is field really intuitive. I often say APIs are [specious](https://www.merriam-webster.com/dictionary/specious). It takes a tremendous amount of work to adapt your incidental understanding of HTTP and REST to conform with the specification and pattern respectively. When people spend a lot of time on work it becomes personal. We become invested in the things we do, and it hurts when people say your wrong. Usually more when its true. I say this from experience, it isn't fun when your best isn't good enough. I can say with utmost confidence that when it comes to API design, I've been wrong a lot more than almost anyone in the world. I learned from each and every time, and now I'd like to help others avoid some of that suffering. I am not here to, nor do I wish to entertain or engage with anyone looking to, dunk on the hard work of others.

This series will be long, wordy, detailed, and nuanced by its nature. I will greatly simplify my life writing, and your's reading, by being direct and removing the complexity of dancing around any particular point. I'm not going to mince words. Points made in these posts will be objectively true. I will specifically state when a particular point has either optionality of multiple correct alternatives or some sort of preferential choice, and I will attempt to list all choices or give illustrative examples. While writing and further over time, depending on how this all shapes out, I may add specific citations to the RFCs, disertations, or writings. The goal of this effort however isn't to write a PhD thesis. I'm writing this to highlight the overwhelming amount of revenue and consumer value being left on the table across the industry due to the significant difference between truly RESTful APIs and what most people believe they are.

## Lets set some groundrules.

Knowledge and affordance over data and documentation. Every time.

The former offers orders of magnitude more value orders of magnitude faster. Before we define the terms, let's go through a quick scenario which will explain it intuitively.
//include picture of pull door with push handle.

I'm willing to wager we have all encountered this situation, even if it wasn't particularly noteworthy in your memory. Sometimes I'll be lost in thought walking somewhere. BAM. My forehead and foot are in pain, and I feel completely foolish. It was a push handle on a pull door. This is a painful lesson in affordances.

I've walked through many doors with push handles. Those experiences gave me the knowledge that a door with it's handle across the glass window is opened by pushing it away from me. This knowledge grants me an intuitive understanding of the doors 'Open' affordance, or both the ability of the door to be opened and a inherent understanding of how to perform the action.

There are many more wordy (and correct) definitions, but for simplicity we'll go with the following. An affordance is the stateful presentation of an entity's ability to perform a state change. Continuing to unpack the example, I saw the handle and my previous experience granted to the understanding that the door could be opened by pushing on the bar. I didn't have to ask someone(retrieve data), or read a manual(documentation). The affordance was presented to me in a way which leveraged my knowledge and intuitive understanding.

Why stateful presentation? Let's get a bit more specific, there's two kinds of open affordances for a typical hinge door: push, and pull. The handle is presenting the push affordance that the state of the door doesn't support. It's a pull door. If you reconfigure the door to push, or change the handle then everything is fine. Affordances should be presented statefully, when they are available by a thing's internal state.

## Terms

### Knowledge.

(GULP)

Let's talk about knowledge. There's a lot of truly brilliant people working on knowledge (Yes, I'm talking about SemWEB). There is an elephant in the room whenver you talk about Knowledge in the Computer Science sense: ontology. There, I said it. Now I'm going to move past it as quickly as I can by analogy. In computer science there is a concept called Turing Complete, which boils down to saying something is calculatable on a turing machine based computer. All our computers are turing machines. Now some algorithms ARE turing complete, and yet completely and utterly useless in a human lifetime unless given substantial constraints. These are extremely necessary for the abstract science to create computers and computer languages, but they have no _direct_ practical use. From a purely _practical_ day-to-day computing standpoint they effectively don't work. The SemWEB world is working on knowledge from an ontological perspective, and while everything they work on and do is correct its effectively not helpful because its inherently _infinite_. For what they are mostly working on it NEEDS to be.

### Why is this a problem? A priori knowledge.

I like to throw some latin in my writing from time to time. It makes me feel fancy like my degree wasn't a complete waste. On the plus side it usually can communicate some big ideas in just a few words. Crudely put 'a priori' is understanding from knowledge _before_ an experience. We discussed a set of affordances 'Open', 'Open-Push', and 'Open-Pull'. This is a _finite_ set. Knowledge of my previous experience _granted_ me the understanding that the push handle granted the door the 'Open-Push' affordance. I knew this before I walked up to the door, and _applied_ my understanding to interpret the situation. Interacting with systems requires a _finite_ vocabulary of entities and affordances. In any given moment you're knowledge is finite. Your understanding of concepts, entities, and affordances are a _bounded vocabulary_. This vocabulary evolves and grows over time and this is akin to new versions of your vocabulary rather than an infinite dynamic set of ever changing words.

### Communication.

You can look at the way people and computers adapt to changing vocabulary as the same with two key differences: speed and cost. We all maintain our own vocabularies constantly in our mind. We don't need to pay anyone else to do it, and it happens almost instantaneously. Therefor we can heavily rely on ambiguity and our ability to adapt our vocabularies in the future as an efficient way to successfully communicate. Communication is fundamentally different for digital systems. Computers don't learn, unless you program them. They don't understand, so they can't infer. I'm going to ignore machine learning for now as it will just complicate the discussion without changing anything. If you want a computer to update it's vocabulary then you need a programmer to make updates in at least one program. There's wildly different programming cadences, but even assuming a relatively good turnaround time (in an enterprise environment) of two weeks between learning something new and updating the vocabulary, for the computer its been an eternity. CPU frequency varies a lot across servers and workloads from about 1.8 GHz to 5+ GHz. Let's assume it takes 10 cycles to 'think' from the computer's perspective, that means at 1.8 GHz the CPU is waiting 217,728,000,000,000 to 604,800,000,000,000 'thinking' cycles. That is a long time, and the change isn't even free. It costs a lot of money to pay a programmer. Probably the worst part is this is possibly the rosiest picture one could paint. In reality things would be far, far worse.

What we see is ambiguity, one of the cornerstones of human communication, is a fatal flaw in computer communication. This is an uncomfortable yet entirely unavoidable truth. The key to optimizing speed and costs in sociotechnical system communication is being very specific and precise about where you MUST be unambiguous while maximizing adaptability of the vocabulary for all parties both digital and biological.

## Design and Comparative Criteria

### What is objectively wrong?

We have seen a glimpse of the staggering differences in cost and scale when the design is wrong. An API design is _wrong_ when it unnecessarily compromising the speed or cost of adaptation or execution. That's it. Everything else is a more specific case of one or more of these 4 errors.

### What are correct alternatives or preferential choices?

Now that we understand what will cause us to conclude a design is objectively wrong, we can define our gray areas as alternative designs which present aproximately the same amount of inherent compromise where other qualities of the design will impact the chosen alternative. The classic example would be the choice between fixing a minor bug or running another instance of the software.

### The Floor - Or Inherent Compromise

Computer science is filled with tradeoffs. As developers we're familiar with many. In a lot of cases there aren't fundamental solutions to a design issue. Quite literally the laws of physics such as the speed of light and quantum mechanics impose invariable constraints on solution design. When faced with such a case API design should _sufficiently_ limit the _magnitude_ of the compromise so that it minimizes or removes the impact to the overall sociotechnical system. In other words, find a solution that is best for the system as a whole. We can clearly see that while 900,000,000 'thinking cycles' might be bad, its clearly better than 217,728,000,000,000.
