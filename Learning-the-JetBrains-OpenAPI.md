## Learning the JetBrains OpenAPI

Learning to come up to speed quickly with other peoples' code is a skill that every developer should have under their belt. The reason is simple. After a year, or sometimes as little as a few months, even your own code starts to look like "someone else's". Ability to orient yourself in unfamiliar code is a necessity for every active developer and not the least of which is human factors that I discussed in a previous blog: [what information can you trust](What-Information-Can-You-Trust.md).

Learning your way around the JetBrains OpenAPI platform is an effort that will take time but is not insurmountable. Just don't expect to do it in one sitting or a leisurely weekend read. Having Java and [Kotlin] under your belt is a definite plus, if not an absolute pre-requisite. The latter depends on how many C like languages you already know and how quickly you can pick up a new one.     

The learning process for doing this is as straight forward as learning anything complex can be. Fortunately, it only requires persistence and time. It does not require that you make sense of what you are reading right off the bat, only that you keep coming back and actively try to make sense of the information. Don't be discouraged if it does not make sense right away. The wonderful thing about our brain is that it learns in a non-linear chaotic process, without us being consciously aware of what happens under the hood.

A major benefit of studying the source for the JetBrains platform is that you will learn a lot of elegant solutions to complex problems. This could not be said for the many projects that I had to work on professionally. I find this a major motivating factor when I have to dive a little deeper into the code than I originally envisioned. I know in the end I will gain a lot more than another "Software Development Jack-Ass" story.

Working with [intellij-community] source base has other advantages. You are running a working version of the code you are looking at and it just happens to be the best tool to help you find your way around any code base. Not only do you get to learn how to use that tool and discover features you did not know it had, it is also the source of the best implementation examples for plugin extensions. Trying to find out how to get something done in your own plugin should be a relatively simple matter of finding the source code for a feature you can see or invoke through the GUI that does what you want to implement in your plugin.

There are hurdles to get used to. The code base is complex, multi-threaded, object oriented with use of reflection API and highly extensible through plugins, leading to implementation that tends to be spread all over the place in space and time. The hardest part of the search is first finding the right bread crumb trail to follow and then figuring out where it continues when it appears to have reached a dead-end.
 
 This is where a few tricks can speed things up until you accumulate your own "hunting" skills. These skills you must gain through your own effort. Software development is not a spectator sport. No amount of reading and doing on line tutorials and seminars will replace real battle experience you get working on real software fixing real bugs.
 
[The Best IntelliJ Plugin Examples](The-Best-IntelliJ-Plugin-Examples.md)
 
[IntelliJ IDEA]: https://www.jetbrains.com/idea/#chooseYourEdition
[intellij-community]: https://github.com/JetBrains/intellij-community
[Kotlin]: https://kotlinlang.org/
                 
