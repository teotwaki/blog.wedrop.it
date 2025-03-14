+++
title = "Deliberately choosing the wrong tool"
date = "2025-03-14"
description = "A quick reply to Steve Klabnik, about bias in tooling."

[taxonomies]
tags = ["management"]
+++

Steve Klabnik [recently wrote][klabnik-choosing-languages] about the toxic reactions to Microsoft's
release of the Golangified TypeScript compiler. It's a great article, and I highly recommend it.

[klabnik-choosing-languages]: https://steveklabnik.com/writing/choosing-languages/

At one point, Steve mentions that he's not a big fan of the "choose the right tool for the job"
trope that we hear very often in software engineering circles:

> There’s some sort of balance here to be struck. But at the same time, I hate “choose the right
> tool for the job” as a suggestion. Other than art projects, has anyone ever deliberately chosen
> the wrong tool? Often, something that seems like the wrong tool is chosen simply because the
> contextual requirements weren’t obvious to you, the interlocutor.

I'm not entirely certain how broad the definition of "contextual requirements" is, but provided it
does not include laziness, I believe that there are many examples where people have chosen the wrong
tool for the job, deliberately.

I, myself, am the first one to be guilty of this. And I'm almost entirely convinced that _you_ are,
too. Growing up, I had a decent collection of pocket knives, and would always have one with me when
I was roaming the countryside. My pocket knife was a pry bar, a screw driver, a bottle opener, a
coal rake, a skewer, a windlass, and a toothpick.

Furthermore, how many of us used our tongues to see if a 9V battery still had a charge in it or not?
I still readily reach for a butter knife when I need to unscrew a flathead screw without opening my
toolbox. How many PMs have used Visio or PowerPoint as a project management tool? How many build
systems started out as "a quick shell script"? How many businesses have _critical_ Excel documents
as the source of truth, or even as an entire database?

In some cases, one might argue that these choices were made out of necessity. Maybe that's the
_contextual requirement_ factor Steve mentions. Is it really, though? One of the most well-known
[StackOverflow answers][stackoverflow-zalgo] documents why one should never use regexes to try and
parse HTML. It is perhaps one of the best examples of Maslow's hammer that we have for software
development. No matter how many warnings, no matter how complex the grammar, once people grasp the
basics of regular expressions they believe they can parse anything with them. After years of that
answer being published, and legions of regex aficionados "Yes, but..."'ing him, the author gave up:

> I think it's time for me to quit the post of Assistant Don't Parse HTML With Regex Officer. No
> matter how many times we say it, they won't stop coming every day... every hour even. It is a lost
> cause, which someone else can fight for a bit. So go on, parse HTML with regex, if you must. It's
> only broken code, not life and death.

[stackoverflow-zalgo]: https://stackoverflow.com/a/1732454

So, why would someone deliberately choose the wrong tool? Laziness is, I think, a big factor.
Ignorance and desperation are other reasons I could trivially understand. Steve gives art a free
pass---and he's right. Sometimes, using the explicitly wrong tool makes a statement or teaches a
lesson.

By "contextual requirements", Steve likely meant that in some cases, a project might adopt a choice
that could be considered objectively inferior by externals, while still being the "correct" choice
for that specific team, given the constraints they are facing. And in a way, the same charity could
be extended to me using my pen knife as a pry bar to open a can of paint: there was no good
alternative immediately available, therefore it was the right choice, because the alternative would
have been to not do something. As Teddy Roosevelt put it, "the next best thing is the _wrong_
thing".

There is a trait in toxic management to try and give everything a positive spin, and therefore we
shouldn't call out errors. Sometimes it's because it's not a business priority to fix that mistake,
and therefore it's easier to not call it a mistake at all. Other times, it's because strong egos
can't accept the egg-on-face effect of having suboptimal decisions attached to their legacy. This
often happens with projects, and wanting to call projects a success, even if it ended up costing 5x
more than originally planned and was delivered 2 years behind schedule (of an original 12 month
schedule). I still hope I'll one day end up in a company that is able to call a project a failure,
and learn from the mistakes, instead of insisting on calling it a success, and ingraining the
mistakes as successful ways of doing something.

This mindset---that everything must be framed as an exclusive success---could actually be why some
of these decisional blunders continue to be made. Instead of admitting that something didn't work,
we double down on poor decisions.

So therefore, there's an aspect of timing, or perspective: if you don't know something is the wrong
tool when you use it, then it isn't the wrong tool in that moment. Hindsight might reveal that
something was objectively the wrong tool. And context helps to explain or justify why a decision was
made, and how that decision might even make sense for a given team.

But we should still be able to label things as a bad choice when they are identified, even if the
only tangible benefit of doing so is to prevent making the same bad choice in the future.

Now, I'd like to clarify something: I don't believe Microsoft switching to Golang instead of
`$OTHER_LANG` is a mistake in any way, shape or form. As I [expressed previously][masto-golang], I
think it's wonderful that Microsoft picked Golang, if and only if because this might finally curb
the current trend of pigeonholing programming languages into a singular purpose.

[masto-golang]: https://mastodon.online/@teotwaki/114151731751082435

Back in the day, Ruby gained insane popularity because it had an amazing development experience. TDD
tools would happily flash at you in your terminal as you implemented features and completed your
backlog. The code was so expressive that what started as APIs became DSLs, and it was glorious.
Writing Ruby put a smile on my face. Many languages still haven't caught up to the absolutely
incredible devex that was achieved, in a completely IDE-agnostic way.

We used Ruby for web, for configuration management, for package management, to manage virtual
machines, and to run exploits. And it was used for so many things exactly because of the devex.

Fish recently rewrote their codebase from C++ to Rust---not for performance, but for fun. That's the
energy we need to bring back into programming. As Steve wrote:

> You should write programs in the language you want to.

Or to put it differently: trying to hammer in a nail using a screwdriver is a case of using the
wrong tool for the job. Using a good programming language the team is comfortable and has fun with,
**isn't**.
