## Are We Building Software Wrong(ly)

Are we building software the wrong way? This is a serious question and I have had the nagging
feeling that the answer is yes for over a decade.

No new language, architecture or nifty pattern is going to change that. Why not? Because the
issue is an impedance mismatch between level of abstraction in the implementation domain vs the
problem domain. The hardest part of the job is finding the right abstraction map from the
implementation domain to the problem domain.

Compounding the difficulty is not only the fact that there are many maps, each with their own
advantages and limitations but that **we do not have a complete picture of the problem domain**
when we have to make these choices with serious end game consequences. We fill in the details in
that picture as we work on the solution and hope that the choices we made earlier do not lead to
a dead-end with no solution workable solution. If we are "lucky" then it works. If not, then we
blow deadlines, budgets and projects.

I do not think the limitation is in how we learn and in what F. P. Brooks Jr called the
"essential complexity" of software in "No Silver Bullet".[^fpbrooks] The technologies have
changed but the underlying problem remains: the ability to choose the right abstraction model to
map between problem and implementation domains and do it before the problem domain has been
fully understood.

As I see it, the essence of good software design lies in the ability to make the right
abstraction choices before we have the necessary knowledge to make and justify these decisions.
Effectively, prescience is a necessary talent for all software designers/developers.

Many _fads_ attempted to address this and in my opinion, all with the same lack luster success.
Back in the day "Flow Charting" for software was the rage and actually demanded of programmers
by "clueless management". Being young and always willing to test out ideas I dove into using
these beasts to help me design and develop programs. Very quickly I realized that they were
pretty much useless in helping me understand the problem or convey that understanding once it
was achieved. Flowcharts took serious effort to create and modify. They quickly fell out of sync
with the program as it evolved. The worst was that they were at a lower level of abstraction
than the program itself.

When UML became the fad "du jour" I saw it as Flowcharting on steroids

Fifteen years ago it dawned on me that I lived an illusion. I fell in love with
programming[^loveprogramming] because I hated doing repetitive work and programming allowed me
to automate the boring stuff, only to wind up doing the same thing over and over again, except
on faster hardware, bigger screens and more flexible software development systems. There was no
re-use of the most valuable element of the development process: the detailed mapping of the
problem domain. 


[^fpbrooks]: F.P. Brooks, Jr., "[No Silver Bullet](http://worrydream.com/refs/Brooks-NoSilverBullet.pdf)"--Essence and
             Accident of Software Engineering (1986).

[^loveprogramming]: I fell in love with programming when I was twelve. Back when it was called
                    programming, not software development. My first programming language was
                    Basic on a PDP-11 system at my mother's work. The next one was Z-80 assembly
                    language which I hand translated into machine code and used a hex-keypad and
                    6 digit LED display to load into the Z-80 prototype board. This was the only
                    system that I could afford at the time. 

"Fail fast", "Write software twice", "Software Prototyping", "Story Boards", "Use
Cases", etc are all aimed at discovering the problem domain before committing to an
implementation because it has been known for a long time that the cost of solving a problem is
greater the later you find it.

I agree but what I want to know is this a law of nature or 





Typed vs. untyped is a perfect example of an argument that misses the point. Typed languages let
the compiler catch bugs that untyped pass through and at best catch at run-time, at worst just
lead to undocumented features. Neither of these is an issue related to the problem domain but
implementation domain.

Do 




Regardless of the label the activity has not changed in essence, only in
details. The development environments are better, smarter and handle almost every aspect of the
process except that is not where the issue lies, as I see it.

From the beginning the industry was rife with hype and promises of a glorious future where the
task will become so easy "your grandmother could do it" and programmers, I mean developers,
would no longer be as critical to the task as they are now.

The goal posts kept shifting as the buzz words changed but no glorious future was ever achieved.
Today, the only real difference I see is that hardware horse power has upped the expectation of
what should be possible, but has not made achieving the results easier.

I would argue that most of the productivity gains are achieved because of proliferation of
reusable solutions, many of which are open sourced. This is great but does it really address the
inherent complexity of creating software? I think not. 

We are still bit-banging the software, except today we do it with larger boxes of bits. We are
not working a
