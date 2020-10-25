|Read No. | Name of chapter|
|:---------: |:--------------:|
|7|[What Google Learned From Its Quest to Build the Perfect Team](what-google.md)|
|7|[How I explained REST to my brother](How-I-explained-REST-to-my-brother.md)|




















# What Google Learned From Its Quest
# to Build the Perfect Team

## THE WORK ISSUE: REIMAGINING THE OFFICE

1- How to Build a Perfect Team

2- The War on Meetings

3- The Case for Blind Hiring

4- Failure to Lunch

5- The 'Good Jobs' Gamble

6- Rethinking the Work-Life Equation

7- The Rise of White-Collar Automation

8- The Post-Cubicle Office

9- The New Dream Jobs


### Yet many of today’s most valuable firms have come to realize that analyzing and improving individual workers ­— a practice known as ‘‘employee performance optimization’’ — isn’t enough. As commerce becomes increasingly global and complex, the bulk of modern work is more and more team-based. One study, published in The Harvard Business Review last month, found that ‘‘the time spent by managers and employees in collaborative activities has ballooned by 50 percent or more’’ over the last two decades and that, at many companies, more than three-quarters of an employee’s day is spent communicating with colleagues.

### In Silicon Valley, software engineers are encouraged to work together, in part because studies show that groups tend to innovate faster, see mistakes more quickly and find better solutions to problems. Studies also show that people working in teams tend to achieve better results and report higher job satisfaction. In a 2015 study, executives said that profitability increases when workers are persuaded to collaborate more. Within companies and conglomerates, as well as in government agencies and schools, teams are now the fundamental unit of organization. If a company wants to outstrip its competitors, it needs to influence not only how people work but also how they work together.

