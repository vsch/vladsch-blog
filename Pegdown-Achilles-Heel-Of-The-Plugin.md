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
integrated with the JetBrains OpenAPI has its advantages as well as having one written in 
[Kotlin]. [commonmark-java] also appeared to be easier to extend. I found its implementation and 
extension architecture easier to understand. This too is a big advantage since I would need to 
add all the missing extension that pegdown had or ones that I added to pegdown over the last 
year. At the same time this parser lacks tracking of the source position in its AST that I would 
definitely need to add. Decisions, decisions, decisions. 

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
| spec.txt          |     316.491533ms |       35.156909ms |      8.863662ms |
| hang-pegdown.md   |     673.086523ms |        0.296050ms |      0.086940ms |
| hang-pegdown2.md  |    1387.808977ms |        0.294905ms |      0.085369ms |
| wrap.md           |      95.332715ms |       17.806722ms |      4.980221ms |

Ratio of performances is stunning:

| File              | pegdown-markdown | intellij-markdown | commonmark-java |
|-------------------|-----------------:|------------------:|----------------:|
| VERSION.md        |            29.69 |              3.99 |            1.00 |
| commonMarkSpec.md |            16.26 |             15.36 |            1.00 |
| spec.txt          |            35.71 |              3.97 |            1.00 |
| hang-pegdown.md   |          7741.97 |              3.41 |            1.00 |
| hang-pegdown2.md  |         16256.59 |              3.45 |            1.00 |
| wrap.md           |            19.14 |              3.58 |            1.00 |

* [VERSION.md] is the version log file I use for idea-multimarkdown 
* [commonMarkSpec.md] is a 33k line file used in [intellij-markdown] test suite for performance 
  evaluation. 
* [spec.txt] commonmark spec markdown file in the [commonmark-java] project
* [hang-pegdown.md] is a file containing a single line of 17 characters `[[[[[[[[[[[[[[[[[` which 
  causes pegdown to go into an hyper-exponential parse time. 
* [hang-pegdown2.md] a file containing a single line of 18 characters `[[[[[[[[[[[[[[[[[[` which
  causes pegdown to go into an hyper-exponential parse time.
* [wrap.md] is a file I was using to test wrap on typing performance only to discover that it has
  nothing to do with the wrap on typing code when 0.1 seconds is taken by pegdown to parse the
  file. In the plugin the parsing may happen more than once: syntax highlighter pass, psi tree 
  building pass, external annotator.

This is not an exhaustive performance test but combined with other advantages of 
[commonmark-java] over [intellij-markdown] I have enough data to convince me to make 
[commonmark-java] as my choice for the parser to use for the MultiMarkdown plugin. 

I am guestimating that it will take me a couple of months to have a version based on the new 
parser available for release. 

I look forward to having a better performing parser in the plugin. 

* * * 
Revision: 2016/04/08 - add spec.txt performance results to tables  

Revision: 2016/04/22 - add wrap.md performance results to tables and links to files used in
comparison.

[Kotlin]: http://kotlinlang.org
[Markdown]: https://daringfireball.net/projects/markdown
[idea-markdown]: https://github.com/nicoulaj/idea-markdown
[pegdown]: http://pegdown.org
[intellij-markdown]: https://github.com/valich/intellij-markdown 
[commonmark-java]: https://github.com/atlassian/commonmark-java

[commonMarkSpec.md]: https://github.com/vsch/idea-multimarkdown/blob/master/test/data/performance/commonMarkSpec.md
[hang-pegdown.md]: https://github.com/vsch/idea-multimarkdown/blob/master/test/data/performance/hang-pegdown.md
[hang-pegdown2.md]: https://github.com/vsch/idea-multimarkdown/blob/master/test/data/performance/hang-pegdown2.md
[spec.txt]: https://github.com/vsch/idea-multimarkdown/blob/master/test/data/performance/spec.md
[table.md]: https://github.com/vsch/idea-multimarkdown/blob/master/test/data/performance/table.md
[VERSION.md]: https://github.com/vsch/idea-multimarkdown/blob/master/test/data/performance/VERSION.md
[wrap.md]: https://github.com/vsch/idea-multimarkdown/blob/master/test/data/performance/wrap.md
        
