## Pegdown - Achilles heel of the MultiMarkdown plugin 

MultiMarkdown plugin uses the [pegdown] markdown parser. This was inherited from the original 
[idea-markdown] plugin and at the time it was the most flexible and complete [Markdown] 
implementation that was available.

I have felt from the beginning that I would need to replace the parser due to pegdown's 
limitations originating from its implementation. It is a recursive parser with many exponential 
or effectively infinite parsing times of some documents. 

Over the last few months major crashes and hanging bugs in the plugin have been caused by these 
bugs and limitations. I have spent literally days isolating and fixing or mitigating them. 

For example, the following string in a markdown document will cause the parser to timeout: 
`[[[[[[[[[[[[[[[[[`, which I mitigated by catching the timeout exception. Even worse is an 
infinite loop in the parser that does not generate a timeout which caused the IDE to hang during 
indexing of markdown documents. Not only is it a source of most complaints of crashes and IDE 
hanging issues it is also a major source of the typing delay in markdown documents caused by the 
plugin. The delay is annoying to say the least and I spent a fair amount of time trying to 
reduce the impact but was not able to eliminate it. 

I finally reached the decision that I have to replace pegdown in the plugin with another parser. 

A significant portion of plugin functionality would need to be rewritten to 
support the implementation of the new parser. This is no small matter since it touches most of 
the functionality added to the plugin since it was forked from [idea-markdown] 

I could no longer keep adding functionality since it would most likely depend on the parser and 
would need to be rewritten once the parser was changed. 

However, having reached the decision did not result in an immediately obvious replacement. I 
have narrowed the choices down to [intellij-markdown] or [commonmark-java] but upon reviewing 
the two parser it became obvious that both have advantages and disadvantages over each other. 
Making the decision was difficult because both parsers would require fair amount of work to 
implement all the extensions implemented in the pegdown parser and used by the plugin. I also to 
make sure that whatever parser I used would continue to be actively developed into the future. 

In this respect the [commonmark-java] appeared to be the winner because [intellij-markdown] is 
currently only supported by its original developer. At the same time using a parser already well 
integrated with the JetBrains OpenAPI has its advantages as well as having one written in [Kotlin]. 
[commonmark-java] also appeared to be easier to extend. I found its implementation and extension 
architecture easier to understand. This too is a big advantage since I would need to add all the 
missing extension that pegdown had or ones that I added to pegdown over the last year. At the 
same time this parser lacks tracking of the source position in its AST that I would definitely 
need to add. Decisions, decisions, decisions. 

I was stuck and not able to move forward. I did not want to commit to a major rewriting effort 
of the plugin without having some solid data. Superficial review of the code and perceptions 
were not enough. I also did not want to try modifying both parsers to see what would work 
better. Too much pain for the buck. 

I finally decided to do some basic profiling of the parsing times of all three parsers. If they 
were close then I would be no closer to making a decision but if there was a clear advantage 
then my mind would be made up for me. 

I used the simple code from [intellij-markdown] test suite that does a loop of 10 iterations for 
the warm up and then computes an average of 100 runs to arrive at a result. The results blew me 
away: 

| File              | pegdown-markdown | intellij-markdown | commonmark-java |  
|-------------------|-----------------:|------------------:|----------------:|
| VERSION.md        |      51.172913ms |        6.886450ms |     1.7238140ms |
| commonMarkSpec.md |     685.310908ms |      647.420365ms |     42.146776ms |
| hang-pegdown.md   |     673.086523ms |        0.296050ms |      0.086940ms |
| hang-pegdown2.md  |    1387.808977ms |        0.294905ms |      0.085369ms |

Ratio of performances is stunning:

| File              | pegdown-markdown | intellij-markdown | commonmark-java |
|-------------------|-----------------:|------------------:|----------------:|
| VERSION.md        |            29.69 |              3.99 |            1.00 |
| commonMarkSpec.md |            16.26 |             15.36 |            1.00 |
| hang-pegdown.md   |          7741.97 |              3.41 |            1.00 |
| hang-pegdown2.md  |         16256.59 |              3.45 |            1.00 |

* VERSION.md is the version log file I use for idea-multimarkdown 
* commonMarkSpec.md is a 33k line file used in [intellij-markdown] test suite for performance 
  evaluation. 
* hang-pegdown.md is a file containing a single line of 17 characters `[[[[[[[[[[[[[[[[[` which 
  causes pegdown to go into an hyper-exponential parse time. 
* a file containing a single line of 18 characters `[[[[[[[[[[[[[[[[[[` which causes pegdown to 
  go into an hyper-exponential parse time. 

This is not an exhaustive performance test but combined with other advantages of 
[commonmark-java] over [intellij-markdown] I have enough data to convince me to make 
[commonmark-java] as my choice for the parser to use for the MultiMarkdown plugin. 

I am guestimating that it will take me a couple of months to have a version based on the new 
parser available for release. 

I look forward to having a better performing parser in the plugin. 


[Kotlin]: http://kotlinlang.org
[Markdown]: https://daringfireball.net/projects/markdown
[idea-markdown]: https://github.com/nicoulaj/idea-markdown
[pegdown]: http://pegdown.org
[intellij-markdown]: https://github.com/valich/intellij-markdown 
[commonmark-java]: https://github.com/atlassian/commonmark-java