### Project Aristotle’s researchers began by reviewing a half-century of academic studies looking at how teams worked. Were the best teams made up of people with similar interests? Or did it matter more whether everyone was motivated by the same kinds of rewards? Based on those studies, the researchers scrutinized the composition of groups inside Google: How often did teammates socialize outside the office? Did they have the same hobbies? Were their educational backgrounds similar? Was it better for all teammates to be outgoing or for all of them to be shy? They drew diagrams showing which teams had overlapping memberships and which groups had exceeded their departments’ goals. They studied how long teams stuck together and if gender balance seemed to have an impact on a team’s success.
![group work](https://user-images.githubusercontent.com/70091044/93966452-6d958700-fd6d-11ea-9c75-252599614960.PNG)


### Imagine you have been invited to join one of two groups.

### Team A is composed of people who are all exceptionally smart and successful. When you watch a video of this group working, you see professionals who wait until a topic arises in which they are expert, and then they speak at length, explaining what the group ought to do. When someone makes a side comment, the speaker stops, reminds everyone of the agenda and pushes the meeting back on track. This team is efficient. There is no idle chitchat or long debates. The meeting ends as scheduled and disbands so everyone can get back to their desks.

### Team B is different. It’s evenly divided between successful executives and middle managers with few professional accomplishments. Teammates jump in and out of discussions. People interject and complete one another’s thoughts. When a team member abruptly changes the topic, the rest of the group follows him off the agenda. At the end of the meeting, the meeting doesn’t actually end: Everyone sits around to gossip and talk about their lives.

### Which group would you rather join?













# How I explained REST to my brother

## *Brother*: Hey, I have a question for you… Who is “Roy Fielding”?

## *ME*: Some guy. He's smart.

## *Brother*: Oh? What did he do?

## *ME*: He helped write the first web servers, that sent documents across the Internet… and then he did a ton of research explaining why the web works the way it does. His name is on the specification for the protocol that is used to get pages from servers to your browser.

## *Brother*: How does that work, anyway?

## *ME*: The web?

## *Brother*: Yeah.

## *ME*: Hmm. Well, it's all pretty amazing really. And the funny thing is that it's all very undervalued. The protocol I mentioned, that he helped write, HTTP, it's capable of all sorts of neat stuff that people ignore for some reason.

## *Brother*: You mean “http” like the beginning of what I type into the browser?

## *ME*: Yeah. That first part tells the browser what protocol to use. That stuff you type in there is one of the most important breakthroughs in the history of computing.

## *Brother*: Why?

## *ME*: Because it is capable of describing the location of something anywhere in the world from anywhere in the world. It's the foundation of the web. You can think of it like GPS coordinates for knowledge and information.

## *Brother*: For web pages?

## *ME*: For anything really. That guy, Roy Fielding, he talks a lot about what those things point to in that research I was talking about. The whole world wide web is built on an architectural style called “REST”. REST provides a definition of a “resource”, which is what those things point to.

## *Brother*: A web page is a resource?

## *ME*: Kind of. A web page is a “representation” of a resource. Resources are just concepts. URLs--those things that you type into the browser...

## *Brother*: I know what a URL is..

## *ME*: Oh, right. Those URLs tell the browser that there's a concept somewhere. A browser can then go ask for a specific representation of the concept. Specifically, the browser asks for the web page representation of the concept.

## *Brother*: What other kinds of representations are there?

## *ME*: Actually, representations is one of these things that doesn't get used a lot. In most cases, a resource has only a single representation. But we're hoping that representations will be used more in the future because there's a bunch of new formats popping up all over the place.

## *Brother*: Like what?

## *ME*: Hmm. Well, there's this concept that people are calling “Web Services” or "APIs". It means a lot of different things to a lot of different people but the basic concept is that machines could use the web just like people do.

## *Brother*: Is this another robot thing?

## *ME*: No, not really. I don't mean that machines will be sitting down at the desk and browsing the web. But computers can use those same protocols to send messages back and forth to each other. We've been doing that for a long time but none of the techniques we use today work well when you need to be able to talk to all of the machines in the entire world.

## *Brother*: Why not?

## *ME*: Because they weren't designed to be used like that. When Fielding and his buddies started building the web, being able to talk to any machine anywhere in the world was a primary concern. Most of the techniques we use at work to get computers to talk to each other didn't have those requirements. You just needed to talk to a small group of machines.

## *Brother*: And now you need to talk to all the machines?

## *ME*: Yes - and more. We need to be able to talk to all machines about all the stuff that's on all the other machines. So we need some way of having one machine tell another machine about a resource that might be on yet another machine.

## *Brother*: What?

## *ME*: Let's say you're talking to our sister and she wants to borrow Great Grandma's silver water jug or something. But you don't have it - Mom has it. So you tell our sister to get it from Mom instead. This happens all the time in real life and it happens all the time when machines start talking too. On the Internet, it's called a "redirect".

## *Brother*: So how do the machines tell each other where things are?

## *ME*: The URL, of course. If everything that machines need to talk about has a corresponding URL, you've created the machine equivalent of a noun. That you and I and the rest of the world have agreed on talking about nouns in a certain way is pretty important, eh?

## *Brother*: Yeah.

## *ME*: Machines don't have a universal noun - that's why they suck. Every programming language, database, or other kind of system has a different way of talking about nouns. That's why the URL is so important. It let's all of these systems tell each other about each other's nouns.

## *Brother*: But when I'm looking at a web page, I don't think of it like that.

## *ME*: Nobody does. Except Fielding and handful of other people. That's why machines still suck.

## *Brother*: Ha, what about verbs and pronouns and adjectives?

## *ME*: Funny you asked because that's another big aspect of REST. Well, verbs are anyway.

## *Brother*: I was just joking.

## *ME*: It was a funny joke! but it's actually not a joke at all. Verbs are important. There's a powerful concept in programming and CS theory called “polymorphism”. That's a geeky way of saying that different nouns can have the same verb applied to them.

## *Brother*: I don't get it.

## *ME*: Well.. Take a look at your coffee table. What are the nouns? Laptop, bottle, book, paper. Now, what are some things you can do to all of these things?

## *Brother*: I don't understand what you mean...

## *ME*: You can "get" them, right? You can pick them up. You can knock them on the floor. You can burn them. You can apply those same exact verbs to any of the objects sitting there.

## *Brother*: Okay... so?

## *ME*: Well, that's important. What if instead of me being able to say to you, "get the bottle," and "get the magazine," and "get the book"; what if instead we needed to come up with different verbs for each of the nouns? I couldn't use the word "get" universally, but instead had to think up a new word for each verb/noun combination. "shmet the bottle", "mandle the magazine", "zorp the book"

## *Brother*: Wow! That's weird.

## *ME*: Yes, it is. Our brains are somehow smart enough to know that the same verbs, like GET, can be applied to many different nouns. Some verbs are more specific than others and apply only to a small set of nouns. For instance, I can't drive a cup and I can't drink a car. But some verbs are almost universal like GET, PUT, and DELETE.

## *Brother*: You can't DELETE a cup.

## *ME*: Well, okay, but you can throw it away. That was another joke, right?

## *Brother*: Yeah.

## *ME*: So anyway, HTTP—this protocol Fielding and his friends created—is all about applying verbs to nouns. For instance, when you go to a web page, the browser does an HTTP GET on the URL you type in and back comes a web page.

## Web pages usually have images, right? Those are separate resources. The web page just specifies the URLs to the images and the browser goes and does more GETs using the HTTP protocol on them until all the resources are obtained and the web page is displayed. But the important thing here is that very different kinds of nouns can be treated the same. Whether the noun is an image, text, video, an mp3, a slideshow, whatever. I can GET all of those things the same way given a URL.

## *Brother*: Sounds like GET is a pretty important verb.

## *ME*: It is. Especially when you're using a web browser because browsers pretty much just GET stuff. They don't do a lot of other types of interaction with resources. This is a problem because it has led many people to assume that HTTP is just for GETing. But HTTP is actually a general purpose protocol for applying verbs to nouns.

## *Brother*: Cool. But I still don't see how this changes anything. What kinds of nouns and verbs do you want?

## *ME*: Well the nouns are there but not in the right format.

## Think about when you're browsing around amazon.com looking for things to buy me for Christmas (whispers: VITAMIX!!!) . Imagine each of the products as being nouns. Now, if they were available in a representation that a machine could understand, you could do a lot of neat things.

## *Brother*: Why can't a machine understand a normal web page?

## *ME*: Because web pages are designed to be understood by people. A machine doesn't care about layout and styling. Machines basically just need the data. Ideally, every URL would have a human readable and a machine readable representation. When a machine GETs the resource, it will ask for the machine readable one. When a browser GETs a resource for a human, it will ask for the human readable one.

## *Brother*: So people would have to make machine formats for all their pages?

## *ME*: If it were valuable.

## Look, we've been talking about this with a lot of abstraction. How about we take a real example. Imagine you are a teacher - at school you probably have a big computer system, or three or four computer systems more likely, that would let you manage students: what classes they're in, what grades they're getting, emergency contacts, information about the books you teach out of, etc. If the systems are web-based, then there's probably a URL for each of the nouns involved here: student, teacher, class, book, room, etc. Right now, getting the URL through the browser gives you a web page. If there were a machine readable representation for each URL, then it would be trivial to latch new tools onto the system because all of that information would be consumable in a standard way. It would also make it quite a bit easier for each of the systems to talk to each other. Or, you could build a state or country-wide system that was able to talk to each of the individual school systems to collect testing scores. The possibilities are endless.

## *Brother*: And they use the nouns and verbs!

## *ME*: Exactly. Each of the systems would retrieve information from each other using a simple HTTP GET. If one system needs to add something to another system, it would use an HTTP POST. If a system wants to replace something in another system, it uses an HTTP PUT, or, to do a partial update, it'll hopefully use PATCH. The only thing left to figure out is what the data models should look like.

## *Brother*: So this is what software developers work on now? Deciding how to best model the data?

## *ME*: More or less, this is what engineers do in the web development world, thanks almost entirely to the popularity of RESTful web frameworks like Ruby on Rails.

## But this is a very recent change! Just a few years ago, the large majority of developers were busy writing layers of complex specifications for how to access data in a different way that isn't nearly as useful or eloquent. Nouns weren't universal and verbs weren't polymorphic. They basically ignored throwing out decades of real field usage and proven technique and kept starting over with something that looks a lot like other systems that have failed in the past. They used HTTP but only because it let them talk to our network and security people less. It was like trading simplicity for flashy tools and wizards.

## *Brother*: Ew…Why?

## *ME*: I have no idea.

## *Brother*: But we are done with all that?

## *ME*: We are done. Now, we just tell Rails what we want our data to look like, and it takes care of all of the communication pieces for us. It's a huge boost for productivity!