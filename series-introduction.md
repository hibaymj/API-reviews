Hello again Internet!

Over the last couple years, I've missed being able to help others by sharing my experiences!

I've put up a poll and it looks like most folks are looking for a combination of video (WHY?) and blog so lets give this a shot!

I'm going to go through the most popular publicly available API repositories starting with Postman and review and redesign what I find in a RESTful (for real) manner.

## Disclaimer Town

Before I say one thing about any API I find, I want to make one thing perfectly clear: every API I will redesign is the result of a tremendous amount of work for a substantial group of people. None of this is field really intuitive. I often say APIs are [https://www.merriam-webster.com/dictionary/specious](specious). It takes a tremendous amount of work to adapt your incidental understanding of HTTP and REST to conform with the specification and pattern respectively. When people spend a lot of time on work it becomes personal. We become invested in the things we do, and it hurts when people say your wrong. Usually more when its true. I say this from experience, it isn't fun when your best isn't good enough. I can say with utmost confidence that when it comes to API design, I've been wrong a lot more than almost anyone in the world. I learned from each and every time, and now I'd like to help others avoid some of that suffering. I am not here, nor do I wish to entertain or engage with anyone looking to dunk on the hard work of others.

This series will be long, wordy, detailed, and nuanced by its very nature. I will greatly simplify my life writing, and your's reading, it by being direct and removing the complexity of dancing around any particular point. Points made in these posts will be objectively true. I will specifically state when a particular point has either optionality of multiple correct alternatives or some sort of preferential choice, and I will attempt to list all choices or give illustrative examples. While writing and further over time, depending on how this all shapes out, I may add specific citations to the RFCs, disertations, or writings. The goal of this effort however isn't to write a PhD thesis. I'm writing this to highlight the overwhelming amount of revenue and consumer value being left on the table across the industry due to the significant difference between truly RESTful APIs and what most people believe they are.

# Lets set some groundrules.

Knowledge and affordance over data and documentation. Every time.

The former offers orders of magnitude more value orders of magnitude faster. Before we define the terms, let's go through a quick scenario which will explain it very quickly.
//include picture of pull door with push handle.

I'm willing to wager we have all encountered this situation, even if it wasn't particularly noteworthy in your memory. Personally, I'm a fast walker and sometimes I'll be lost in thought walking. Then BAM. My forehead and foot are in pain, and I feel completely foolish. It was a push handle on a pull door, and a painful lesson in affordances.

I've walked through many doors with push handles. Those experiences gave me the knowledge that a door with it's handle across the glass window is opened by pushing it away from me. This knowledge grants me an intuitive understanding of the doors 'Open' affordance, or both the ability of the door to be opened and a inherent understanding of how to perform the action.

There are many more wordy (and correct) definitions, but for simplicities sake we'll go with this short one. An affordance is the stateful presentation of an entity's ability to perform a state change. Continuing the example, I saw the handle and my previous experience granted to the understanding that the door could be opened by pushing on the bar. I didn't have to ask someone(retrieve data), or read a manual(documentation). The affordance was presented to me in a way which leveraged my knowledge and intuitive understanding.

Why stateful presentation? Let's get a bit more specific, there's two kinds of open affordances for a typical hinge door: push, and pull. The handle is presenting the push affordance that the state of the door doesn't support. It's a pull door. If you reconfigure the door to push, or change the handle then everything is fine. Affordances should be presented statefully, when they are available by a thing's internal state.

Knowledge.

(GULP)

Let's talk about knowledge. There's a lot of truly brilliant people working on knowledge (Yes, I'm talking about SemWEB). There is an elephant in the room whenver you talk about Knowledge in the Computer Science and Infomatics sense: ontology. There, I said it. Now I'm going to move past it as quickly as I can by analogy. In computer science there is a concept called Turing Complete, which boils down to saying something is calculatable on a turing machine based computer. All our computers are turing machines. Now some algorithms ARE turing complete, and yet completely and utterly useless in a human lifetime unless given substantial constraints. These are extremely necessary for the abstract science to create computers and computer languages, but they have no _direct_ practical use. From a purely _practical_ day-to-day computing standpoint they effectively don't work. The SemWEB is working on knowledge from an ontological perspective, and while everything they work on and do is correct its effectively not helpful because its inherently _infinite_ (and it NEEDS to be).

'A priori' I like to throw some latin in my writing from time to time. It makes me feel fancy like my degree wasn't a waste. On the plus side it usually can communicate some big ideas in just a few words. Crudely put 'a priori' is understanding from knowledge _before_ an experience. We discussed a set of affordances 'Open', 'Open-Push', and 'Open-Pull'. This is a _finite_ set. Knowledge of my previous experience _granted_ me the understanding that the push handle granted the door the 'Open-Push' affordance. I knew this before I walked up to the door, and _applied_ my understanding to interpret the situation. Interacting with systems requires a _finite_ vocabulary of entities and affordances. In any given moment you're knowledge is finite. Your understanding of concepts, entities, and affordances are a _bounded vocabulary_. This vocabulary evolves and grows over time and this is akin to new versions of your vocabulary rather than an infinite dynamic set of ever changing words.


