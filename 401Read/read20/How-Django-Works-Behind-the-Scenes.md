# How Django Works Behind the Scenes

### Django is a Python-based web framework used by millions of developers and billions of consumers through popular apps like Instagram. It is open source, meaning the code is available for free on Github and can be downloaded onto any developer’s computer and used alongside the official documentation. 
### As with all open source projects, the two major issues that crop up are funding and control. Let’s start with funding: why does an open-source project need funding?

### It turns out that while writing code is fun and developers are generally willing to contribute their time for free to do so, there are a host of decidedly less fun tasks needed to maintain and sustain an open source project. This includes handling any legal/trademark issues, triaging tickets, guiding community discussions, organizing conferences, managing releases, and so on. As a result, almost all popular open source packages have some degree of funding involved, typically in one of three forms:

1) **Corporate Sponsor** - A group of engineers within a larger, for-profit company decide to open-source internal code. This is how React (Facebook) and Angular (Google) emerged.

2) **Solo** - An individual developer initially creates code, open sources it, and retains default control. This is the case for VueJS, Tailwind CSS, and Laravel, among others.

3) **Non-profit** - This was Django’s approach early on, in 2008, when the Django Software Foundation was formed to promote, support, and advance Django.

## Django Software Foundation
### The DSF supports and maintains Django in a number of capacities. The largest expense, by far, is the Fellows Program, paid contractors who triage tickets, manage releases, and generally perform the unsexy but necessary work needed to keep Django on track.

### Tim Graham was the inaugural fellow during its 3-month pilot in the fall of 2014 and became a full-time fellow in 2015. He remained in this role until 2018 before transitioning to a part-time role. Carlton Gibson joined as a part-time Fellow in 2018 and in 2019 Mariusz Felisiak took over from Tim Graham.

## Technical Organization
### The DSF handles legal, financial, and administrative matters for Django. But there is a separate organizational structure for the technical team.

### Historically, Django followed Python’s model of having a Benevolent Dictator for Life, that is, a project founder who retained final say for disputes/arguments within the community. Adrian Holovaty and Jacob Kaplan-Moss functioned as Django’s dual-BDFLs from 2005 until their retirement in 2014.

### Django has a small, core team of trusted volunteers who work alongside the Django Fellows to manage technical side of the Django Project. Django Core members are divided into teams that have authority over the Django Project infrastructure, including the Django Project website itself, the official issue tracker, official mailing lists, IRC channels, and more. There is currently ongoing discussion around potentially dissolving Django core or updating it in a meaningful way.