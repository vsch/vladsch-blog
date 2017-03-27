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

