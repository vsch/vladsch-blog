## What Information Can You Trust?

When I worked as a freelance software development consultant over a two decade period I encountered all kinds of software projects and situations that were less than ideal, to say the least. From `LEGO architects` put in charge of complex software projects to hostile environments where employees were put on my team with the sole purpose of derailing my efforts through sabotage and misinformation. 

Why would a company pay me money and not want me to succeed? The company does not exist. It is an abstract concept, a legal fiction. What exists is a group of human individuals working under the umbrella of that legal fiction, who have their own goals, fears and fragile egos. It is usually the latter that winds up "snatching defeat from the jaws of victory" on every failed project.    

I cannot claim to have seen it all but I have seen how real commercial software is made. Real software efforts are constrained by available resources, schedules, market pressures and fragile human egos. They are not created in a laboratory environment with unrealistic pristine conditions: sufficient budgets and schedules, by a team of brains-in-a-jar with Spock-like logical detachment in decision making. 
 
Recently, I was told that my experience is no longer applicable: "Today with CI and TDD software development is completely different than what you know." I beg to disagree. The only thing that is different is the quality of available tools, accepted methodologies and the number of excellent software developers. What has not changed are human factors, which always were and probably always will be, the weakest link in the chain.  

The desire to feel special because we are in possession of the "ultimate answer" always blinds us from seeing the limitations of our approach. Similarly, the desire not to feel inadequate because we lack understanding, causes us to suppress opinions superior to our own because it is easier than admitting that we are full of s--t. Inevitably, this leads to unpleasant surprises when uncaring reality runs through our illusions with its mud covered boots.

Software development is a process of exploration and discovery, not a process of "transcribing" a perfect vision into working code. Vision is absolutely necessary as a guide to where you think you want to be, It cannot be cast in stone as "the ultimate goal". The latter should be treated with prescription medication instead of driving software projects.

Good software always was and always will be created the same way: iterative improvement cycles. You have to start with a simple working system which solve problems you think you understand and evolve it into a complex working system as your understanding of the real problem domain evolves. As long as humans are in charge of the task, any attempt to create a "perfect" complex working system from scratch will always fail as it has consistently failed in the past. 

This brings me around to the topic of what information can you trust? When you are responsible for fixing bugs, adding features or integrating a third party library into your project do you trust: source code comments, documentation, books or stack-overflow testimonials? 

You must take human factor into consideration. Comments and documentation can be out of sync and cannot be trusted. Who updates comments anyway? Same for documentation, which is always lagging behind, has bugs of its own and cannot possibly document bugs which you will be the first to encounter. 

Comments, documentation and books are to be used as pointers and general orienteering tools. Trust them blindly and you will encounter "unfathomable" behaviour in your code caused by "undocumented features" in software components that it depends on.  

In the end, the best and most accurate information about any program is its source code. It is not the easiest to absorb, at first, but it is the most up to date, unemotional and not concerned with fragile egos or political correctness. If your software has a critical, intimate dependence on another software component then you will eventually have no choice but to "grok" its source code and most likely fix some of its bugs.

#### Trust THE SOURCE

Source code is the final arbiter of truth about any program. It is **the program**. Everything else is but a **simplified approximation** for the acolytes. There is nothing you can do about it but learn to use the source, and **trust only what you can confirm in the source**.

[IntelliJ IDEA]: https://www.jetbrains.com/idea/#chooseYourEdition
[intellij-community]: https://github.com/JetBrains/intellij-community
