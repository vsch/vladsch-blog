## The Best IntelliJ Plugin Examples

The best source of examples of IntelliJ plugins is the [intellij-community] source code. It is also the biggest code base of plugins because most of the product functionality is implemented as extensions to the base architecture. 

Figuring out how to find your way around is a challenge. I constantly find myself distracted by interesting code that I know I will need in the future. It is very much like looking things up in an encyclopedia (that's Wikipedia on paper for those born after the internet revolution) and spending an hour reading other interesting stuff, never getting to the item that you intended to look up.

As an example, I will take you through the steps I used to figure out how and where to add "Collapse by default" options that I could see in the GUI of IDEA but had no clue how to go about implementing these for my plugin.

### Pre-requisites

I am assuming you have the [IntelliJ IDEA] installed and have gotten to the point where you can search the source, if not yet debug your own copy, of [intellij-community]. 

### Goal: Implement `collapse by default` configuration

I wanted to implement user configurable "Collapse by default" settings for markdown elements in my plugin. These are available for Java and other custom languages in settings/preferences under <kbd>Editor > General > Code Folding</kbd> 

![Blog 1 settings](https://github.com/vsch/vladsch-blog/raw/master/images/Blog_1_settings.png)

Now, I could see that plugins extend this list but where to start? Choose the most unlikely text to be repeated all over the source code and search [intellij-community] for it. I chose `I18n strings` as a promising candidate. Search in path for it at the root of the project:

![Blog 1 find I18n](https://github.com/vsch/vladsch-blog/raw/master/images/Blog_1_find_I18n.png)

Hit find and keep your fingers crossed. You can also use the preview tab but I prefer to see the results in the find tool window that way I can explore various options without having to search again. Pay dirt! We have the bundle that is used for the localization of strings:

![Blog 1 found I18n](https://github.com/vsch/vladsch-blog/raw/master/images/Blog_1_found_I18n.png)

Now we repeat the process but this time searching for the key `checkbox.collapse.i18n.messages` 

![Blog 1 find bundle key](https://github.com/vsch/vladsch-blog/raw/master/images/Blog_1_find_bundle_key.png)

Again, pay dirt `JavaCodeFoldingOptionsProvider` sounds like the class that handles customization of folding settings. In general it will be a provider for settings or a handler for actions.  

![Blog 1 found bundle key](https://github.com/vsch/vladsch-blog/raw/master/images/Blog_1_found_bundle_key.png)
                            
Now what the hell are those screaming snake case ids in strings? IntelliJ uses Java reflection API a lot so I suspect that these are properties of a settings provider.  Well, search in path to the rescue:

![Blog 1 find property](https://github.com/vsch/vladsch-blog/raw/master/images/Blog_1_find_property.png)

I was on a lucky streak: `JavaCodeFoldingSettingsBase` looks perfect for what we are looking for.

![Blog 1 found property](https://github.com/vsch/vladsch-blog/raw/master/images/Blog_1_found_property.png)

Now, I already know that both the `JavaCodeFoldingSettingsBase` and `JavaCodeFoldingOptionsProvider` need to have extension entries in the plugin.xml but which ones? Easiest part of the search. Just put your cursor on the identifier and use the Navigate to Declaration. For `JavaCodeFoldingSettingsBase` you are first taken to abstract `JavaCodeFoldingSettings` class and from there to the `IdeaPlugin.xml` file's entry for the service provider.

![Blog found plugin service](https://github.com/vsch/vladsch-blog/raw/master/images/Blog_1_found_plugin_service.png)

And the same procedure to find the entry for `JavaCodeFoldingSettingsBase`:

![Blog 1 found folding provider](https://github.com/vsch/vladsch-blog/raw/master/images/Blog_1_found_folding_provider.png)

Now it is only a matter of implementing your own classes and registering them in your plugin.xml file. 

90% of the time the hard part is finding what 3 lines of code to implement and how to get the IDE to know that those lines exist. Writing the code itself is easy. Sometimes it takes the implementation of multiple providers to have a working feature, as in the case of IntelliLang language injections, but that I will leave for another blog.  

[IntelliJ IDEA]: https://www.jetbrains.com/idea/#chooseYourEdition
[intellij-community]: https://github.com/JetBrains/intellij-community
